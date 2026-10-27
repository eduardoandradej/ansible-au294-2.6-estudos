# Roles e collections — Capítulo 7

Projeto autoral que materializa as seções
[7.1](../../capitulos/07-roles-e-collections/7.1-definindo-a-estrutura-de-roles.md),
[7.3](../../capitulos/07-roles-e-collections/7.3-criando-roles.md),
[7.5](../../capitulos/07-roles-e-collections/7.5-implantando-roles-de-fontes-externas.md) e
[7.7](../../capitulos/07-roles-e-collections/7.7-roles-e-modulos-de-collections.md).
Cenário próprio: estações de administração e um coletor de logs (diferente dos
exercícios oficiais). Hosts e fontes fictícios (`example.net`).

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | `roles_path` e `collections_path` apontando para o projeto |
| [ansible-navigator.yml](ansible-navigator.yml) | EE `ee-supported-rhel9`, `stdout`, sem artefatos |
| [inventory](inventory) | Grupos `estacoes_admin` e `coleta` |
| [roles/ferramentas_admin](roles/ferramentas_admin/) | Role com `defaults`, template, handler, `meta` e README |
| [roles/coletor_logs](roles/coletor_logs/) | Role com `files`, `vars` internas, módulo `ansible.posix.firewalld` e dependência |
| [roles/requirements.yml](roles/requirements.yml) | Manifesto de role externa (Git fictício, versão fixa) |
| [collections/requirements.yml](collections/requirements.yml) | Manifesto de collections com versão |
| [group_vars/coleta/coletor.yml](group_vars/coleta/coletor.yml) | Sobrescreve um `default` da role |
| [site.yml](site.yml) | Seção `roles` com parâmetro e `include_role` |
| [ordem.yml](ordem.yml) | `pre_tasks`, `roles`, `tasks`, `post_tasks` |

## Comandos de estudo

```bash
ansible-galaxy collection install -r collections/requirements.yml -p collections
ansible-galaxy role list
ansible-navigator run site.yml --syntax-check
ansible-navigator run ordem.yml --list-tasks
```

## Status

✅ Validado: YAML, `--syntax-check` e `ansible-lint` (perfil *production*).
⚠️ Não executado contra hosts (nomes fictícios); requirements não instalados (fontes fictícias).
