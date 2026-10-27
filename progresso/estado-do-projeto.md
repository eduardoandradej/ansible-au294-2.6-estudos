# Estado do projeto

> Registro do estado real do repositório para continuar em sessões futuras.
> Atualize este arquivo ao concluir cada capítulo. As regras permanentes ficam no
> [CLAUDE.md](../CLAUDE.md). Este arquivo registra **documentação produzida**, não
> aprendizagem do aluno (essa fica no [checklist](checklist-geral.md) e no [diário](diario-de-laboratorios.md)).

**Última atualização:** 2026-10-27 (sessão 1: estrutura inicial + Capítulo 0 + Capítulo 1)

## Situação por módulo

Legenda: ⏳ aguardando PDF · 🟡 parcial · 📝 documentado · ✅ documentado e validado

| Módulo | Status | PDF recebido | Observações |
|--------|--------|--------------|-------------|
| Estrutura do repositório | ✅ | — | Árvore, modelos, `.gitignore`, navegação, CLAUDE.md |
| 00-comecar-aqui | ✅ | C00 (p. 1–11) | Objetivos, público, ambiente (sem IPs), comando `lab` |
| 01-fundamentos-essenciais | ✅ | — | 4 lições autorais (F1–F4) |
| Capítulo 1 | ✅ | C01 (p. 12–61) | 3 lições + prática oficial, revisão (21 questões), resumo |
| Capítulos 2–7 | ⏳ | — | Só `README.md` estrutural, a partir do sumário (PDF p. 3–5) |
| Capítulo 8 | ⏳ | — | Será recebido em duas partes (08A e 08B) |
| Capítulo 9 | ⏳ | — | Só `README.md` estrutural |
| consulta-rapida | 🟡 | — | Comandos, configuração, troubleshooting, glossário e módulos cobrem o Cap. 1; demais páginas aguardam capítulos |
| exemplos-originais | ✅ (Cap. 1) | — | `cap01-projeto-base` validado |
| certificacao-ex294 | 🟡 | — | Objetivos oficiais **não** conferidos (página inacessível nesta sessão) |

## Fatos verificados no PDF

- Material: `AU294-RHAAP2.6-en-2-20260909`, edição 2, data da edição 2026-09-09, publicação 2026-08-27, 615 páginas.
- Introdução (p. 1–11): objetivos, público, pré-requisito RHCSA (EX200) ou equivalente; máquinas `workstation`, `servera`–`serverd`, `utility`, `bastion` (sempre ligado), `classroom`; domínio `lab.example.com`; `lab start|grade|finish`, `grade` só em labs de fim de capítulo e comprehensive review; Tab completion.
- Capítulo 1 (p. 12–61): capa p. 12; 1.1 (p. 13–19); 1.2 Quiz (p. 20–21, sem `lab`); 1.3 (p. 22–34); 1.4 GE `intro-devenv` (p. 35–43, sem `lab grade`); 1.5 (p. 44–54); 1.6 GE `intro-configure` (p. 55–60, sem `lab grade`); 1.7 Summary (p. 61). **Sem lab de fim de capítulo.**
- Alinhamento citado: AAP 2.4 ⇔ ansible-core 2.15; AAP 2.5 e 2.6 ⇔ ansible-core 2.16.
- Imagens citadas: development tools `ansible-automation-platform-26/ansible-dev-tools-rhel9`; EE `ansible-automation-platform-26/ee-supported-rhel9` (no curso, espelhadas em um registry local em `utility`).
- Repositório RPM citado: `ansible-automation-platform-2.6-for-rhel-10-x86_64-rpms`; pacote `ansible-dev-tools`.

## Correções e complementos (marcados nas lições)

- **Chave `transport`:** o PDF (p. 49) apresenta o plug-in de conexão do `ansible.cfg` como `connection`; no ansible-core 2.16 a chave INI é `transport` (`DEFAULT_TRANSPORT`). Verificado localmente: `connection = local` é ignorado.
- **Comentário inline:** em `ansible.cfg`, `;` comenta inline; `#` só no início da linha (verificado: `timeout = 30 # x` gera erro de tipo).
- **Diretório gravável por todos:** `ansible.cfg` ignorado (verificado localmente; fonte externa).
- **`remote_user` vazio:** curso diz `root` no EE; documentação descreve o padrão do plug-in de conexão. Ambos registrados.
- Fontes externas marcadas com 📘: `visudo -cf`, `ansible-config dump/list`, `ansible-inventory --graph`, chaves de `settings.json` das extensões, pull policy `tag`, repasse de variáveis `ANSIBLE_*` ao EE (verificado no código do navigator 26.10.0), nome padrão dos artefatos e do log do navigator.

## Validação do Capítulo 1

- [x] Seções 1.1–1.7 representadas, na ordem; ausência de lab de fim de capítulo registrada.
- [x] Identificadores `intro-devenv` e `intro-configure` conferidos; nenhum `lab grade`.
- [x] Quiz 1.2 sem respostas reproduzidas; guided exercises sem passos nem arquivos de solução.
- [x] Sem senhas do laboratório, IPs da sala de aula, e-mail/nome da marca d'água.
- [x] Exemplos validados com ansible-core 2.16.19, ansible-lint 26.10.1 (perfil *production*), ansible-navigator 26.10.0 e yamllint 1.38.0. **Não executados contra hosts.**
- [x] YAML embutido nos Markdown validado por parser; links relativos e âncoras verificados por script.

## Fluxo de publicação

- Pedido do usuário: commit e push direto em `main`, sem PR.
- Restrição real desta sessão: a plataforma impõe o branch `claude/ansible-automation-platform-26-7e98tt` e proíbe push em outro branch sem permissão explícita na sessão. O trabalho foi commitado **localmente** nesse branch.
- **Push da sessão 1 recusado (HTTP 403):** o Claude não tinha acesso de escrita ao repositório no GitHub (app do Claude não instalado/vinculado para a conta). O commit ficou apenas no container da sessão. Depois de corrigir o acesso, é preciso fazer o push (e a integração em `main`, a critério do usuário).

## Pendências e assuntos a retomar

| Item | Quando |
|------|--------|
| Conferir objetivos públicos atuais do EX294 e preencher `certificacao-ex294/` | Assim que a página oficial estiver acessível |
| Integrar o branch de trabalho em `main` | A critério do usuário |
| Ad hoc commands (`ansible -m`), se o curso abordar | Ao receber o Cap. 2 |
| Ampliar `consulta-rapida` com cada capítulo | A cada capítulo |
| Capítulo 8 em duas partes: manter 🟡 após 08A | Caps. 8A/8B |

## Próximo passo

Aguardar o PDF **`AU294_AAP2.6_C02_Desenvolvendo_Automacao_p062-140.pdf`**
(Capítulo 2, p. 62–140). Não avançar sem ele.
