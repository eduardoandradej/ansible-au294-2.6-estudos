# Administração Linux — Capítulo 8

Projeto autoral que materializa as seções conceituais do capítulo:
[8.1](../../capitulos/08-administracao-linux/8.1-usando-system-roles.md),
[8.3](../../capitulos/08-administracao-linux/8.3-automatizando-software-e-assinaturas.md),
[8.5](../../capitulos/08-administracao-linux/8.5-automatizando-usuarios-e-autenticacao.md),
[8.7](../../capitulos/08-administracao-linux/8.7-automatizando-boot-e-agendamentos.md),
[8.9](../../capitulos/08-administracao-linux/8.9-automatizando-armazenamento.md) e
[8.11](../../capitulos/08-administracao-linux/8.11-automatizando-rede.md).
Cenário próprio: servidores de análise e de relatórios (diferente dos exercícios
oficiais). Hosts, repositório, chaves e endereços fictícios (`example.net`, RFC 5737,
MAC de documentação).

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | Inventário, usuário remoto e `collections_path` |
| [ansible-navigator.yml](ansible-navigator.yml) | EE `ee-supported-rhel9` (já inclui `redhat.rhel_system_roles`) |
| [inventory](inventory) | Grupos `analise` e `relatorios` |
| [collections/requirements.yml](collections/requirements.yml) | `redhat.rhel_system_roles` (só para atualizar) |
| [group_vars/relatorios/selinux.yml](group_vars/relatorios/selinux.yml) | Variáveis da role de SELinux |
| [selinux.yml](selinux.yml) | System role de SELinux com `block`/`rescue` para reboot |
| [software.yml](software.yml) | `rpm_key`, `yum_repository`, `dnf` com lista, `package_facts`, `assert` |
| [vars/equipe.yml](vars/equipe.yml) | Grupo e membros da equipe |
| [usuarios.yml](usuarios.yml) | `group`, `user`, `authorized_key`, sudo e `sshd_config` com `validate` e handler |
| [agendamentos.yml](agendamentos.yml) | `cron` (usuário e `/etc/cron.d`), `at`, timer, alvo de boot e `reboot` |
| [group_vars/relatorios/storage.yml](group_vars/relatorios/storage.yml) | VG, LVs (absoluto, `%VG`) e swap para a role `storage` |
| [armazenamento.yml](armazenamento.yml) | Role `storage`, montagem NFS e facts de montagens |
| [host_vars/rel01.example.net/network.yml](host_vars/rel01.example.net/network.yml) | Conexão para a role `network` |
| [rede.yml](rede.yml) | `hostname`, role `network`, `firewalld` e facts de rede |

## Comandos de estudo

```bash
ansible-navigator run selinux.yml --syntax-check
ansible-navigator run software.yml --syntax-check
ansible-navigator run usuarios.yml --syntax-check
ansible-navigator run agendamentos.yml --syntax-check
ansible-navigator run armazenamento.yml --syntax-check
ansible-navigator run rede.yml --syntax-check
```

## Status

✅ Validado: YAML, `--syntax-check` e `ansible-lint` (perfil *production*).
⚠️ Não executado contra hosts (todos os nomes e endereços são fictícios).
