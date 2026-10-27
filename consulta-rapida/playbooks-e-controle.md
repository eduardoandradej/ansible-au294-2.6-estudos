# Playbooks e controle de tarefas

Cobertura: **estrutura de playbooks** (Capítulo 2). ⏳ Loops, condicionais, handlers
e tratamento de falhas chegam com o Capítulo 4.

## Esqueleto

```yaml
---
- name: <objetivo do play>          # play = item de lista
  hosts: <grupo|host|all>
  remote_user: <usuário>            # opcional: vence o ansible.cfg
  become: true                      # opcional: true/false
  become_user: root                 # opcional
  gather_facts: false               # opcional: pula ansible.builtin.setup
  tasks:
    - name: <estado desejado>       # task = item de lista
      <namespace.collection.modulo>:
        <parametro>: <valor>
```

| Regra | Detalhe |
|-------|---------|
| Ordem | Plays e tasks rodam na ordem escrita; chaves de dicionário não têm ordem |
| Indentação | Só espaços; play 2, tasks 4, módulo 6, parâmetros 8 (convenção do curso) |
| Booleanos | `true`/`false` (não `yes`/`no`) |
| Módulos | Sempre FQCN; forma expandida (sem `chave=valor` na mesma linha) |
| Octal | `mode: '0644'` entre aspas |

## Usuário e privilégio

| Prioridade do usuário de conexão | |
|---|---|
| 1 | `ansible_user` (inventário) |
| 2 | `remote_user` do play |
| 3 | `remote_user` do `ansible.cfg` |
| 4 | Padrão (`root` no EE) |

`become`, `become_user`, `become_method` no play (ou na task) sobrepõem `[privilege_escalation]`.

## Comandos arbitrários

| Módulo | Shell | Python no host | Idempotência |
|--------|-------|----------------|--------------|
| `ansible.builtin.command` | Não | Sim | Só com `creates`/`removes` |
| `ansible.builtin.shell` | Sim | Sim | Só com `creates`/`removes` |
| `ansible.builtin.raw` | Sim | **Não** | Não |

## YAML em playbooks

| Forma | Uso |
|-------|-----|
| `\|` | Bloco que preserva quebras de linha (conteúdo de arquivo) |
| `>` | Bloco que junta linhas (comando longo) |
| `'...'` | Literal (`\` não escapa) |
| `"..."` | Interpreta `\n`, `\t` |
| `{a: 1}` / `[a, b]` | Inline: evitar |

## Executar e verificar

| Tarefa | Opção de `ansible-navigator run` |
|--------|----------------------------------|
| Sintaxe | `--syntax-check` |
| Simular | `--check` (📘 `--diff` mostra diferenças) |
| Detalhe | `-v` … `-vvvvvv` |
| Passo a passo | `--step` (com `-m stdout --pae false`) |
| Começar em uma task | `--start-at-task "<nome>"` |
| Listar tasks / hosts | `--list-tasks` / `--list-hosts` |
| Sem artefato | `--pae false` |

---
[Índice geral](../README.md)
