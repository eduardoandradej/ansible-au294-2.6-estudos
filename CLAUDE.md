# CLAUDE.md — Regras permanentes do projeto

Este arquivo orienta qualquer sessão futura do Claude Code neste repositório.
Leia-o inteiro antes de criar ou alterar conteúdo. Depois leia
[progresso/estado-do-projeto.md](progresso/estado-do-projeto.md), o
[README](README.md) e rode `git status`.

## 1. Propósito

Guia pessoal de estudos do curso **AU294 — Red Hat Enterprise Linux Automation with
Ansible**, edição 2 (2026-09-09), baseado em **Red Hat Ansible Automation Platform 2.6**,
**RHEL 10** e **ansible-core 2.16**. Objetivo final: domínio prático de automação com
Ansible e preparação para o exame **EX294**.

O repositório **não é uma tradução** da apostila. É material autoral: explicações
próprias, exemplos YAML originais, revisões e ponte para os laboratórios oficiais.
A metodologia replica a do repositório de referência
`eduardoandradej/openshift-do180-4.22-estudos` (consultado em modo somente leitura
em 2026-10-27), adaptada ao Ansible.

## 2. Regras de conteúdo (obrigatórias)

- Texto didático em **português brasileiro**; módulos, collections, comandos, opções,
  chaves YAML e nomes de configuração permanecem em **inglês**.
- Respeitar a **cronologia e a numeração oficial** de capítulos e seções.
- **Não** traduzir capítulos ou exercícios integralmente; **não** copiar parágrafos
  extensos, figuras, tabelas proprietárias, enunciados, passos de exercícios,
  arquivos de solução ou gabaritos (inclusive respostas de quizzes oficiais).
- **Não** versionar PDFs, extrações de texto, credenciais, senhas do ambiente de
  laboratório, senhas de Vault, chaves SSH, tokens, dados da assinatura, nem o nome
  ou e-mail que aparecem na marca d'água do PDF.
- **Não** reproduzir endereços IP do ambiente de sala de aula; usar só hostnames
  `*.lab.example.com` quando necessário e valores fictícios nos exemplos.
- Referências a páginas somente após verificação, no formato `PDF p. NN`, usando a
  **numeração original da apostila** (1–615), não a do arquivo segmentado.
- Identificadores de `lab` somente se verificados no PDF. Nunca inventar.
- `lab grade` apenas quando a atividade oficial aceitar avaliação (labs de fim de
  capítulo e comprehensive review).
- Conteúdo obtido de documentação pública é marcado como **📘 Fonte externa**.
- Não tratar ansible-core, pacote comunitário `ansible` e Red Hat Ansible Automation
  Platform como produtos equivalentes.
- Diferenciar exemplos **validados** (YAML/sintaxe/lint executados) de não validados.
  Nunca executar playbooks contra hosts reais ou contra o ambiente oficial.
- Regra central: **simplificar a explicação, nunca simplificar incorretamente a tecnologia.**

## 3. Formato das lições

Toda lição conceitual segue [modelos/modelo-licao.md](modelos/modelo-licao.md):
Identificação → A (problema que resolve) → B (modelo mental e arquitetura) →
C (entendimento progressivo, com diferenças entre conceitos próximos) → D (exemplo
autoral incremental) → E (execução e verificação) → F (troubleshooting) →
G (preparação para o lab) → H (fixação com respostas recolhíveis) → I (essencial).
Cada lição termina com a barra `Anterior | Índice do capítulo | Próximo`.

Cada capítulo em `capitulos/NN-nome/` contém: `README.md` (índice), um arquivo por
seção conceitual (`N.M-titulo.md`), `PRATICA-OFICIAL.md`, `REVISAO.md`, `RESUMO.md`.
Capítulos sem PDF recebido têm só um `README.md` marcado **⏳ Aguardando PDF**.

## 4. Proibições operacionais

- Não executar exercícios oficiais nem criar scripts que reproduzam ou alterem a
  infraestrutura do treinamento. Não criar avaliadores próprios (`lab grade`).
- Não copiar arquivos extraídos dos laboratórios Red Hat.
- O conteúdo precisa ser seguro para leitura pública, qualquer que seja a
  visibilidade do repositório. Não alterar a visibilidade.
- O `.gitignore` bloqueia `*.pdf`, `AU294_*`, `.vault_pass*`, `.vault-*` (arquivos de senha do vault), chaves, artefatos do
  `ansible-navigator` e `.devcontainer/`. Exemplos de `devcontainer.json` e de
  `.vscode/settings.json` ficam **dentro de Markdown**.

## 5. Fluxo de trabalho por capítulo (um PDF por sessão)

1. Ler este arquivo, `progresso/estado-do-projeto.md`, README e `git status`.
2. Extrair texto do PDF **apenas no scratchpad**, nunca dentro do repositório.
3. Confirmar seções, páginas e identificadores `lab`.
4. Produzir as lições seção por seção; depois PRATICA-OFICIAL, REVISAO, RESUMO.
5. Validar: YAML com parser, `ansible-playbook --syntax-check` e `ansible-lint` nos
   exemplos; links e âncoras por script; busca por segredos, e-mail e IPs.
6. Atualizar `progresso/` (estado, checklist, diário), README geral, README do
   capítulo, `consulta-rapida/` e `certificacao-ex294/`.
7. Commit descritivo e push. **Parar** e aguardar o próximo PDF.

Capítulo 8 chega em duas partes (08A: 8.1–8.6; 08B: 8.7–8.14). Com 08A, o capítulo
fica **🟡 parcial**; `REVISAO.md`, `RESUMO.md` e o status concluído só após 08B.
O PDF 00 (p. 1–11) alimenta `00-comecar-aqui/`.

## 6. Publicação (branch)

- Decisão do usuário: entregar diretamente em `main`, sem Pull Request, sem force push.
- **Autorização explícita (2026-10-27):** o usuário autorizou na sessão "tudo para
  `main` a partir de agora". Todo trabalho futuro é commitado e enviado para
  `origin/main` (antes, `git fetch origin main` e integração sem reescrever histórico).
- Histórico: na sessão 1 a plataforma impôs o branch
  `claude/ansible-automation-platform-26-7e98tt`; seu conteúdo foi integrado em `main`
  por fast-forward. Se uma sessão futura voltar a impor outro branch sem permitir
  push em `main`, registre a restrição e informe o usuário no relatório.
- Nunca `reset --hard`, `push --force` ou rebase arbitrário.

## 7. Estado do projeto

O estado efetivo (capítulos concluídos, fatos verificados no PDF, pendências,
situação do push e próximo passo) fica em
**[progresso/estado-do-projeto.md](progresso/estado-do-projeto.md)**.
Atualize-o ao final de cada capítulo. Documentação escrita **não** significa
laboratório realizado pelo aluno: isso só é marcado pelo próprio aluno no checklist.
