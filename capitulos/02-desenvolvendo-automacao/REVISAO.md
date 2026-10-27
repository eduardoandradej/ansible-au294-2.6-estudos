# Revisão — Capítulo 2

Questões **autorais**. Elas não reproduzem o lab oficial nem perguntas de exame.
Responda por escrito (ou no terminal, com um `lab start` ativo) antes de abrir as
respostas.

## Parte 1 — Conceitos

1. Diferencie inventário estático de dinâmico e diga quando cada um é mais adequado.
2. O que são os grupos `all` e `ungrouped`? Um host pode estar em `ungrouped` e em outro grupo ao mesmo tempo?
3. Por que a ordem das tasks importa, mas a ordem das chaves de um play não?
4. O que é a task `Gathering Facts` e qual módulo ela executa?
5. Qual a diferença entre `ansible-navigator run` e `ansible-playbook` quanto ao ambiente de execução e ao suporte?
6. Em que ordem o Ansible decide o usuário de conexão?
7. Diferencie `command`, `shell` e `raw`. Quando `raw` é a única opção?
8. Cite três motivos para desligar artefatos de playbook.

## Parte 2 — Escreva o arquivo ou o comando

9. Um inventário INI com: `proxy.example.net` sem grupo; grupo `web` com `web01` a `web06`; grupo `db` com `db1` e `db2`; grupo `datacenter` contendo `web` e `db`; porta SSH 2200 para todo o grupo `db`. Domínio `example.net`.
10. O comando que mostra só a árvore do grupo `datacenter`.
11. O comando que mostra as variáveis efetivas de `db1.example.net`.
12. Um play que garanta, nos hosts de `web`, o pacote `nginx` instalado (sem atualizar) e o serviço ativo e habilitado.
13. Um segundo play, no mesmo playbook, que rode em `proxy.example.net` como o usuário `monitor`, sem escalada, e aguarde a porta 80 de `web01.example.net`.
14. O comando que lista os nomes das tasks de `site.yml`.
15. O comando que executa `site.yml` passo a passo.
16. O comando ad hoc que testa a conexão com o grupo `db`.
17. Um `.ansible-lint` que transforme `yaml[empty-lines]` em aviso.

## Parte 3 — Diagnóstico

18. `--host web1.example.net` falha, mas o inventário tem `web[01:06].example.net`. Explique.
19. `ansible-navigator inventory --graph ungrouped` lista `proxy.example.net`, mas `--graph datacenter` não. Por quê?
20. A saída mostra `fatal: [db1.example.net]: UNREACHABLE! ... monitor@db1.example.net: Permission denied (publickey...)`. Liste duas causas possíveis.
21. Uma task falha com `Missing sudo password`. A conexão funcionou? O que verificar?
22. Um playbook com `ansible.builtin.shell: echo "x" >> /etc/arquivo` mostra `changed` toda vez e o arquivo cresce. Proponha uma correção.
23. Um playbook roda bem no seu ambiente, mas no de um colega falha com `couldn't resolve module/action 'community.general.timezone'`. O que aconteceu?

---

<details>
<summary>Respostas comentadas</summary>

1. Estático: arquivo mantido por você (INI/YAML), ideal para frotas estáveis, laboratórios e exame. Dinâmico: plug-in ou script consulta uma fonte externa (nuvem, CMDB) a cada execução, ideal quando hosts entram e saem com frequência. Podem ser combinados.
2. `all` contém todos os hosts listados; `ungrouped`, os que não estão em nenhum outro grupo. Por definição, um host em outro grupo **não** está em `ungrouped`.
3. Tasks são itens de uma **lista** YAML (ordenada) e executam em sequência. As chaves de um play formam um **dicionário** (sem ordem).
4. Task especial executada por padrão no início de cada play; roda `ansible.builtin.setup` e coleta facts do host. Desliga-se com `gather_facts: false`.
5. `ansible-navigator run` executa dentro de um execution environment (mesmas versões em todo lugar) e é a ferramenta do AAP 2.6. `ansible-playbook` usa o Python e as collections do control node e tem suporte limitado no RHEL 9+.
6. `ansible_user` (inventário) → `remote_user` do play → `remote_user` do `ansible.cfg` → padrão (`root` no EE; usuário local com `ansible-playbook`).
7. `command`: executa sem shell. `shell`: executa pelo shell (pipes, redirecionamentos, variáveis). `raw`: envia o comando direto pelo shell remoto, sem o subsistema de módulos e sem precisar de Python; é a opção para equipamentos sem Python ou para instalar o Python.
8. Dados sensíveis gravados no JSON; prompts interativos (senha, `--step`); arquivos acumulando no diretório do projeto.
9. Exemplo:
   ```ini
   proxy.example.net

   [web]
   web[01:06].example.net

   [db]
   db[1:2].example.net

   [datacenter:children]
   web
   db

   [db:vars]
   ansible_port=2200
   ```
10. `ansible-navigator inventory -m stdout --graph datacenter`
11. `ansible-navigator inventory -m stdout --host db1.example.net`
12. Exemplo:
    ```yaml
    - name: Garantir o nginx nos servidores web
      hosts: web
      become: true
      tasks:
        - name: Garantir que o nginx está instalado
          ansible.builtin.dnf:
            name: nginx
            state: present

        - name: Garantir que o nginx está ativo e habilitado
          ansible.builtin.systemd_service:
            name: nginx
            state: started
            enabled: true
    ```
13. Exemplo:
    ```yaml
    - name: Verificar o web01 a partir do proxy
      hosts: proxy.example.net
      remote_user: monitor
      become: false
      tasks:
        - name: Aguardar a porta 80 do web01
          ansible.builtin.wait_for:
            host: web01.example.net
            port: 80
    ```
14. `ansible-navigator run site.yml --list-tasks`
15. `ansible-navigator run site.yml -m stdout --pae false --step`
16. `ansible db -m ansible.builtin.ping`
17. Exemplo:
    ```yaml
    ---
    warn_list:
      - yaml[empty-lines]
    ```
18. O range tem zero à esquerda: gerou `web01`…`web06`. `web1` não existe.
19. `proxy.example.net` não pertence a nenhum grupo (por isso está em `ungrouped`), e `datacenter` só contém os grupos `web` e `db`.
20. (a) O usuário está errado: era para conectar com outro usuário, e `monitor` veio de `ansible_user` ou de `remote_user`. (b) O usuário está certo, mas a chave pública não está no `authorized_keys` de `monitor` em `db1`.
21. Sim, a conexão funcionou (é `FAILED`, não `UNREACHABLE`). Verifique o `sudo` do usuário remoto no host (`NOPASSWD` ou não), `become`/`become_user` e, se a senha for exigida, forneça-a (`become_ask_pass`/`-K`, com `-m stdout --pae false`).
22. Trocar por um módulo idempotente: `ansible.builtin.lineinfile` para garantir uma linha (Capítulo 5), ou `ansible.builtin.copy` com `content:` se o arquivo inteiro é gerenciado.
23. A collection `community.general` não existe naquele ambiente de execução. Use um EE que a contenha ou instale a collection (Capítulo 7).

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 21–23 | Siga para o Capítulo 3 |
| 16–20 | Refaça a Parte C das lições onde errou |
| < 16 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
