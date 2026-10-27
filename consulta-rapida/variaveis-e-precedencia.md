# Variáveis, facts, vault e precedência

Cobertura: **Capítulo 3**. Lições: [3.1](../capitulos/03-variaveis-e-vault/3.1-usando-variaveis.md),
[3.3](../capitulos/03-variaveis-e-vault/3.3-coletando-informacoes-com-facts.md),
[3.5](../capitulos/03-variaveis-e-vault/3.5-protegendo-dados-com-ansible-vault.md).

## Precedência (versão do curso, verificada localmente)

| # (menor → maior) | Onde |
|---|------|
| 1 | Variável de grupo no inventário (`[g:vars]`) |
| 2 | `group_vars/<g>.yml` ou `group_vars/<g>/` |
| 3 | Variável de host no inventário (`host var=valor`) |
| 4 | `host_vars/<h>.yml` ou `host_vars/<h>/` |
| 5 | Facts |
| 6 | `vars` / `vars_files` do play |
| 7 | `vars` da task |
| 8 | `-e` / `--extra-vars` |

`group_vars`/`host_vars` ao lado do **playbook** vencem os ao lado do **inventário**.
`-u`, `-b` e similares **não** são variáveis.

## Sintaxe

| Situação | Forma |
|----------|-------|
| Nome | `[A-Za-z_][A-Za-z0-9_]*`, sem palavras reservadas |
| Valor que começa com variável | `"{{ var }}"` (aspas obrigatórias) |
| Dicionário | `d['chave']['sub']` (evite `d.chave`) |
| Lista de dicionários | `l[0]['chave']` (aspas na chave!) |
| Variável composta | `destino: "{{ base }}/arquivo"` |
| Guardar resultado | `register: resultado` |
| Mostrar | `debug: msg: "..."` · `debug: var: nome` |

## Facts

| Item | Forma |
|------|-------|
| Todos | `ansible.builtin.debug: var: ansible_facts` |
| FQDN / hostname | `ansible_facts['fqdn']` / `ansible_facts['hostname']` |
| IPv4 principal | `ansible_facts['default_ipv4']['address']` |
| Kernel / distribuição | `ansible_facts['kernel']` / `ansible_facts['distribution']` |
| Forma antiga | `ansible_hostname` etc. (`inject_facts_as_vars`, padrão `true`) |
| Desligar coleta | `gather_facts: false` |
| Coletar quando quiser | `ansible.builtin.setup:` |
| Subconjunto | `gather_subset: [hardware]` · `["!hardware"]` |
| Customizados | `/etc/ansible/facts.d/<nome>.fact` (INI/JSON/script) → `ansible_facts['ansible_local']['<nome>']` |
| Derivar | `ansible.builtin.set_fact: atalho: "{{ ... }}"` |

## Variáveis mágicas

| Variável | Conteúdo |
|----------|----------|
| `inventory_hostname` | Nome do host no inventário |
| `group_names` | Grupos do host atual |
| `groups` | Todos os grupos e hosts |
| `hostvars['h']` | Variáveis (e facts já coletados) de outro host |

## Vault

| Tarefa | Comando / configuração |
|--------|------------------------|
| Criar / cifrar | `ansible-vault create <f>` · `ansible-vault encrypt <f>...` |
| Valor isolado | `ansible-vault encrypt_string --stdin-name <var>` |
| Ver / editar | `ansible-vault view <f>` · `ansible-vault edit <f>` (reescreve) |
| Decifrar | `ansible-vault decrypt <f> [--output=<novo>]` |
| Trocar senha | `ansible-vault rekey <f>` |
| Com rótulo | `--vault-id <rótulo>@prompt\|<arquivo>\|<script>` |
| Executar | `--ask-vault-pass` (com `-m stdout --pae false`) · `--vault-password-file=<f>` · `--vault-id ...` |
| `ansible.cfg` | `vault_password_file = <f>` · `vault_identity_list = a@f1,b@f2` · `vault_id_match = true` |
| Ambiente | `ANSIBLE_VAULT_PASSWORD_FILE` · `ANSIBLE_VAULT_IDENTITY_LIST` |
| Arquivo cifrado para o host | `decrypt: true` (`copy`, `template`, `unarchive`, `script`, `assemble`) |
| Ocultar saída | `no_log: true` |

Cabeçalhos: `$ANSIBLE_VAULT;1.1;AES256` (sem rótulo) · `$ANSIBLE_VAULT;1.2;AES256;<rótulo>`.

---
[Índice geral](../README.md)
