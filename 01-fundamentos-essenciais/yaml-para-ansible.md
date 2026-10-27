# F2 — YAML para Ansible

> Lição autoral de fundamentos. Usada desde o Capítulo 1 (`ansible-navigator.yml`) e
> intensamente a partir do Capítulo 2 (playbooks).

## Por que YAML

Playbooks, o `ansible-navigator.yml`, arquivos de variáveis e muitos inventários
são YAML: um formato de dados legível, em que a **indentação é sintaxe**. Quase
todo erro de iniciante em Ansible é um erro de YAML, não de Ansible.

## As três estruturas

| Estrutura | Aparência | Em Python | Uso no Ansible |
|-----------|-----------|-----------|----------------|
| **Escalar** | `porta: 8080` · `nome: web01` · `ativo: true` | número, string, booleano | Valores de parâmetros |
| **Mapa** (dicionário) | `chave: valor` em linhas com a mesma indentação | `dict` | Um play, os argumentos de um módulo |
| **Lista** (sequência) | Itens iniciados por `- ` | `list` | Os plays de um playbook, as tasks de um play |

```yaml
---                                   # início de documento (opcional, recomendado)
servidor:                             # mapa "servidor"...
  nome: web01.example.net             # ...com três chaves escalares
  portas:                             # ...e uma lista
    - 80
    - 443
  ativo: true                         # booleano (true/false)
```

## Regras de indentação

1. **Só espaços.** Tabulação é proibida em YAML.
2. Itens irmãos ficam **na mesma coluna**.
3. Filhos ficam **mais à direita** que o pai (o padrão do curso é 2 espaços).
4. Depois de `:` e de `-`, vem um espaço.

## Lendo a forma de um playbook (prévia do Capítulo 2)

```yaml
---
- name: Exemplo de forma          # item de lista = um play (é um mapa)
  hosts: web                      #   chave do play
  tasks:                          #   chave cujo valor é uma LISTA de tasks
    - name: Primeira task         #     item da lista = uma task (é um mapa)
      ansible.builtin.ping:       #       chave = nome do módulo; valor vazio
```

Leia de fora para dentro: **lista de plays → cada play é um mapa → `tasks` é uma
lista → cada task é um mapa → o módulo é uma chave cujo valor é um mapa de argumentos.**

## Strings e aspas

| Situação | Exemplo | Por quê |
|----------|---------|---------|
| Texto simples | `msg: Servidor pronto` | Aspas desnecessárias |
| Valor começa com `{{` (variável Jinja2) | `msg: "{{ inventory_hostname }}"` | Sem aspas, o YAML interpreta `{` como início de mapa |
| Contém `: ` ou `#` | `desc: "porta: 8080 # padrão"` | Evita que vire chave ou comentário |
| Parece outro tipo | `versao: "2.10"` · `resposta: "yes"` | Evita conversão para número ou booleano |
| Lista em uma linha | `- "--tls-verify=false"` | Começa com `-`: aspas deixam claro que é string |

## Texto em várias linhas

```yaml
literal: |          # preserva quebras de linha (bom para arquivos de configuração)
  linha 1
  linha 2
dobrado: >          # junta as linhas em uma só (bom para mensagens longas)
  esta frase longa
  vira uma linha só
```

## Validar antes de executar

```bash
python3 -c 'import sys, yaml; yaml.safe_load(open(sys.argv[1]))' arquivo.yml   # parser puro
yamllint arquivo.yml                                                         # estilo e erros
ansible-lint arquivo.yml                                                     # regras de Ansible
```

## Erros clássicos

| Mensagem/sintoma | Causa |
|------------------|-------|
| `mapping values are not allowed here` | Faltou espaço após `:` ou indentação errada |
| `found character '\t' that cannot start any token` | Tabulação no arquivo |
| `expected <block end>, but found '<block sequence start>'` ou `did not find expected '-' indicator` | Itens de lista desalinhados |
| Valor `yes` virou `true`, `2.10` virou `2.1` | Falta de aspas em valores ambíguos |
| `found unhashable key` com `{{` | Expressão Jinja2 no início do valor sem aspas |

## Fixação

1. No exemplo "forma de um playbook", qual estrutura é o valor de `tasks`? E de `hosts`?
2. Por que `msg: {{ nome }}` quebra e `msg: "{{ nome }}"` funciona?
3. Qual a diferença entre `|` e `>`?

<details>
<summary>Respostas</summary>

1. `tasks` é uma **lista** (de mapas); `hosts` é um **escalar** (string).
2. Sem aspas, o YAML vê `{` e tenta ler um mapa em fluxo; com aspas, é uma string que o Ansible depois avalia como Jinja2.
3. `|` preserva as quebras de linha; `>` as transforma em espaços.

</details>

---
[← F1 Arquitetura Ansible](arquitetura-ansible.md) | [Índice](README.md) | [Próximo: F3 Automação e idempotência →](automacao-idempotencia.md)
