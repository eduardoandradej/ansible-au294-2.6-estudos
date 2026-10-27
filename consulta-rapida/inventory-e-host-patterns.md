# Inventário e host patterns

Cobertura: **inventário** (Capítulo 2) e **host patterns** (Capítulo 6). Lição completa: [2.1](../capitulos/02-desenvolvendo-automacao/2.1-construindo-um-inventario.md).

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

## Host patterns (Cap. 6)

Lição: [6.3](../capitulos/06-automacao-em-escala/6.3-selecionando-hosts-com-host-patterns.md).

| Pattern em `hosts:` | Alvo |
|---------------------|------|
| `host.example.net` · `192.0.2.10` | Um host (IP só se estiver listado no inventário) |
| `grupo` | Hosts do grupo (inclui filhos de `:children`) |
| `all` · `'*'` | Todos |
| `ungrouped` | Hosts sem grupo |
| `'web*'` · `'*.example.net'` · `192.0.2.*` | Curinga (casa hosts, IPs **e** grupos) |
| `a,b` | União (OU); `:` também separa, mas prefira `,` |
| `a,&b` | Interseção (E) |
| `'a,!b'` | Exclusão (NÃO) |

- Aspas quando o pattern começa com `!`, `*` ou `&`.
- A ordem dos itens não importa.
- Conferir antes: `ansible-navigator run <pb>.yml --list-hosts`.
- Restringir na execução: `--limit <pattern>` (ou `-l`).

---
[Índice geral](../README.md)
