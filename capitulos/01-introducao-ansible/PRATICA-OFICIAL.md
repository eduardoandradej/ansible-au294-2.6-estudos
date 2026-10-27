# Prática oficial — Capítulo 1

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, arquivos
> de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais estão no enunciado de cada atividade
> e **não** devem ser copiadas para este repositório.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 1.2 | Quiz | — (sem comando `lab`) | — | p. 20–21 |
| 1.4 | Guided Exercise | `intro-devenv` | Não | p. 35–43 |
| 1.6 | Guided Exercise | `intro-configure` | Não | p. 55–60 |

Identificadores verificados no PDF do Capítulo 1. O capítulo **não tem lab de fim
de capítulo**: nenhuma atividade aceita `lab grade`.

Ambiente: `workstation` (onde você trabalha), `servera`–`serverd` (managed hosts) e
`utility` (serviços de apoio do curso, como o servidor Git e um registry de
containers local), todos em `lab.example.com`. Detalhes em
[ambiente-oficial.md](../../00-comecar-aqui/ambiente-oficial.md).

---

## 1.2 Quiz: Automating Tasks with Ansible

| Campo | Valor |
|-------|-------|
| Seção | 1.2 |
| Tipo | Quiz (6 questões de múltipla escolha/verdadeiro-falso) |
| Identificador `lab` | Não se aplica |
| Avaliação | Autoavaliação (a solução está no próprio PDF) |
| Referência | PDF p. 20–21 |

**Competência avaliada:** vocabulário e conceitos da seção 1.1: arquitetura,
protocolo padrão, arquivo que descreve as ações, formato desse arquivo, conteúdo do
`ansible-core` e idempotência.

**Domine antes:** [1.1](1.1-automatizando-tarefas-com-ansible.md), Partes B, C e I.

**Pontos de atenção:**
- Leia cada alternativa contra a definição exata da lição, não pela "cara" da palavra.
- Uma das questões testa a separação entre `ansible-core` e collections: releia a Parte C.3 da lição 1.1.
- Responda **antes** de abrir a página de solução.

---

## 1.4 Guided Exercise: Configuring Your Ansible Development Environment

| Campo | Valor |
|-------|-------|
| Seção | 1.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `intro-devenv` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 35–43 |

**Competência praticada:** montar o ambiente de desenvolvimento do curso. Clonar
um repositório do servidor Git do curso pelo VS Code, configurar a extensão Ansible
(lint e execution environment) e a Dev Containers (Podman), gerar o devcontainer,
apontá-lo para a imagem das development tools do registry local, reabrir o projeto
dentro do container, executar um playbook simples via `ansible-navigator run` e
fazer stage, commit e push da alteração.

**Domine antes:** [1.3](1.3-configurando-o-ambiente-de-desenvolvimento.md):
development container × execution environment, configurações de User × Workspace,
ciclo Git.

```bash
lab start intro-devenv
lab finish intro-devenv
```

**Pontos de atenção:**
- Observe em **qual subaba** (User ou Workspace) cada configuração é feita e em qual `settings.json` ela acaba sendo gravada.
- O registry do curso usa certificado próprio: entenda **por que** o exercício desliga a verificação TLS e por que isso não deve ir para produção.
- Ao clicar em **Create** no assistente do devcontainer, a confirmação é uma mensagem de log, não uma janela.
- A primeira abertura do container pode levar alguns minutos (download da imagem).
- No `PLAY RECAP`, confira `failed=0` e `unreachable=0`. Pergunte-se por que a task de mensagem resulta em `ok` e não em `changed`.
- Antes do push, veja o contador do ícone *Source Control* e confirme o que está em *Staged Changes*.
- Se o VS Code oferecer `git fetch` periódico, o exercício orienta recusar; o motivo é não gerar ruído no ambiente.
- Feche a conexão remota ao final (*File › Close Remote Connection*) antes do `lab finish`.

**Critério de prontidão:** você consegue repetir o fluxo em outro projeto sem
roteiro e explicar para que serve cada extensão e cada container.

---

## 1.6 Guided Exercise: Configuring Ansible Settings

| Campo | Valor |
|-------|-------|
| Seção | 1.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `intro-configure` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 55–60 |

**Competência praticada:** criar os dois arquivos de configuração de um projeto.
Escrever o `ansible-navigator.yml` (engine, imagem, política e argumentos de pull,
modo de saída), baixar e listar a imagem com `ansible-navigator images`, escrever o
`ansible.cfg` (inventário, usuário remoto, `ask_pass`), testar a conectividade com
playbooks de `ping` em dois grupos do inventário, desligar os artefatos de playbook
e explorar a origem dos parâmetros com `ansible-navigator config`.

**Domine antes:** [1.5](1.5-configurando-ajustes-do-ansible.md): precedência,
chaves do `ansible-navigator.yml`, leitura da coluna `Default`, TUI do navigator.

```bash
lab start intro-configure
lab finish intro-configure
```

**Pontos de atenção:**
- Escreva os arquivos **de memória** primeiro e só depois compare com o enunciado. Indentação YAML errada no `ansible-navigator.yml` é o erro mais comum.
- O projeto define `mode: stdout`. Para ver a TUI, o exercício sobrepõe o modo **só naquele comando** com `-m`.
- Depois das primeiras execuções, procure os arquivos `*-artifact-*.json` no projeto, entenda de onde vieram e confirme que não surgem mais após desligar os artefatos.
- Na TUI do `config`, use o filtro e abra os detalhes de um parâmetro: localize `env`, `ini`, `source` e `via`.
- Dentro do devcontainer, o caminho do projeto aparece sob `/workspaces/`, não sob `/home/student/`.

**Critério de prontidão:** você explica por que o `ping` funcionou com o usuário
configurado, o que aconteceria sem `remote_user` e onde conferir isso.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 1.5 Configurando o Ansible](1.5-configurando-ajustes-do-ansible.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
