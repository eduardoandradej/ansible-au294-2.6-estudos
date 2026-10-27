# Inventário e host patterns

Cobertura: **inventário** (Capítulo 2). ⏳ Host patterns avançados chegam com o
Capítulo 6. Lição completa: [2.1](../capitulos/02-desenvolvendo-automacao/2.1-construindo-um-inventario.md).

## Sintaxe INI

```ini
# host sem grupo (ungrouped)
solto.example.net

[web]
web[01:04].example.net            # range (zeros à esquerda contam)
web10.example.net ansible_port=2222

[db]
db[a:c].example.net               # range alfabético

[producao]
web[01:04:2].example.net          # range com passo: 01 e 03

[dc:children]                     # membros são grupos
web
db

[db:vars]                         # variáveis para o grupo inteiro
ansible_user=dba
```

| Elemento | Regra |
|----------|-------|
| Comentário | Linha iniciada por `#` |
| Grupos implícitos | `all` (todos) e `ungrouped` (sem outro grupo) |
| Host × grupo | Não podem ter o mesmo nome |
| `[x:vars]` | Variáveis `chave=valor` para o grupo inteiro |
| `[x]` + `[x:children]` | Hosts próprios e herdados se somam |

## Variáveis de conexão

| Variável | Uso |
|----------|-----|
| `ansible_host` | Endereço real de conexão |
| `ansible_port` | Porta SSH |
| `ansible_user` | Usuário SSH (vence `remote_user` do play e do `ansible.cfg`) |
| `ansible_connection` | Plug-in de conexão |
| `ansible_ssh_private_key_file` | Chave privada |

## Consultar

| Tarefa | Comando |
|--------|---------|
| Árvore | `ansible-navigator inventory -m stdout --graph [grupo]` |
| JSON completo | `ansible-navigator inventory -m stdout --list` |
| Variáveis de um host | `ansible-navigator inventory -m stdout --host <host>` |
| TUI | `ansible-navigator inventory` (`:0` grupos, `:1` hosts) |
| Outro inventário | `-i <caminho>` (sobrepõe `inventory=` do `ansible.cfg`) |
| Hosts de cada play (📘) | `ansible-navigator run <pb>.yml --list-hosts` |

## Host patterns já vistos

| Padrão em `hosts:` | Alvo |
|--------------------|------|
| `all` | Todos os hosts |
| `<grupo>` | Hosts do grupo (incluindo filhos) |
| `<fqdn>` | Um host |

⏳ Combinações, exclusões e curingas: Capítulo 6.

---
[Índice geral](../README.md)
