# Prática oficial — Capítulo 4

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, valores,
> arquivos de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 4.2 | Guided Exercise | `control-flow` | Não | p. 239–244 |
| 4.4 | Guided Exercise | `control-handlers` | Não | p. 248–254 |
| 4.6 | Guided Exercise | `control-errors` | Não | p. 261–276 |
| 4.7 | Lab | `control-review` | **Sim** | p. 277–290 |

Identificadores e avaliação verificados no PDF do Capítulo 4. Como nos capítulos
anteriores, cada atividade abre o projeto em um **development container** no VS Code.

---

## 4.2 Guided Exercise: Using Loops and Conditional Tasks

| Campo | Valor |
|-------|-------|
| Seção | 4.2 |
| Tipo | Guided Exercise |
| Identificador `lab` | `control-flow` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 239–244 |

**Competência praticada:** gerenciar usuários em hosts remotos com tasks que
iteram sobre listas de dicionários e só rodam conforme um fact do host (o modo do
SELinux).

**Domine antes:** [4.1](4.1-loops-e-tarefas-condicionais.md): `loop` sobre lista de
dicionários, `item['chave']`, `when` com facts.

```bash
lab start control-flow
lab finish control-flow
```

**Pontos de atenção:**
- Leia o inventário antes de escrever o playbook: as variáveis com as listas de usuários vêm de lá.
- `loop` e `when` ficam no nível da task, não dentro do módulo.
- Antes de executar, preveja em quais hosts cada task vai aparecer como `skipping`; depois compare com a saída.

**Critério de prontidão:** você explica, host por host, por que cada item foi
aplicado ou pulado.

---

## 4.4 Guided Exercise: Implementing Handlers

| Campo | Valor |
|-------|-------|
| Seção | 4.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `control-handlers` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 248–254 |

**Competência praticada:** completar um playbook de aplicação web em que tasks de
configuração notificam handlers diferentes, que reiniciam os serviços definidos por
variáveis, e verificar que os handlers só rodam quando notificados por uma task que
mudou algo.

**Domine antes:** [4.3](4.3-implementando-handlers.md): `notify`, seção `handlers`,
quando os handlers rodam.

```bash
lab start control-handlers
lab finish control-handlers
```

**Pontos de atenção:**
- Revise as variáveis do playbook antes de escrever as tasks: os handlers usam esses nomes de serviço.
- O texto do `notify` deve ser **idêntico** ao `name` do handler.
- A seção `handlers` fica no nível do play, ao lado de `tasks`.
- Compare a primeira e a segunda execução: em qual delas aparece `RUNNING HANDLER`, e por quê?

**Critério de prontidão:** você prevê, antes de executar, quais handlers vão rodar.

---

## 4.6 Guided Exercise: Handling Task Failure

| Campo | Valor |
|-------|-------|
| Seção | 4.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `control-errors` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 261–276 |

**Competência praticada:** uma sequência de playbooks curtos para observar cada
mecanismo: o efeito de `ignore_errors`, handlers forçados após falha com
`force_handlers`, condições que mudam conforme uma variável passada na linha de
comando, e um bloco que ganha `rescue` e `always`.

**Domine antes:** [4.5](4.5-tratando-falhas-de-tarefas.md): `ignore_errors`,
`force_handlers`, `failed_when`/`changed_when`, `block`/`rescue`/`always`.

```bash
lab start control-errors
lab finish control-errors
```

**Pontos de atenção:**
- Em cada etapa, execute **antes e depois** da mudança pedida e compare o `PLAY RECAP`.
- Observe quais contadores mudam (`failed`, `ignored`, `rescued`).
- Com `force_handlers`, confira o efeito no host (o exercício pede uma verificação de login).
- Uma das execuções passa uma variável com `-e`: note como isso altera qual task roda.

**Critério de prontidão:** para cada mecanismo, você descreve em uma frase o
comportamento observado.

---

## 4.7 Lab: Developing Automation Content: Task Control

| Campo | Valor |
|-------|-------|
| Seção | 4.7 |
| Tipo | Lab (fim de capítulo) |
| Identificador `lab` | `control-review` |
| Avaliação | **`lab grade control-review`** |
| Referência | PDF p. 277–290 |

**Competência avaliada:** completar um playbook que implanta um servidor NFS e
exporta compartilhamentos, usando falha antecipada com `ansible.builtin.fail` e
condições sobre facts, loops sobre listas de variáveis, um bloco de verificação
com recuperação que notifica um handler, configuração de firewall e o handler que
reinicia os serviços.

**Domine antes:** [4.1](4.1-loops-e-tarefas-condicionais.md),
[4.3](4.3-implementando-handlers.md) e [4.5](4.5-tratando-falhas-de-tarefas.md).

```bash
lab start control-review
# ... resolva no VS Code, dentro do development container ...
lab grade control-review
lab finish control-review
```

**Pontos de atenção (sem solução):**
- O playbook já vem com comentários marcando onde cada task entra: respeite a ordem.
- As variáveis estão em um arquivo do projeto: leia-o antes e use os nomes exatos.
- Na condição de falha antecipada, identifique os dois facts necessários (memória e distribuição) e combine as condições corretamente.
- "Não atualizar pacotes já instalados" corresponde a um valor específico de `state`.
- No bloco de verificação, pense em como uma task de `debug` pode notificar um handler (o enunciado dá a dica).
- Nomes de tasks, handlers e mensagens pedidos no enunciado devem ser usados **exatamente**.
- Se o `lab grade` reportar FAIL, leia o critério, corrija e rode de novo; só então compare com `solutions`.

**Critério de prontidão:** `lab grade` com todos os critérios PASS **sem** consultar
a solução. Anote o tempo no diário.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 4.5 Falhas](4.5-tratando-falhas-de-tarefas.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
