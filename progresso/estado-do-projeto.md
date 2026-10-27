# Estado do projeto

> Registro do estado real do repositório para continuar em sessões futuras.
> Atualize este arquivo ao concluir cada capítulo. As regras permanentes ficam no
> [CLAUDE.md](../CLAUDE.md). Este arquivo registra **documentação produzida**, não
> aprendizagem do aluno (essa fica no [checklist](checklist-geral.md) e no [diário](diario-de-laboratorios.md)).

**Última atualização:** 2026-10-27 (sessão 7: Capítulo 7)

## Situação por módulo

Legenda: ⏳ aguardando PDF · 🟡 parcial · 📝 documentado · ✅ documentado e validado

| Módulo | Status | PDF recebido | Observações |
|--------|--------|--------------|-------------|
| Estrutura do repositório | ✅ | — | Árvore, modelos, `.gitignore`, navegação, CLAUDE.md |
| 00-comecar-aqui | ✅ | C00 (p. 1–11) | Objetivos, público, ambiente (sem IPs), comando `lab` |
| 01-fundamentos-essenciais | ✅ | — | 4 lições autorais (F1–F4) |
| Capítulo 1 | ✅ | C01 (p. 12–61) | 3 lições + prática oficial, revisão (21 questões), resumo |
| Capítulo 2 | ✅ | C02 (p. 62–140) | 4 lições + prática oficial (4 GEs + lab com `lab grade`), revisão (23 questões), resumo |
| Capítulo 3 | ✅ | C03 (p. 141–225) | 3 lições + prática oficial (3 GEs + lab com `lab grade`), revisão (25 questões), resumo |
| Capítulo 4 | ✅ | C04 (p. 226–291) | 3 lições + prática oficial (3 GEs + lab com `lab grade`), revisão (22 questões), resumo |
| Capítulo 5 | ✅ | C05 (p. 292–339) | 2 lições + prática oficial (2 GEs + lab com `lab grade`), revisão (22 questões), resumo |
| Capítulo 6 | ✅ | C06 (p. 340–384) | 2 lições + prática oficial (2 GEs + lab com `lab grade`), revisão (22 questões), resumo |
| Capítulo 7 | ✅ | C07 (p. 385–452) | 4 lições + prática oficial (quiz, 3 GEs + lab com `lab grade`), revisão (23 questões), resumo |
| Capítulo 8 | ⏳ | — | Será recebido em duas partes (08A e 08B) |
| Capítulo 9 | ⏳ | — | Só `README.md` estrutural |
| consulta-rapida | 🟡 | — | Todos os arquivos atualizados até o Cap. 7 (inclui roles, collections e templates); administração Linux aguarda o Cap. 8 |
| exemplos-originais | ✅ (Caps. 1–7) | — | `cap01` a `cap07` com checagem estática (YAML, syntax-check, lint) |
| certificacao-ex294 | 🟡 | — | Objetivos oficiais **não** conferidos (página inacessível nesta sessão) |

## Fatos verificados no PDF

