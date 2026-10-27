# Revisão — Capítulo 9 (simulado autoral integrado)

Exercícios **autorais** que misturam todo o curso, no formato de especificações (como
os labs de revisão). Eles **não** reproduzem os labs oficiais nem perguntas de exame.
Faça em um ambiente de prática seu (nunca no ambiente oficial fora das atividades),
escreva os arquivos e só depois compare com as respostas, que são **um** caminho
possível. Referência de projeto pronto:
[exemplos-originais/cap09-revisao-integrada](../../exemplos-originais/cap09-revisao-integrada/).

Tempo sugerido: 90 minutos para as Partes 1 a 3.

## Cenário

Hosts fictícios: `docs01.example.net` e `docs02.example.net` (grupo `portal`) e
`mon01.example.net` (grupo `apoio`). Usuário remoto `automacao`, com sudo.

## Parte 1 — Projeto e inventário

1. Escreva o `ansible.cfg` do projeto: inventário `./inventory`, usuário remoto `automacao`, roles em `./roles` e collections em `./collections` e no EE.
2. Escreva o inventário com os grupos `portal` (use range) e `apoio`, e um grupo `todos` que contenha os dois.
3. Qual comando lista os hosts que o pattern `'portal,!docs02*'` atinge em `site.yml`?

## Parte 2 — Role e variáveis

4. Crie o esqueleto da role `portal_docs` e diga quais diretórios você apagaria se a role não usa `files/`, `vars/` nem `tests/`.
5. Em qual arquivo da role fica `portal_docs_porta: 8080`, e como o grupo `portal` passa a usar 8081 sem tocar na role?
6. Escreva as tasks da role que instalam `nginx` e `firewalld` em uma transação e garantem os dois serviços ativos e habilitados.
7. Escreva a task que publica `/etc/nginx/conf.d/portal.conf` a partir de template e o handler que recarrega o nginx.
8. Escreva um template de página que liste `portal_docs_secoes` numeradas, ou mostre "Nenhuma seção publicada." se a lista estiver vazia.

## Parte 3 — Plays e controle

9. Escreva o play que aplica a role ao grupo `portal`, com privilégio e handlers forçados mesmo se algo falhar.
10. Escreva o play, no grupo `apoio`, que testa a página de cada servidor do portal com `ansible.builtin.uri` dentro de `block`, falha com mensagem clara no `rescue` e sempre mostra quais servidores foram testados.
11. Escreva o `site.yml` que importa os dois plays.
12. Antes de publicar, rotule a porta do portal como `http_port_t` usando a system role de SELinux, com o tratamento de reboot recomendado.

## Parte 4 — Administração (escreva só as variáveis ou a task)

13. `storage_pools` para o VG `vg_portal` em `vdb`, com `lv_conteudo` de `1g` (XFS em `/srv/portal`).
14. Job em `/etc/cron.d/portal_backup` que rode `/usr/local/bin/backup-portal` como `root` às 01h15 todos os dias.
15. Conta `editor` no grupo `editores` (criar o grupo), com senha a partir de `vault_editor_hash` em um arquivo do Vault.
16. Sudo sem senha para `editores`, validado.

## Parte 5 — Diagnóstico

17. A verificação falha só em `docs02`. Liste, em ordem, as camadas que você verificaria.
18. A role foi aplicada, mas o grupo `portal` continua na porta 8080. Por quê?
19. O `--list-tasks` não mostra as tasks da role. Em que situação isso é esperado?

---

<details>
<summary>Respostas comentadas</summary>

1. Exemplo:
   ```ini
   [defaults]
   inventory = ./inventory
   remote_user = automacao
   roles_path = ./roles
   collections_path = ./collections:/usr/share/ansible/collections
   ```
2. Exemplo:
   ```ini
   [portal]
   docs[01:02].example.net

   [apoio]
   mon01.example.net

   [todos:children]
   portal
   apoio
   ```
3. `ansible-navigator run site.yml --list-hosts --limit 'portal,!docs02*'` (ou o pattern no `hosts:` do play e `--list-hosts`).
4. `ansible-galaxy role init roles/portal_docs`; apagar `files/`, `vars/` e `tests/`.
5. Em `defaults/main.yml`; `group_vars/portal/<arquivo>.yml` com `portal_docs_porta: 8081` (inventário vence `defaults`).
6. Exemplo:
   ```yaml
   - name: Garantir os pacotes do portal
     ansible.builtin.dnf:
       name:
         - nginx
         - firewalld
       state: present

   - name: Garantir os serviços ativos e habilitados
     ansible.builtin.systemd_service:
       name: "{{ item }}"
       state: started
       enabled: true
     loop:
       - nginx
       - firewalld
   ```
