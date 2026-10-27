# Revisão — Capítulo 5

Questões **autorais**. Elas não reproduzem o lab oficial nem perguntas de exame.
Responda por escrito antes de abrir as respostas.

## Parte 1 — Conceitos

1. Quais módulos de arquivo vêm em `ansible.builtin` e qual dos citados no capítulo vem de `ansible.posix`?
2. Como o `copy` garante idempotência?
3. Com um execution environment, quem é o control node e por que isso importa para caminhos de arquivos?
4. Qual a diferença entre `lineinfile` e `blockinfile`? Quando usar cada um?
5. Para que servem os marcadores do `blockinfile`?
6. Quais são os valores de `state` do módulo `file` e o que cada um garante?
7. Cite quatro vantagens do módulo `template` sobre editar linha a linha.
8. Qual a diferença entre `{{ }}`, `{% %}` e `{# #}`?

## Parte 2 — Escreva a task ou o trecho

9. Copiar `files/banner` para `/etc/issue.net`, dono e grupo `root`, modo `0644`.
10. Copiar, **no próprio host**, `/etc/fstab` para `/etc/fstab.bak`, só se o backup ainda não existir.
11. Trazer `/etc/os-release` de um único host para `relatorios/os-release`, sem subdiretórios.
12. Garantir `MaxAuthTries 3` no `/etc/ssh/sshd_config`, substituindo a linha existente (comentada ou não).
13. Garantir um bloco com duas linhas em `/etc/hosts`, com marcadores `# {mark} LAB`.
14. Garantir o diretório `/srv/app` com dono `root`, modo `0755` e tipo SELinux `httpd_sys_content_t`.
15. Verificar se `/etc/estoque.conf` existe e mostrar uma mensagem só se existir.
16. Um template que gere uma linha `server <nome>` para cada item de `ntp_servidores`.
17. Uma linha de template que use `porta_app`, com `8080` se a variável não estiver definida.

## Parte 3 — Diagnóstico

18. O `copy` de um diretório criou `/srv/destino/conteudo/...` quando você queria os arquivos direto em `/srv/destino/`. Por quê?
19. O `lineinfile` acrescentou uma segunda linha `PermitRootLogin` em vez de alterar a existente. O que faltou?
20. Dois `blockinfile` no mesmo arquivo ficam sobrescrevendo um ao outro. Explique.
21. O template gera o arquivo sem o IP do host. O que verificar?
22. Você tentou escrever `{% if %}` dentro de um playbook. Por que não funciona e o que usar?

---

<details>
<summary>Respostas comentadas</summary>

1. `ansible.builtin`: `copy`, `fetch`, `lineinfile`, `blockinfile`, `file`, `stat`, `find` (e `template`). `ansible.posix.synchronize` vem de `ansible.posix`.
2. Compara o checksum SHA1 da origem com o do destino; só sobrescreve (e reporta `changed`) se forem diferentes.
3. O container do EE é o control node; o `ansible-navigator` monta o diretório do projeto dentro dele. Por isso, use caminhos relativos ao projeto para os arquivos de origem.
4. `lineinfile` garante, substitui ou remove **uma linha**; `blockinfile` gerencia um **bloco de várias linhas** como unidade. Use `lineinfile` para ajustes pontuais e `blockinfile` para seções inteiras.
5. Identificam o bloco nas execuções seguintes, garantindo idempotência (atualizar em vez de duplicar) e permitindo vários blocos independentes no mesmo arquivo.
6. `file` (arquivo existente), `directory` (diretório), `link` (link simbólico), `hard` (hard link), `touch` (cria vazio ou atualiza a data), `absent` (remove).
7. Idempotência, eficiência (uma task gera o arquivo inteiro), flexibilidade (loops e condições no template) e manutenção (um modelo central).
8. `{{ }}` insere valores; `{% %}` controla o fluxo (`for`, `if`); `{# #}` é comentário que não vai para o arquivo final.
9. Exemplo:
   ```yaml
   - name: Publicar o banner de pré-login
     ansible.builtin.copy:
       src: files/banner
       dest: /etc/issue.net
       owner: root
       group: root
       mode: '0644'
   ```
10. Exemplo:
    ```yaml
    - name: Guardar backup do fstab
      ansible.builtin.copy:
        src: /etc/fstab
        dest: /etc/fstab.bak
        remote_src: true
        force: false
        mode: '0644'
    ```
11. Exemplo:
    ```yaml
    - name: Coletar o os-release
      ansible.builtin.fetch:
        src: /etc/os-release
        dest: relatorios/
        flat: true
    ```
12. Exemplo:
    ```yaml
    - name: Limitar tentativas de autenticação
      ansible.builtin.lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?MaxAuthTries'
        line: 'MaxAuthTries 3'
    ```
13. Exemplo:
    ```yaml
    - name: Garantir entradas de laboratório
      ansible.builtin.blockinfile:
        path: /etc/hosts
        marker: "# {mark} LAB"
        block: |
          192.0.2.10 lab1.example.net
          192.0.2.11 lab2.example.net
    ```
14. Exemplo:
    ```yaml
    - name: Garantir o diretório da aplicação
      ansible.builtin.file:
        path: /srv/app
        state: directory
        owner: root
        mode: '0755'
        setype: httpd_sys_content_t
    ```
15. Exemplo:
    ```yaml
    - name: Consultar o arquivo
      ansible.builtin.stat:
        path: /etc/estoque.conf
      register: conf

    - name: Avisar que o arquivo existe
      ansible.builtin.debug:
        msg: "estoque.conf presente"
      when: conf['stat']['exists']
    ```
16. Exemplo:
    ```jinja
    {% for servidor in ntp_servidores %}
    server {{ servidor }}
    {% endfor %}
    ```
17. `porta = {{ porta_app | default('8080') }}`
18. O `src` foi informado **sem** barra final, então o diretório foi copiado junto com o conteúdo. Com `src: conteudo/`, só o conteúdo é copiado.
19. O `regexp` que casa a linha existente; sem ele, o `lineinfile` só garante que a linha exata exista e acrescenta outra.
20. Os dois usam o mesmo marcador; para o Ansible, é o mesmo bloco. Use marcadores próprios (`marker`, `marker_begin`, `marker_end`) em cada um.
21. Se os facts foram coletados (`gather_facts` não está `false`) e se a expressão usa o fact correto, por exemplo `ansible_facts['default_ipv4']['address']`.
22. Estruturas de controle Jinja2 são para templates; nos playbooks, use `when` e `loop`.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 20–22 | Siga para o Capítulo 6 |
| 15–19 | Refaça a Parte C das lições onde errou |
| < 15 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
