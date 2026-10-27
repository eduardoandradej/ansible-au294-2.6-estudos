# Prática oficial — Capítulo 6

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, valores,
> arquivos de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 6.2 | Guided Exercise | `scale-files` | Não | p. 347–354 |
| 6.4 | Guided Exercise | `scale-hosts` | Não | p. 365–372 |
| 6.5 | Lab | `scale-review` | **Sim** | p. 373–383 |

Identificadores e avaliação verificados no PDF do Capítulo 6. Como nos capítulos
anteriores, cada atividade abre o projeto em um **development container** no VS Code.

---

## 6.2 Guided Exercise: Including and Importing Files

| Campo | Valor |
|-------|-------|
| Seção | 6.2 |
| Tipo | Guided Exercise |
| Identificador `lab` | `scale-files` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 347–354 |

**Competência praticada:** montar um playbook de configuração de servidor web a
partir de arquivos de tasks e de um play externo já fornecidos: incluir um arquivo
de tasks, acrescentar tasks próprias, adicionar um play de validação e comparar a
listagem de tasks com a execução.

**Domine antes:** [6.1](6.1-incluindo-e-importando-arquivos.md): import × include,
`import_playbook`, arquivos de tasks parametrizados.

```bash
lab start scale-files
lab finish scale-files
```

**Pontos de atenção:**
- Leia primeiro os arquivos do diretório `tasks` e o play em `plays/`: entenda quais variáveis cada um espera.
- Caminhos de arquivos importados/incluídos são relativos ao arquivo que os referencia.
- Compare o `--list-tasks` com a execução real: o que aparece e o que não aparece, e por quê (import × include).
- `import_playbook` fica no nível superior do playbook.

**Critério de prontidão:** você explica, para cada arquivo, se ele foi importado ou
incluído e o efeito disso.

---

## 6.4 Guided Exercise: Selecting Hosts by Using Host Patterns

| Campo | Valor |
|-------|-------|
| Seção | 6.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `scale-hosts` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 365–372 |

**Competência praticada:** ler um playbook e um inventário, prever e conferir os
hosts atingidos com `--list-hosts` e restringir a execução com `--limit`, sem alterar
o playbook, inclusive com valores que precisam de aspas.

**Domine antes:** [6.3](6.3-selecionando-hosts-com-host-patterns.md): grupos,
curingas, `,`/`&`/`!`, `--list-hosts`, `--limit`.

```bash
lab start scale-hosts
lab finish scale-hosts
```

**Pontos de atenção:**
- Antes de cada comando, escreva no papel a lista de hosts que você espera; depois compare.
- Patterns com `!`, `*` ou `&` no início precisam de aspas também na linha de comando (o shell também os interpreta).
- O objetivo é restringir **sem** editar o playbook.

**Critério de prontidão:** você acerta a lista de hosts de um pattern composto antes
de executar.

---

## 6.5 Lab: Developing Automation Content at Scale

| Campo | Valor |
|-------|-------|
| Seção | 6.5 |
| Tipo | Lab (fim de capítulo) |
| Identificador `lab` | `scale-review` |
| Avaliação | **`lab grade scale-review`** |
| Referência | PDF p. 373–383 |

**Competência avaliada:** reorganizar um playbook herdado: simplificar a lista de
hosts com um curinga, mover grupos de tasks para arquivos de tasks importados e,
por fim, consolidar as tasks repetidas (instalar pacotes e habilitar serviços) em um
único arquivo parametrizado por variáveis, importado com os valores adequados.

**Domine antes:** [6.1](6.1-incluindo-e-importando-arquivos.md) e
[6.3](6.3-selecionando-hosts-com-host-patterns.md).

```bash
lab start scale-review
# ... resolva no VS Code, dentro do development container ...
lab grade scale-review
lab finish scale-review
```

**Pontos de atenção (sem solução):**
- Antes de mexer, rode o playbook original mentalmente: quais tasks vão para cada arquivo, em que ordem.
- O curinga precisa casar **exatamente** os hosts que estavam listados; confira com `--list-hosts`.
- Use o módulo de import pedido no enunciado e os nomes de arquivo e de variável indicados.
- No arquivo consolidado, as tasks recebem as variáveis de quem importa: lembre como passar `vars` na task de import.
- Valide a sintaxe e execute; se o `lab grade` reportar FAIL, leia o critério, corrija e rode de novo; só então compare com `solutions`.

**Critério de prontidão:** `lab grade` com todos os critérios PASS **sem** consultar
a solução. Anote o tempo no diário.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 6.3 Host patterns](6.3-selecionando-hosts-com-host-patterns.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
