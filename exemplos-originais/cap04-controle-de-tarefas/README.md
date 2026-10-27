# Controle de tarefas — Capítulo 4

Projeto autoral que materializa as seções
[4.1](../../capitulos/04-controle-de-tarefas/4.1-loops-e-tarefas-condicionais.md),
[4.3](../../capitulos/04-controle-de-tarefas/4.3-implementando-handlers.md) e
[4.5](../../capitulos/04-controle-de-tarefas/4.5-tratando-falhas-de-tarefas.md).
Cenário próprio: servidores centrais de logs com rsyslog (diferente dos exercícios
oficiais).

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | Inventário, usuário remoto, `become` desligado por padrão |
| [ansible-navigator.yml](ansible-navigator.yml) | EE `ee-supported-rhel9`, `stdout`, sem artefatos |
| [inventory](inventory) | Grupos `coletores` e `clientes` |
| [vars/logs.yml](vars/logs.yml) | Requisitos mínimos, pacotes, serviços, diretórios (lista de dicionários) e portas |
| [files/remoto.conf](files/remoto.conf) | Configuração de recepção remota do rsyslog |
| [servidor-logs.yml](servidor-logs.yml) | `fail` + `when` com facts, loops, `notify`, `flush_handlers`, handler |
| [verificacao.yml](verificacao.yml) | `force_handlers`, `changed_when`, `failed_when`, `block`/`rescue`/`always` |

## Comandos de estudo

```bash
ansible-navigator run servidor-logs.yml --syntax-check
ansible-navigator run verificacao.yml --syntax-check
```

## Status

✅ Validado: YAML, `--syntax-check` e `ansible-lint` (perfil *production*).
⚠️ Não executado contra hosts (nomes fictícios).
