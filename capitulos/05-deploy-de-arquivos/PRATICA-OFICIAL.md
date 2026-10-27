# Prática oficial — Capítulo 5

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, valores,
> arquivos de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 5.2 | Guided Exercise | `files-manage` | Não | p. 305–316 |
| 5.4 | Guided Exercise | `files-templates` | Não | p. 325–329 |
| 5.5 | Lab | `files-review` | **Sim** | p. 330–338 |

Identificadores e avaliação verificados no PDF do Capítulo 5. Como nos capítulos
anteriores, cada atividade abre o projeto em um **development container** no VS Code.

---

## 5.2 Guided Exercise: Automating File Management Tasks

| Campo | Valor |
|-------|-------|
| Seção | 5.2 |
| Tipo | Guided Exercise |
| Identificador `lab` | `files-manage` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 305–316 |

**Competência praticada:** um playbook que prepara um servidor FTP com várias
operações de arquivo (pacotes, cópia, edição de linhas e blocos, atributos,
serviço), seguido de um teste de conexão a partir de outro host; depois, um segundo
playbook com outras operações de arquivo.

**Domine antes:** [5.1](5.1-automatizando-gerenciamento-de-arquivos.md): `copy`,
`lineinfile`, `blockinfile`, `file`, `stat`, `find`, `fetch`.

```bash
lab start files-manage
lab finish files-manage
```

**Pontos de atenção:**
- Para cada task, identifique **qual módulo** o enunciado pede antes de escrever os parâmetros.
- Em edições de configuração, observe se a task usa `regexp`, `insertbefore`/`insertafter` ou marcadores de bloco.
- Confira no host o efeito das tasks (conteúdo, dono, permissões, contexto) além do `PLAY RECAP`.
- O teste de FTP a partir de outro host valida a configuração inteira.

**Critério de prontidão:** você explica por que cada operação usou aquele módulo e
não outro.

---

## 5.4 Guided Exercise: Using Jinja2 Templates and Filters

| Campo | Valor |
|-------|-------|
| Seção | 5.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `files-templates` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 325–329 |

**Competência praticada:** criar um template Jinja2 para a mensagem de login
(`/etc/motd`) usando facts e variáveis, implantá-lo com um playbook e confirmar que
o arquivo ficou personalizado nos hosts de grupos diferentes.

**Domine antes:** [5.3](5.3-templates-jinja2-e-filtros.md): delimitadores,
`ansible.builtin.template`, `templates/`, facts no template.

```bash
lab start files-templates
lab finish files-templates
```

**Pontos de atenção:**
- Revise o inventário: o resultado esperado depende dos grupos.
- O template fica no diretório `templates` do projeto.
- Valide a sintaxe do playbook antes de executar.
- Confirme o conteúdo do `/etc/motd` em mais de um host e compare.

**Critério de prontidão:** você escreve um template com facts de memória e prevê o
arquivo gerado para um host específico.

---

## 5.5 Lab: Developing Automation Content: Deploying Files

| Campo | Valor |
|-------|-------|
| Seção | 5.5 |
| Tipo | Lab (fim de capítulo) |
| Identificador `lab` | `files-review` |
| Avaliação | **`lab grade files-review`** |
| Referência | PDF p. 330–338 |

**Competência avaliada:** descobrir nomes de facts despejando-os em um host, criar
um template que usa facts de memória e processadores, e escrever um play que
implanta o template, verifica o arquivo com `stat`, mostra o resultado registrado,
copia um arquivo do projeto e cria um link simbólico, com usuário remoto e escalada
definidos no play.

**Domine antes:** [5.1](5.1-automatizando-gerenciamento-de-arquivos.md) e
[5.3](5.3-templates-jinja2-e-filtros.md); [3.3 — facts](../03-variaveis-e-vault/3.3-coletando-informacoes-com-facts.md).

```bash
lab start files-review
# ... resolva no VS Code, dentro do development container ...
lab grade files-review
lab finish files-review
```

**Pontos de atenção (sem solução):**
- Primeiro descubra os nomes exatos dos facts despejando `ansible_facts`; depois escreva o template.
- Nomes de arquivos, caminhos, donos e permissões pedidos no enunciado devem ser usados **exatamente**.
- O resultado do `stat` vai para uma variável registrada: lembre onde fica o dicionário de atributos.
- Para o link simbólico, revise os parâmetros e o `state` do `ansible.builtin.file`.
- O efeito final aparece ao fazer login no host (mensagens de `/etc/issue` e `/etc/motd`).
- Se o `lab grade` reportar FAIL, leia o critério, corrija e rode de novo; só então compare com `solutions`.

**Critério de prontidão:** `lab grade` com todos os critérios PASS **sem** consultar
a solução. Anote o tempo no diário.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 5.3 Templates e filtros](5.3-templates-jinja2-e-filtros.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
