# Exemplos originais

Projetos pequenos, **autorais**, com hostnames fictícios (domínio reservado
`example.net`). Nenhum arquivo foi copiado dos laboratórios Red Hat.

| Projeto | Capítulo | Conteúdo | Validação |
|---------|----------|----------|-----------|
| [cap01-projeto-base](cap01-projeto-base/) | 1 | `ansible.cfg`, `ansible-navigator.yml`, inventário INI e playbook de conectividade | ✅ ver abaixo |
| [cap02-inventario-e-playbooks](cap02-inventario-e-playbooks/) | 2 | Inventário com grupos, ranges e `:children`; playbook de um play (NTP) e de dois plays (banco + verificação) | ✅ ver o README do projeto |
| [cap03-variaveis-fatos-vault](cap03-variaveis-fatos-vault/) | 3 | `group_vars`/`host_vars`, `vars_files`, facts customizados, `set_fact`, `hostvars`, vault ID e `no_log` | ✅ ver o README do projeto |

## Como a validação é feita

Com `ansible-core` 2.16.19, `ansible-lint` 26.10.1, `ansible-navigator` 26.10.0 e
`yamllint` 1.38.0, em ambiente isolado (sem hosts reais). Collections fora de
`ansible.builtin` (ex.: `ansible.posix`) vêm do pacote comunitário `ansible` 9,
baseado no ansible-core 2.16, apontado por `ANSIBLE_COLLECTIONS_PATH`:

```bash
cd exemplos-originais/cap01-projeto-base
yamllint -d relaxed ansible-navigator.yml verificar-conectividade.yml
ansible-config dump --only-changed          # o ansible.cfg do projeto é lido?
ansible-inventory --graph                   # o inventário resolve os grupos?
ansible-playbook --syntax-check verificar-conectividade.yml
ansible-lint verificar-conectividade.yml    # perfil production
ansible-navigator settings --effective --ee false -m stdout   # o ansible-navigator.yml é aceito?
```

⚠️ **Nenhum exemplo foi executado contra hosts.** Os nomes não resolvem na internet,
de propósito. Para usar de verdade, ajuste o inventário, o `remote_user` e a imagem
do EE para o seu ambiente.

## Estrutura prevista

Novas pastas serão criadas somente quando um capítulo justificar (por exemplo,
roles no Capítulo 7, templates no Capítulo 5).

---
[Índice geral](../README.md)