- Material: `AU294-RHAAP2.6-en-2-20260909`, edição 2, data da edição 2026-09-09, publicação 2026-08-27, 615 páginas.
- Introdução (p. 1–11): objetivos, público, pré-requisito RHCSA (EX200) ou equivalente; máquinas `workstation`, `servera`–`serverd`, `utility`, `bastion` (sempre ligado), `classroom`; domínio `lab.example.com`; `lab start|grade|finish`, `grade` só em labs de fim de capítulo e comprehensive review; Tab completion.
- Capítulo 1 (p. 12–61): capa p. 12; 1.1 (p. 13–19); 1.2 Quiz (p. 20–21, sem `lab`); 1.3 (p. 22–34); 1.4 GE `intro-devenv` (p. 35–43, sem `lab grade`); 1.5 (p. 44–54); 1.6 GE `intro-configure` (p. 55–60, sem `lab grade`); 1.7 Summary (p. 61). **Sem lab de fim de capítulo.**
- Alinhamento citado: AAP 2.4 ⇔ ansible-core 2.15; AAP 2.5 e 2.6 ⇔ ansible-core 2.16.
- Imagens citadas: development tools `ansible-automation-platform-26/ansible-dev-tools-rhel9`; EE `ansible-automation-platform-26/ee-supported-rhel9` (no curso, espelhadas em um registry local em `utility`).
- Repositório RPM citado: `ansible-automation-platform-2.6-for-rhel-10-x86_64-rpms`; pacote `ansible-dev-tools`.
- Capítulo 2 (p. 62–140): abertura p. 62; 2.1 (p. 63–69); 2.2 GE `develop-inventory` (p. 70–75); 2.3 (p. 76–85); 2.4 GE `develop-singleplay` (p. 86–93); 2.5 (p. 94–102); 2.6 GE `develop-multiplay` (p. 103–109); 2.7 (p. 110–118); 2.8 GE `develop-troubleshoot` (p. 119–126); 2.9 Lab `develop-review` (p. 127–139, **com** `lab grade`); 2.10 Summary (p. 140). Sem quiz. GEs sem `lab grade`.
- Capítulo 3 (p. 141–225): 3.1 (p. 142–155); 3.2 GE `variables-vars` (p. 156–168); 3.3 (p. 169–178); 3.4 GE `variables-facts` (p. 179–187); 3.5 (p. 188–198); 3.6 GE `variables-vault` (p. 199–208); 3.7 Lab `variables-review` (p. 209–224, **com** `lab grade`); 3.8 Summary (p. 225). Sem quiz.
- Capítulo 4 (p. 226–291): 4.1 (p. 227–238); 4.2 GE `control-flow` (p. 239–244); 4.3 (p. 245–247); 4.4 GE `control-handlers` (p. 248–254); 4.5 (p. 255–260); 4.6 GE `control-errors` (p. 261–276); 4.7 Lab `control-review` (p. 277–290, **com** `lab grade`); 4.8 Summary (p. 291). Sem quiz.
- Capítulo 5 (p. 292–339): 5.1 (p. 293–304); 5.2 GE `files-manage` (p. 305–316); 5.3 (p. 317–324); 5.4 GE `files-templates` (p. 325–329); 5.5 Lab `files-review` (p. 330–338, **com** `lab grade`); 5.6 Summary (p. 339). Sem quiz.
- Capítulo 6 (p. 340–384): 6.1 (p. 341–346); 6.2 GE `scale-files` (p. 347–354); 6.3 (p. 355–364); 6.4 GE `scale-hosts` (p. 365–372); 6.5 Lab `scale-review` (p. 373–383, **com** `lab grade`); 6.6 Summary (p. 384). Sem quiz. Os exemplos de 6.3 no PDF usam IPs da sala de aula; nas lições, foram trocados por IPs de documentação.
- Capítulo 7 (p. 385–452): abertura p. 385; 7.1 (p. 386–395); 7.2 Quiz (p. 396–399, 7 questões); 7.3 (p. 400–405); 7.4 GE `roles-create` (p. 406–412); 7.5 (p. 413–419); 7.6 GE `roles-external` (p. 420–425); 7.7 (p. 426–433); 7.8 GE `roles-collections` (p. 434–440); 7.9 Lab `roles-review` (p. 441–451, **com** `lab grade`); 7.10 Summary (p. 452).
- O curso afirma que, com `ansible-navigator`, o usuário padrão de conexão é `root` (o usuário do processo no EE), e que esse `root` usa as chaves SSH do usuário da workstation.

## Diretriz de fidelidade ao material (decisão do usuário, 2026-10-27)

- O PDF é a referência definitiva. Não há testes locais nem "correções ao PDF" nas lições.
- Nos Capítulos 1–3, as notas de correção e os trechos "verificado localmente" foram removidos e o texto foi alinhado ao material oficial.
- Validação mantida: apenas checagens estáticas dos exemplos autorais (YAML, `--syntax-check`, `ansible-lint`) e de links/âncoras. Nada é executado.
- Fontes externas continuam permitidas e marcadas com 📘, sem contradizer o curso.

## Validação do Capítulo 1

- [x] Seções 1.1–1.7 representadas, na ordem; ausência de lab de fim de capítulo registrada.
- [x] Identificadores `intro-devenv` e `intro-configure` conferidos; nenhum `lab grade`.
- [x] Quiz 1.2 sem respostas reproduzidas; guided exercises sem passos nem arquivos de solução.
- [x] Sem senhas do laboratório, IPs da sala de aula, e-mail/nome da marca d'água.
- [x] Exemplos com YAML, `--syntax-check` e `ansible-lint` (perfil *production*) sem erros. **Não executados contra hosts.**
- [x] YAML embutido nos Markdown validado por parser; links relativos e âncoras verificados por script.

## Validação do Capítulo 2

- [x] Seções 2.1–2.10 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `develop-inventory`, `develop-singleplay`, `develop-multiplay`, `develop-troubleshoot` e `develop-review` conferidos; `lab grade` só no 2.9.
- [x] Guided exercises e lab sem passos, arquivos de solução ou conteúdo esperado; exemplos com cenários próprios (NTP, banco), diferentes do serviço web dos exercícios.
- [x] Sem senhas do laboratório, IPs da sala de aula, e-mail/nome da marca d'água. IPs de exemplo apenas de documentação (RFC 5737).
- [x] `cap02-inventario-e-playbooks`: YAML, `--syntax-check` e `ansible-lint` (perfil *production*) sem erros. **Não executado contra hosts.**
- [x] YAML embutido validado por parser; links e âncoras verificados por script.

## Validação do Capítulo 3

