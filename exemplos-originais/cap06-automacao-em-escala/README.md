# Automação em escala — Capítulo 6

Projeto autoral que materializa as seções
[6.1](../../capitulos/06-automacao-em-escala/6.1-incluindo-e-importando-arquivos.md) e
[6.3](../../capitulos/06-automacao-em-escala/6.3-selecionando-hosts-com-host-patterns.md).
Cenário próprio: baseline de servidores dividida em arquivos e um playbook de host
patterns (diferente dos exercícios oficiais). IPs de documentação (RFC 5737).

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | Inventário e usuário remoto |
| [ansible-navigator.yml](ansible-navigator.yml) | EE `ee-supported-rhel9`, `stdout`, sem artefatos |
| [inventory](inventory) | Hosts sem grupo (IPs), grupos por local e função, `servicos:children` |
| [tasks/instalar_e_habilitar.yml](tasks/instalar_e_habilitar.yml) | Tasks parametrizadas por `pacote` e `servico` |
| [tasks/auditoria.yml](tasks/auditoria.yml) | Regra de auditoria comum |
| [tasks/especifico_rhel10.yml](tasks/especifico_rhel10.yml) | Incluído dinamicamente com `when` |
| [plays/baseline.yml](plays/baseline.yml) | `import_tasks` com `vars` e `include_tasks` com `when` |
| [plays/monitoramento.yml](plays/monitoramento.yml) | Reuso do arquivo parametrizado para outro pacote |
| [site.yml](site.yml) | Playbook principal com `import_playbook` |
| [padroes.yml](padroes.yml) | Curinga, `&`, `!` e `ungrouped` |

## Comandos de estudo

```bash
ansible-navigator run site.yml --syntax-check
ansible-navigator run site.yml --list-tasks
ansible-navigator run -m stdout padroes.yml --list-hosts
```

## Status

✅ Validado: YAML, `--syntax-check` e `ansible-lint` (perfil *production*).
⚠️ Não executado contra hosts (nomes fictícios).
