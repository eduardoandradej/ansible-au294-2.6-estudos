# Variáveis, facts e vault — Capítulo 3

Projeto autoral que materializa as seções
[3.1](../../capitulos/03-variaveis-e-vault/3.1-usando-variaveis.md),
[3.3](../../capitulos/03-variaveis-e-vault/3.3-coletando-informacoes-com-facts.md) e
[3.5](../../capitulos/03-variaveis-e-vault/3.5-protegendo-dados-com-ansible-vault.md).
Cenário próprio: uma aplicação de estoque e seu banco de dados (diferente dos
exercícios oficiais).

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | Inventário, usuário remoto e `vault_identity_list = exemplo@.vault-exemplo` |
| [ansible-navigator.yml](ansible-navigator.yml) | `stdout` e artefatos desligados (prompts e segredos) |
| [inventory](inventory) | Só hosts e grupos: as variáveis ficam fora dele |
| [group_vars/all/vars.yml](group_vars/all/vars.yml) | Padrões para todos (`porta_banco: 5432`, banner com variável dentro de variável) |
| [group_vars/db/vars.yml](group_vars/db/vars.yml) | Dados do grupo `db` em texto puro, com indireção para o segredo |
| [group_vars/db/vault.yml](group_vars/db/vault.yml) | **Cifrado** com o vault ID `exemplo` (`$ANSIBLE_VAULT;1.2;AES256;exemplo`) |
| [host_vars/db02.sp.example.net.yml](host_vars/db02.sp.example.net.yml) | Exceção de um host (`porta_banco: 5433`) |
| [vars/app.yml](vars/app.yml) | Dicionário e lista de dicionários, carregados com `vars_files` |
| [variaveis.yml](variaveis.yml) | `vars`, `vars_files`, acesso por índice/colchetes, `register`, `debug` |
| [fatos.yml](fatos.yml) | Fato customizado INI, recoleta, `set_fact`, facts no `/etc/motd`, `hostvars` e `group_names` |
| [segredos.yml](segredos.yml) | Uso da variável cifrada com `no_log: true` |

## Senha de estudo (fictícia)

O arquivo de senha **não** é versionado (padrão `.vault-*` no `.gitignore`). Para
usar o projeto, crie-o localmente:

```bash
umask 077
echo 'estudo-au294-ficticia' > .vault-exemplo
ansible-vault view group_vars/db/vault.yml     # deve mostrar o segredo fictício
```

> A senha e o segredo são **fictícios** e existem só para estudo. Em um projeto
> real, nunca publique a senha do vault, nem em README.

## Comandos de estudo

```bash
ansible-navigator inventory -m stdout --host db02.sp.example.net   # porta 5433 vence group_vars/all
ansible-navigator run variaveis.yml --syntax-check
ansible-navigator run segredos.yml --syntax-check                  # exige a senha do vault
ansible-navigator run variaveis.yml -e porta_banco=6000            # extra var vence tudo
```

## Status

✅ Validado: YAML, `--syntax-check` dos três playbooks e `ansible-lint` (perfil
*production*).
⚠️ Não executado contra hosts (nomes fictícios).
