# Arquivos e templates — Capítulo 5

Projeto autoral que materializa as seções
[5.1](../../capitulos/05-deploy-de-arquivos/5.1-automatizando-gerenciamento-de-arquivos.md) e
[5.3](../../capitulos/05-deploy-de-arquivos/5.3-templates-jinja2-e-filtros.md).
Cenário próprio: logs da aplicação de estoque, journald e chrony (diferente dos
exercícios oficiais).

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | Inventário, usuário remoto e texto de `ansible_managed` |
| [ansible-navigator.yml](ansible-navigator.yml) | EE `ee-supported-rhel9`, `stdout`, sem artefatos |
| [inventory](inventory) | Grupos `ntp` e `clientes` |
| [files/rotacao-app.conf](files/rotacao-app.conf) | Política de rotação publicada com `copy` |
| [templates/chrony.conf.j2](templates/chrony.conf.j2) | `ansible_managed`, comentário Jinja2, facts, `for`, `if`, `default` |
| [templates/clientes.txt.j2](templates/clientes.txt.j2) | `groups[...]`, `loop.index`, `lower` |
| [arquivos.yml](arquivos.yml) | `copy` (com `remote_src`/`force`), `lineinfile`, `blockinfile`, `file`, `stat`, `find`, `fetch`, handler |
| [templates.yml](templates.yml) | `template` com handler e cópia com `to_nice_yaml` |

## Comandos de estudo

```bash
ansible-navigator run arquivos.yml --syntax-check
ansible-navigator run templates.yml --syntax-check
```

O `fetch` grava em `coletados/` no diretório do projeto (ignorado pelo Git).

## Status

✅ Validado: YAML, `--syntax-check` e `ansible-lint` (perfil *production*).
⚠️ Não executado contra hosts (nomes fictícios).