7. Ver [roles/portal_docs/tasks/main.yml](../../exemplos-originais/cap09-revisao-integrada/roles/portal_docs/tasks/main.yml) e [handlers/main.yml](../../exemplos-originais/cap09-revisao-integrada/roles/portal_docs/handlers/main.yml): `ansible.builtin.template` com `notify: Recarregar o nginx` e handler `ansible.builtin.systemd_service` com `state: reloaded`.
8. Ver [index.html.j2](../../exemplos-originais/cap09-revisao-integrada/roles/portal_docs/templates/index.html.j2): `{% if portal_docs_secoes | length > 0 %}` com `{% for %}` e `loop.index`; `{% else %}` com a mensagem.
9. Exemplo:
   ```yaml
   - name: Publicar o portal
     hosts: portal
     become: true
     force_handlers: true
     tasks:
       - name: Aplicar a role do portal
         ansible.builtin.import_role:
           name: portal_docs
   ```
10. Ver [plays/verificacao.yml](../../exemplos-originais/cap09-revisao-integrada/plays/verificacao.yml): `uri` com `status_code: 200` em loop sobre `groups['portal']`, usando `hostvars[item]['portal_docs_porta']`; `rescue` com `ansible.builtin.fail`; `always` com `debug`.
11. Ver [site.yml](../../exemplos-originais/cap09-revisao-integrada/site.yml): dois `ansible.builtin.import_playbook` no nível superior.
12. `selinux_ports` em `group_vars/portal` e `include_role` de `redhat.rhel_system_roles.selinux` dentro de `block`, com `rescue` que falha se `not selinux_reboot_required`, reinicia e reaplica (ver [plays/portal.yml](../../exemplos-originais/cap09-revisao-integrada/plays/portal.yml)).
13. Exemplo:
    ```yaml
    storage_pools:
      - name: vg_portal
        type: lvm
        disks:
          - vdb
        volumes:
          - name: lv_conteudo
            size: 1g
            fs_type: xfs
            mount_point: /srv/portal
            state: present
    ```
14. Exemplo:
    ```yaml
    - name: Backup diário do portal
      ansible.builtin.cron:
        name: Backup diário do portal
        cron_file: portal_backup
        user: root
        minute: "15"
        hour: "1"
        job: /usr/local/bin/backup-portal
    ```
15. Exemplo (com `vars_files` apontando para o arquivo do Vault e execução com `--ask-vault-pass` ou arquivo de senha):
    ```yaml
    - name: Garantir o grupo editores
      ansible.builtin.group:
        name: editores
        state: present

    - name: Garantir a conta editor
      ansible.builtin.user:
        name: editor
        groups: editores
        append: true
        password: "{{ vault_editor_hash }}"
    ```
16. Exemplo:
    ```yaml
    - name: Sudo sem senha para editores
      ansible.builtin.lineinfile:
        path: /etc/sudoers.d/editores
        line: "%editores ALL=(ALL) NOPASSWD: ALL"
        create: true
        owner: root
        group: root
        mode: '0440'
        validate: /usr/sbin/visudo -cf %s
    ```
17. Conectividade e inventário (o host responde ao `ping`?), resultado da role em `docs02` (`PLAY RECAP`), serviço ativo, firewall (porta na zona), SELinux (porta rotulada), conteúdo e configuração do site.
18. A variável está definida em `vars/main.yml` da role (precedência maior que o inventário), ou o arquivo de `group_vars` não está no diretório/grupo certo.
19. Quando a role é incluída com `include_role` (dinâmico): só a task de inclusão aparece. Com `import_role` ou seção `roles`, as tasks aparecem.

</details>

## Autoavaliação

| Resultado | Ação |
|-----------|------|
| Partes 1–3 em até 90 min, sem consulta | Faça os labs oficiais no tempo indicado e siga para o [roteiro do EX294](../../certificacao-ex294/roteiro-de-revisao.md) |
| Precisou consultar em até 5 itens | Revise as lições ligadas no [mapa de objetivos](9.1-mapa-de-objetivos.md) e refaça |
| Mais de 5 consultas | Repita os labs de fim de capítulo correspondentes e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
