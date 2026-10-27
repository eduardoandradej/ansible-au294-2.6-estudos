# Inventário e playbooks — Capítulo 2

Projeto autoral que materializa as seções
[2.1](../../capitulos/02-desenvolvendo-automacao/2.1-construindo-um-inventario.md),
[2.3](../../capitulos/02-desenvolvendo-automacao/2.3-desenvolvendo-playbooks.md) e
[2.5](../../capitulos/02-desenvolvendo-automacao/2.5-playbooks-com-multiplos-plays.md).
Cenários diferentes dos exercícios oficiais: servidores NTP e banco de dados.

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | Inventário do projeto, `remote_user = automacao`, `become` desligado por padrão |
| [ansible-navigator.yml](ansible-navigator.yml) | EE `ee-supported-rhel9`, `stdout`, sem artefatos |
| [inventory](inventory) | Host sem grupo, grupos por função/local/ambiente, ranges com passo, `:children`, `ansible_host`, `[app:vars]` |
| [files/chrony.conf](files/chrony.conf) | Arquivo publicado pelo `ntp.yml` (endereços de documentação) |
| [ntp.yml](ntp.yml) | **Um play**: chrony instalado, configuração, serviço, firewall |
| [site.yml](site.yml) | **Dois plays**: preparar o MariaDB (com `become`) e testar a porta a partir das aplicações (outro `remote_user`, sem `become`) |

## Comandos de estudo (com hosts reais seus)

```bash
ansible-navigator inventory -m stdout --graph
ansible-navigator inventory -m stdout --host app01.rj.example.net
ansible-navigator run ntp.yml --syntax-check
ansible-navigator run site.yml --list-hosts
ansible-navigator run site.yml --check
```

## Status

✅ Validado com ansible-core 2.16.19, ansible-lint 26.10.1 (perfil *production*) e
a collection `ansible.posix` (do pacote comunitário `ansible` 9): YAML, grafo e
variáveis do inventário, `--syntax-check`, `--list-hosts` (play 1: 2 hosts;
play 2: 5 hosts) e lint.
⚠️ Não executado contra hosts: os nomes são fictícios e os IPs são de documentação
(RFC 5737).
