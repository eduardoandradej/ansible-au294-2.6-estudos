# Revisão — Capítulo 3

Questões **autorais**. Elas não reproduzem o lab oficial nem perguntas de exame.
Responda por escrito (ou no terminal, com um `lab start` ativo) antes de abrir as
respostas.

## Parte 1 — Conceitos

1. Ordene, da menor para a maior precedência: `host_vars`, `-e`, variável de grupo no inventário, `vars` do play, `group_vars`, `vars` da task, facts, variável de host no inventário.
2. Quando usar `vars`, `vars_files`, `group_vars` e `host_vars`?
3. Por que a Red Hat recomenda colchetes em vez de notação de ponto?
4. O que é um fact? Qual módulo coleta os facts e quando ele roda?
5. Diferencie um fact customizado de uma variável criada com `set_fact`.
6. O que são variáveis mágicas? Cite quatro e o que contêm.
7. O que o Ansible Vault protege e o que ele **não** protege?
8. Qual a diferença entre os cabeçalhos `$ANSIBLE_VAULT;1.1;AES256` e `$ANSIBLE_VAULT;1.2;AES256;prod`?

## Parte 2 — Escreva o arquivo ou o comando

9. Em `group_vars/web.yml`, defina `porta_http: 8080` e um dicionário `site` com `nome: intranet` e `raiz: /srv/intranet`.
10. A expressão que lê `raiz` do dicionário `site`.
11. Uma task que crie o diretório de `site['raiz']` com modo `0755`.
12. Uma task que mostre o FQDN e o IPv4 principal do host em uma mensagem.
13. O conteúdo de `/etc/ansible/facts.d/manutencao.fact` (INI) com seção `janela`, chaves `dia=domingo` e `hora=02:00`, e a expressão que lê `hora`.
14. Um play que não colete facts automaticamente, mas colete só os facts de rede em uma task.
15. O comando que cifra `group_vars/db/vault.yml` com o rótulo `prod`, lendo a senha de `.vault-prod`.
16. O comando que executa `site.yml` pedindo a senha de vault interativamente com o `ansible-navigator`.
17. A configuração do `ansible.cfg` para que os rótulos `dev` e `prod` usem `.vault-dev` e `.vault-prod`.
18. Uma task que entregue `files/app.key` (cifrado) decifrado em `/etc/app/app.key`, modo `0600`.

## Parte 3 — Diagnóstico

19. `name: {{ pacote }}` gera um erro que fala em aspas. Explique e corrija.
20. `porta` vale `80` em `group_vars/all.yml`, mas um host recebe `9000` e você não sabe de onde vem. Como investigar?
21. `{{ contas[0][nome] }}` falha com `'nome' is undefined`. Por quê?
22. A task depois da publicação de um `.fact` não enxerga `ansible_local`. O que falta?
23. O playbook falha com `Attempting to decrypt but no vault secrets found`. Liste três formas de resolver.
24. A senha do banco apareceu na saída de uma task que falhou. O que faltou?
25. Você cifrou o `ansible.cfg` para esconder um caminho e agora nada funciona. Explique.

---

<details>
<summary>Respostas comentadas</summary>

1. Grupo no inventário < `group_vars` < host no inventário < `host_vars` < facts < `vars` do play < `vars` da task < `-e`.
2. `vars`: poucas variáveis específicas do play. `vars_files`: muitas variáveis ou reaproveitadas entre playbooks (inclusive arquivos cifrados). `group_vars`: valores por grupo de hosts. `host_vars`: valores de um host específico.
3. Porque a notação de ponto colide com métodos e atributos do Python (`items`, `keys`, `copy`...) e falha de formas difíceis de diagnosticar.
4. Uma variável com informação descoberta no managed host (SO, rede, hardware). É coletada pelo `ansible.builtin.setup`, por padrão no início de cada play (task `Gathering Facts`).
5. O fact customizado mora no host (`/etc/ansible/facts.d/*.fact`) e persiste entre execuções; o `set_fact` cria uma variável por host que existe só durante a execução.
6. Variáveis definidas pelo próprio Ansible, de nomes reservados: `inventory_hostname` (nome no inventário), `group_names` (grupos do host atual), `groups` (todos os grupos e hosts), `hostvars` (variáveis de todos os hosts).
7. Protege dados **em repouso** (arquivos no repositório). Não protege valores em uso: saída, logs e artefatos, que exigem `no_log` e artefatos desligados.
8. 1.1: senha única, sem rótulo (legado). 1.2: cifrado com o vault ID `prod`, gravado no cabeçalho.
9. Exemplo:
   ```yaml
   ---
   porta_http: 8080
   site:
     nome: intranet
     raiz: /srv/intranet
   ```
10. `site['raiz']`
11. Exemplo:
    ```yaml
    - name: Garantir a raiz do site
      ansible.builtin.file:
        path: "{{ site['raiz'] }}"
        state: directory
        mode: '0755'
    ```
12. Exemplo:
    ```yaml
    - name: Identificar o host
      ansible.builtin.debug:
        msg: "{{ ansible_facts['fqdn'] }} usa {{ ansible_facts['default_ipv4']['address'] }}"
    ```
13. Arquivo:
    ```ini
    [janela]
    dia=domingo
    hora=02:00
    ```
    Expressão: `ansible_facts['ansible_local']['manutencao']['janela']['hora']`.
14. Exemplo:
    ```yaml
    - name: Só facts de rede
      hosts: all
      gather_facts: false
      tasks:
        - name: Coletar facts de rede
          ansible.builtin.setup:
            gather_subset:
              - network
    ```
15. `ansible-vault encrypt group_vars/db/vault.yml --vault-id prod@.vault-prod`
16. `ansible-navigator run site.yml -m stdout --pae false --ask-vault-pass`
17. `vault_identity_list = dev@.vault-dev,prod@.vault-prod` na seção `[defaults]`.
18. Exemplo:
    ```yaml
    - name: Entregar a chave decifrada
      ansible.builtin.copy:
        src: files/app.key
        dest: /etc/app/app.key
        mode: '0600'
        decrypt: true
    ```
19. Sem aspas, o YAML interpreta `{` no início do valor como dicionário. Corrija para `name: "{{ pacote }}"`.
20. Percorra a escada de precedência de cima para baixo: `-e` na execução, `vars` de task e de play, facts, `host_vars`, variável de host no inventário, `group_vars` do grupo. Ferramentas: `ansible-navigator inventory -m stdout --host <h>` (variáveis de inventário) e `grep -Rw porta:` (definições no projeto).
21. Sem aspas, `nome` é tratado como **variável**, que não existe. Use `contas[0]['nome']`.
22. Recoletar facts depois de criar o arquivo (`ansible.builtin.setup`, por exemplo com `filter: ansible_local`).
23. `--ask-vault-pass` (com `-m stdout --pae false`), `--vault-password-file=<arq>`, `--vault-id rotulo@origem`, `vault_password_file`/`vault_identity_list` no `ansible.cfg`, ou as variáveis `ANSIBLE_VAULT_PASSWORD_FILE`/`ANSIBLE_VAULT_IDENTITY_LIST`.
24. `no_log: true` na task.
25. O Ansible lê a configuração antes de ter acesso ao vault; um `ansible.cfg` cifrado não é interpretado (erro de seção ausente). Restaure o arquivo em texto puro.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 23–25 | Siga para o Capítulo 4 |
| 18–22 | Refaça a Parte C das lições onde errou |
| < 18 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
