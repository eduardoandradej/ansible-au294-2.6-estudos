# Revisão integrada — Capítulo 9

Projeto autoral que combina conteúdos de vários capítulos e serve de gabarito para o
[simulado autoral](../../capitulos/09-revisao-geral/REVISAO.md). Cenário próprio:
portal estático de documentação com nginx em porta configurável (diferente dos labs
oficiais). Hosts fictícios (`example.net`).

| Arquivo | Papel | Capítulos |
|---------|-------|-----------|
| [ansible.cfg](ansible.cfg) | Inventário, usuário remoto, `roles_path`, `collections_path` | 1, 7 |
| [ansible-navigator.yml](ansible-navigator.yml) | EE `ee-supported-rhel9`, `stdout` | 1 |
| [inventory](inventory) | Range e dois grupos | 2 |
| [group_vars/portal/portal.yml](group_vars/portal/portal.yml) | Sobrescreve `defaults` da role; `selinux_ports` | 3, 7, 8 |
| [roles/portal_docs](roles/portal_docs/) | Role: pacotes, serviços em loop, diretório com `setype`, templates, handler, firewall | 4, 5, 7 |
| [plays/portal.yml](plays/portal.yml) | System role de SELinux com `block`/`rescue`; `import_role`; `force_handlers` | 4, 7, 8 |
| [plays/verificacao.yml](plays/verificacao.yml) | `uri` em loop com `hostvars`; `block`/`rescue`/`always` | 3, 4 |
| [site.yml](site.yml) | `import_playbook` dos dois plays | 6 |

## Comandos de estudo

```bash
ansible-navigator run site.yml --syntax-check
ansible-navigator run site.yml --list-tasks
ansible-navigator run site.yml --list-hosts
```

## Status

✅ Validado: YAML, `--syntax-check` e `ansible-lint` (perfil *production*).
⚠️ Não executado contra hosts (nomes fictícios).