- [x] Seções 3.1–3.8 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `variables-vars`, `variables-facts`, `variables-vault` e `variables-review` conferidos; `lab grade` só no 3.7.
- [x] GEs e lab sem passos, valores (variáveis, senhas, rótulos) ou soluções; exemplos com cenário próprio (aplicação de estoque).
- [x] Sem senhas do laboratório, IPs da sala de aula, e-mail/nome da marca d'água; a senha do vault do exemplo é fictícia, documentada, e o arquivo de senha está no `.gitignore` (padrão `.vault-*` adicionado nesta sessão).
- [x] `cap03-variaveis-fatos-vault`: YAML, `--syntax-check` e `ansible-lint` (perfil *production*) sem erros. **Não executado contra hosts.**
- [x] YAML embutido validado por parser; links e âncoras verificados por script.

## Validação do Capítulo 4

- [x] Seções 4.1–4.8 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `control-flow`, `control-handlers`, `control-errors` e `control-review` conferidos; `lab grade` só no 4.7.
- [x] Conteúdo seguindo o PDF, sem testes locais nem correções; GEs e lab sem passos, valores ou soluções; exemplo com cenário próprio (servidor de logs).
- [x] `cap04-controle-de-tarefas`: YAML, `--syntax-check` e `ansible-lint` (perfil *production*) sem erros. **Não executado.**
- [x] YAML embutido validado por parser; links e âncoras verificados por script.

## Validação do Capítulo 5

- [x] Seções 5.1–5.6 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `files-manage`, `files-templates` e `files-review` conferidos; `lab grade` só no 5.5.
- [x] Conteúdo seguindo o PDF, sem testes locais nem correções; GEs e lab sem passos, valores ou soluções; exemplo com cenário próprio (logs, journald, chrony).
- [x] `cap05-arquivos-e-templates`: YAML, `--syntax-check` e `ansible-lint` (perfil *production*) sem erros. **Não executado.**
- [x] YAML embutido validado por parser; links e âncoras verificados por script.

## Validação do Capítulo 6

- [x] Seções 6.1–6.6 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `scale-files`, `scale-hosts` e `scale-review` conferidos; `lab grade` só no 6.5.
- [x] Conteúdo seguindo o PDF, sem testes locais nem correções; GEs e lab sem passos, valores ou soluções; exemplo com cenário próprio (baseline de servidores).
- [x] `cap06-automacao-em-escala`: YAML, `--syntax-check` e `ansible-lint` (perfil *production*) sem erros. **Não executado.**
- [x] YAML embutido validado por parser; links e âncoras verificados por script.

## Validação do Capítulo 7

- [x] Seções 7.1–7.10 representadas, na ordem; quiz 7.2 sem respostas reproduzidas.
- [x] Identificadores `roles-create`, `roles-external`, `roles-collections` e `roles-review` conferidos; `lab grade` só no 7.9.
- [x] Conteúdo seguindo o PDF, sem testes locais nem correções; GEs e lab sem passos, valores, senhas ou soluções; exemplo com cenário próprio (estações de administração e coletor de logs).
- [x] `cap07-roles-e-collections`: YAML, `--syntax-check` e `ansible-lint --offline` (perfil *production*) sem erros. **Não executado**; requirements não instalados (fontes fictícias).
- [x] YAML embutido validado por parser; links e âncoras verificados por script.

## Fluxo de publicação

- Pedido do usuário: commit e push direto em `main`, sem PR.
- Sessão 1: a plataforma impôs o branch `claude/ansible-automation-platform-26-7e98tt`; o trabalho foi commitado nele.
- **Push da sessão 1:** inicialmente recusado (HTTP 403, Claude GitHub App sem acesso ao repositório). Após o usuário liberar o acesso, o push para `origin/claude/ansible-automation-platform-26-7e98tt` foi concluído em 2026-10-27. Em seguida, com autorização explícita do usuário ("tudo para main a partir de agora"), o conteúdo foi integrado em `main` por fast-forward e enviado para `origin/main`.
- **A partir de agora, todo trabalho vai direto para `main`.**

## Pendências e assuntos a retomar

| Item | Quando |
|------|--------|
| Conferir objetivos públicos atuais do EX294 e preencher `certificacao-ex294/` | Assim que a página oficial estiver acessível |
| Ampliar `consulta-rapida` com cada capítulo | A cada capítulo |
| Host patterns avançados em `inventory-e-host-patterns.md` | Ao receber o Cap. 6 |
| Capítulo 8 em duas partes: manter 🟡 após 08A | Caps. 8A/8B |

## Próximo passo

Aguardar o PDF **`AU294_AAP2.6_C08A_...`** (Capítulo 8, parte A: seções 8.1–8.6,
PDF p. 453–508). Não avançar sem ele. Com 08A, o capítulo fica 🟡 parcial.
