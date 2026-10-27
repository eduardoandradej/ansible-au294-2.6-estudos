# Exemplos originais

Projetos pequenos, **autorais**, com hostnames fictícios (domínio reservado
`example.net`). Nenhum arquivo foi copiado dos laboratórios Red Hat.

| Projeto | Capítulo | Conteúdo | Validação |
|---------|----------|----------|-----------|
| [cap01-projeto-base](cap01-projeto-base/) | 1 | `ansible.cfg`, `ansible-navigator.yml`, inventário INI e playbook de conectividade | ✅ ver abaixo |
| [cap02-inventario-e-playbooks](cap02-inventario-e-playbooks/) | 2 | Inventário com grupos, ranges e `:children`; playbook de um play (NTP) e de dois plays (banco + verificação) | ✅ ver o README do projeto |
| [cap03-variaveis-fatos-vault](cap03-variaveis-fatos-vault/) | 3 | `group_vars`/`host_vars`, `vars_files`, facts customizados, `set_fact`, `hostvars`, vault ID e `no_log` | ✅ ver o README do projeto |
| [cap04-controle-de-tarefas](cap04-controle-de-tarefas/) | 4 | Loops, `when` com facts, handlers, `flush_handlers`, `force_handlers`, `changed_when`/`failed_when`, blocos | ✅ ver o README do projeto |
| [cap05-arquivos-e-templates](cap05-arquivos-e-templates/) | 5 | Módulos de arquivo, `ansible_managed`, templates com facts/`for`/`if` e filtros | ✅ ver o README do projeto |
| [cap06-automacao-em-escala](cap06-automacao-em-escala/) | 6 | `import_playbook`, `import_tasks` com `vars`, `include_tasks` com `when`, host patterns | ✅ ver o README do projeto |
| [cap07-roles-e-collections](cap07-roles-e-collections/) | 7 | Duas roles (defaults, vars, files, templates, handlers, dependência), `roles`/`include_role`, `pre_tasks`/`post_tasks`, requirements de roles e collections | ✅ ver o README do projeto |
| [cap09-revisao-integrada](cap09-revisao-integrada/) | 9 | Projeto integrado: role com templates e handler, system role de SELinux, `block`/`rescue`/`always`, `hostvars`, `import_playbook` | ✅ ver o README do projeto |
| [cap08-administracao-linux](cap08-administracao-linux/) | 8 | System roles (SELinux, storage, network), repositório e chave GPG, `package_facts`, usuários e sudo, cron/at/boot, montagens | ✅ ver o README do projeto |

## Como a validação é feita

Apenas checagens estáticas, que não executam nada: sintaxe YAML, verificação de
sintaxe do playbook e `ansible-lint` (ansible-core 2.16):

```bash
cd exemplos-originais/cap01-projeto-base
yamllint -d relaxed ansible-navigator.yml verificar-conectividade.yml
ansible-playbook --syntax-check verificar-conectividade.yml
ansible-lint verificar-conectividade.yml    # perfil production
```

⚠️ **Nenhum exemplo foi executado contra hosts.** Os nomes não resolvem na internet,
de propósito. Para usar de verdade, ajuste o inventário, o `remote_user` e a imagem
do EE para o seu ambiente.

## Estrutura prevista

Novas pastas serão criadas somente quando um capítulo justificar (por exemplo,
roles no Capítulo 7, templates no Capítulo 5).

---
[Índice geral](../README.md)
