# Playbooks e controle de tarefas

Cobertura: **estrutura de playbooks** (Capítulo 2) e **controle de tarefas**
(Capítulo 4: loops, condicionais, handlers, falhas).

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

## Loops e condicionais (Cap. 4)

| Recurso | Forma |
|---------|-------|
| Loop simples | `loop:` + itens; valor atual em `item` |
| Lista em variável | `loop: "{{ lista }}"` |
| Lista de dicionários | `item['chave']` |
| Sintaxe antiga | `with_items` (achata listas), `with_file`, `with_sequence` |
| Register com loop | `var['results']`; cada item tem `item` e o retorno do módulo |
| Condição | `when: <expressão>` no nível da task |
| Operadores | `==`, `!=`, `<`, `>`, `<=`, `>=`, `is defined`, `is not defined`, `not`, `in` |
| Várias condições | `and`, `or`, lista em `when` (= `and`), parênteses |
| Facts de serviços | `ansible.builtin.service_facts` → `ansible_facts['services']` |

## Handlers (Cap. 4)

| Recurso | Forma |
|---------|-------|
| Notificar | `notify: <nome>` (ou lista) na task |
| Definir | Seção `handlers:` no play |
| Quando roda | Task notificadora `changed`; uma vez, no fim do play |
| Ordem | Ordem da seção `handlers` |
| Antecipar | `ansible.builtin.meta: flush_handlers` |

## Tratamento de falhas (Cap. 4)

| Palavra-chave | Efeito |
|---------------|--------|
| `ignore_errors: true` | Segue após a falha da task |
| `force_handlers: true` (play) | Handlers já notificados rodam mesmo após falha |
| `failed_when: <expr>` | Condição de falha personalizada |
| `changed_when: <expr>` / `false` / `true` | Condição de mudança personalizada |
| `ansible.builtin.fail` + `when` | Falha explícita com mensagem |
| `block` / `rescue` / `always` | Agrupar / recuperar / garantir |

## Imports e includes (Cap. 6)

| Módulo | Tipo | Observações |
|--------|------|-------------|
| `ansible.builtin.import_playbook` | Estático | Só no nível superior do playbook |
| `ansible.builtin.import_tasks` | Estático | `when` aplicado a cada task; sem loops; nome em variável estática; aparece no `--list-tasks` |
| `ansible.builtin.include_tasks` | Dinâmico | `when` só no include; aceita loops e dados da execução; não aparece no `--list-tasks` |

```yaml
- name: Importar tasks parametrizadas
  ansible.builtin.import_tasks: tasks/instalar_e_habilitar.yml
  vars:
    pacote: chrony
    servico: chronyd
```

## Pacotes, usuários e sudo (Cap. 8)

```yaml
- name: Vários pacotes em uma transação
  ansible.builtin.dnf:
    name: [postgresql, sqlite, jq]
    state: present          # absent | latest; '@Grupo'; name: '*' + latest = atualizar tudo

- name: Usuário sem perder grupos
  ansible.builtin.user:
    name: ana.souza
    groups: analistas
    append: true

- name: Sudo para grupo, com validação
  ansible.builtin.lineinfile:
    path: /etc/sudoers.d/analistas
    line: "%analistas ALL=(ALL) NOPASSWD: ALL"
    create: true
    mode: '0440'
    validate: /usr/sbin/visudo -cf %s
```

```yaml
- name: Job recorrente em /etc/cron.d
  ansible.builtin.cron:
    name: Limpeza noturna     # identifica o job
    cron_file: limpeza
    user: root
    minute: "0"
    hour: "3"
    job: /usr/local/bin/limpeza

- name: Alvo de boot idempotente
  ansible.builtin.file:
    src: /usr/lib/systemd/system/multi-user.target
    dest: /etc/systemd/system/default.target
    state: link
    force: true
```

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
