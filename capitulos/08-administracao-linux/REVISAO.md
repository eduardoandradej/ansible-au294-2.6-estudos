# Revisão — Capítulo 8

Questões **autorais** sobre o capítulo inteiro (partes A e B). Elas não reproduzem o
lab oficial nem perguntas de exame. Responda por escrito antes de abrir as respostas.

## Parte 1 — Conceitos

1. Por que uma system role simplifica um parque com várias versões do RHEL?
2. Como obter as system roles no EE do curso, com assinatura do AAP e no ansible-core do RHEL?
3. Por que a role de SELinux é chamada dentro de `block`/`rescue`?
4. Diferencie `state: present` e `state: latest` no `dnf`.
5. Por que o fact `ansible_facts['packages']` pode estar desatualizado?
6. Qual a diferença entre `group` e `groups` no módulo `user`, e o papel de `append`?
7. O que `validate` garante ao editar o sudoers?
8. Quando usar `ansible.posix.at` e quando usar `ansible.builtin.cron`?
9. Com `reboot_timeout: 600`, qual a espera máxima, e por quê?
10. Quais casos a role de armazenamento suporta formalmente?
11. Qual a diferença entre `state: mounted` e `state: ephemeral` em `ansible.posix.mount`?
12. Qual `network_provider` usar no RHEL 10?

## Parte 2 — Escreva a task ou as variáveis

13. Variáveis da role `timesync` com os servidores `ntp1.example.net` e `ntp2.example.net`, com `iburst`.
14. Uma task que importe a chave `https://repo.example.net/RPM-GPG-KEY-x` e outra que declare o repositório `x-interno` (`baseurl` `https://repo.example.net/x/`, com verificação GPG).
15. Uma task que instale `tmux`, `htop` e `jq` em uma única transação.
16. Uma task que garanta o usuário `carla` nos grupos suplementares `dev` e `ops` sem remover outros grupos.
17. Uma task que autorize a chave do arquivo `files/carla.pub` do projeto para a conta `carla`.
18. Um job em `/etc/cron.d/relatorio` que rode `/usr/local/bin/relatorio` como `root` a cada 30 minutos, de segunda a sexta.
19. Uma task que torne `graphical.target` o alvo de boot de forma idempotente.
20. `storage_pools` para o VG `vg_web` no disco `vdb`, com o LV `lv_web` de `500m` em XFS montado em `/var/www`.
21. `network_connections` para a conexão `enp2s0` com `203.0.113.10/24`, gateway `203.0.113.1` e ativa.

## Parte 3 — Diagnóstico

22. A role de SELinux falha em toda execução, mesmo após o reboot manual. O que verificar?
23. Depois de instalar um pacote, uma task com `when: ansible_facts['packages']['x'] is defined` foi pulada. Por quê?
24. Um usuário perdeu acesso a um grupo depois do playbook. Causa provável?
25. O job cron aparece duplicado no crontab após mudar a task. Por quê?
26. A role de armazenamento recusa o tamanho `2G`. Corrija.

---

<details>
<summary>Respostas comentadas</summary>

1. A role escolhe o serviço ou método adequado a cada versão (ex.: `chronyd` × `ntpd`), permitindo um só playbook sem condicionais complexos.
2. No EE `ee-supported-rhel9`, já vem a collection; com AAP, `collections/requirements.yml` + `ansible-galaxy collection install`; no RHEL, o RPM `rhel-system-roles`.
3. Ela nunca reinicia o host: quando precisa, define `selinux_reboot_required` e falha. O `rescue` falha de verdade se for outra causa, ou reinicia e reaplica a role.
4. `present` garante instalado; `latest` instala ou atualiza até a versão mais recente.
5. Ele reflete o momento em que `package_facts` rodou; instalações posteriores só aparecem se o módulo for executado de novo.
6. `group` é o primário; `groups`, os suplementares. Sem `append: true`, `groups` substitui a lista existente.
7. O conteúdo é validado (ex.: `visudo -cf %s`) em um temporário antes de ir para o destino; arquivo inválido não é instalado.
8. `at` para execução única em momento futuro; `cron` para execução recorrente.
9. 1200 segundos: o limite vale para cada fase (desligar e subir; reconectar e testar).
10. Discos físicos, volume groups LVM e pools Stratis (v3+).
11. `mounted` monta e grava no `/etc/fstab`; `ephemeral` monta sem gravar no `fstab`.
12. `nm` (NetworkManager), o único suportado no RHEL 10.
13. Exemplo:
    ```yaml
    timesync_ntp_servers:
      - hostname: ntp1.example.net
        iburst: true
      - hostname: ntp2.example.net
        iburst: true
    ```
14. Exemplo:
    ```yaml
    - name: Importar a chave do repositório
      ansible.builtin.rpm_key:
        key: https://repo.example.net/RPM-GPG-KEY-x
        state: present

    - name: Declarar o repositório
      ansible.builtin.yum_repository:
        name: x-interno
        description: Repositório interno X
        baseurl: https://repo.example.net/x/
        gpgcheck: true
        enabled: true
    ```
15. Exemplo:
    ```yaml
    - name: Ferramentas em uma transação
      ansible.builtin.dnf:
        name:
          - tmux
          - htop
          - jq
        state: present
    ```
16. Exemplo:
    ```yaml
    - name: Grupos da carla
      ansible.builtin.user:
        name: carla
        groups: dev,ops
        append: true
    ```
17. Exemplo:
    ```yaml
    - name: Chave da carla
      ansible.posix.authorized_key:
        user: carla
        key: "{{ lookup('ansible.builtin.file', 'files/carla.pub') }}"
        state: present
    ```
18. Exemplo:
    ```yaml
    - name: Relatório a cada 30 minutos em dias úteis
      ansible.builtin.cron:
        name: Relatório periódico
        cron_file: relatorio
        user: root
        minute: "*/30"
        weekday: "1-5"
        job: /usr/local/bin/relatorio
    ```
19. Exemplo:
    ```yaml
    - name: Alvo gráfico no boot
      ansible.builtin.file:
        src: /usr/lib/systemd/system/graphical.target
        dest: /etc/systemd/system/default.target
        state: link
        force: true
    ```
20. Exemplo:
    ```yaml
    storage_pools:
      - name: vg_web
        type: lvm
        disks:
          - vdb
        volumes:
          - name: lv_web
            size: 500m
            fs_type: xfs
            mount_point: /var/www
            state: present
    ```
21. Exemplo:
    ```yaml
    network_provider: nm
    network_connections:
      - name: enp2s0
        type: ethernet
        state: up
        ip:
          address:
            - 203.0.113.10/24
          gateway4: 203.0.113.1
    ```
22. Se a falha é mesmo por reboot pendente (`selinux_reboot_required`) ou por outra causa (variável inválida, por exemplo); use o `block`/`rescue` e leia a mensagem da role.
23. O fact foi coletado antes da instalação; rode `package_facts` de novo antes da condição.
24. `groups` sem `append: true`: a lista de grupos suplementares foi substituída.
25. O `name` mudou; o módulo identifica o job pelo `name`, então criou outro. Remova o antigo com `state: absent` e o `name` original.
26. Use minúsculas: `2g`.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 23–26 | Siga para o Capítulo 9 |
| 18–22 | Refaça a Parte C das lições onde errou |
| < 18 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
