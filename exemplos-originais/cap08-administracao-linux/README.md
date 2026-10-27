# Administração Linux — Capítulo 8

Projeto autoral que materializa as seções da parte A do capítulo:
[8.1](../../capitulos/08-administracao-linux/8.1-usando-system-roles.md),
[8.3](../../capitulos/08-administracao-linux/8.3-automatizando-software-e-assinaturas.md) e
[8.5](../../capitulos/08-administracao-linux/8.5-automatizando-usuarios-e-autenticacao.md).
Cenário próprio: servidores de análise e de relatórios (diferente dos exercícios
oficiais). Hosts, repositório e chaves fictícios (`example.net`). ⏳ A parte B
(boot, agendamentos, armazenamento e rede) será acrescentada com o PDF 08B.

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

## Comandos de estudo

```bash
ansible-navigator run selinux.yml --syntax-check
ansible-navigator run software.yml --syntax-check
ansible-navigator run usuarios.yml --syntax-check
```

## Status

✅ Validado: YAML, `--syntax-check` e `ansible-lint` (perfil *production*).
⚠️ Não executado contra hosts (nomes, repositório e chaves fictícios).
