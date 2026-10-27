# Estado do projeto

> Registro do estado real do repositório para continuar em sessões futuras.
> Atualize este arquivo ao concluir cada capítulo. As regras permanentes ficam no
> [CLAUDE.md](../CLAUDE.md). Este arquivo registra **documentação produzida**, não
> aprendizagem do aluno (essa fica no [checklist](checklist-geral.md) e no [diário](diario-de-laboratorios.md)).

**Última atualização:** 2026-10-27 (sessão 3: Capítulo 3)

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
| Capítulos 4–7 | ⏳ | — | Só `README.md` estrutural, a partir do sumário (PDF p. 3–5) |
| Capítulo 8 | ⏳ | — | Será recebido em duas partes (08A e 08B) |
| Capítulo 9 | ⏳ | — | Só `README.md` estrutural |
| consulta-rapida | 🟡 | — | Comandos, configuração, troubleshooting, glossário, módulos, inventário e playbooks cobrem os Caps. 1–2; variáveis cobertas pelo Cap. 3; roles/templates aguardam capítulos |
| exemplos-originais | ✅ (Caps. 1–3) | — | `cap01-projeto-base`, `cap02-inventario-e-playbooks` e `cap03-variaveis-fatos-vault` validados |
| certificacao-ex294 | 🟡 | — | Objetivos oficiais **não** conferidos (página inacessível nesta sessão) |

## Fatos verificados no PDF

- Material: `AU294-RHAAP2.6-en-2-20260909`, edição 2, data da edição 2026-09-09, publicação 2026-08-27, 615 páginas.
- Introdução (p. 1–11): objetivos, público, pré-requisito RHCSA (EX200) ou equivalente; máquinas `workstation`, `servera`–`serverd`, `utility`, `bastion` (sempre ligado), `classroom`; domínio `lab.example.com`; `lab start|grade|finish`, `grade` só em labs de fim de capítulo e comprehensive review; Tab completion.
- Capítulo 1 (p. 12–61): capa p. 12; 1.1 (p. 13–19); 1.2 Quiz (p. 20–21, sem `lab`); 1.3 (p. 22–34); 1.4 GE `intro-devenv` (p. 35–43, sem `lab grade`); 1.5 (p. 44–54); 1.6 GE `intro-configure` (p. 55–60, sem `lab grade`); 1.7 Summary (p. 61). **Sem lab de fim de capítulo.**
- Alinhamento citado: AAP 2.4 ⇔ ansible-core 2.15; AAP 2.5 e 2.6 ⇔ ansible-core 2.16.
- Imagens citadas: development tools `ansible-automation-platform-26/ansible-dev-tools-rhel9`; EE `ansible-automation-platform-26/ee-supported-rhel9` (no curso, espelhadas em um registry local em `utility`).
- Repositório RPM citado: `ansible-automation-platform-2.6-for-rhel-10-x86_64-rpms`; pacote `ansible-dev-tools`.
- Capítulo 2 (p. 62–140): abertura p. 62; 2.1 (p. 63–69); 2.2 GE `develop-inventory` (p. 70–75); 2.3 (p. 76–85); 2.4 GE `develop-singleplay` (p. 86–93); 2.5 (p. 94–102); 2.6 GE `develop-multiplay` (p. 103–109); 2.7 (p. 110–118); 2.8 GE `develop-troubleshoot` (p. 119–126); 2.9 Lab `develop-review` (p. 127–139, **com** `lab grade`); 2.10 Summary (p. 140). Sem quiz. GEs sem `lab grade`.
- A abertura do Capítulo 2 (p. 62) repete o objetivo do Capítulo 1 (provável erro editorial); o README do capítulo usa um objetivo reescrito a partir das seções e do resumo.
- Capítulo 3 (p. 141–225): 3.1 (p. 142–155); 3.2 GE `variables-vars` (p. 156–168); 3.3 (p. 169–178); 3.4 GE `variables-facts` (p. 179–187); 3.5 (p. 188–198); 3.6 GE `variables-vault` (p. 199–208); 3.7 Lab `variables-review` (p. 209–224, **com** `lab grade`); 3.8 Summary (p. 225). Sem quiz.
- O curso afirma que, com `ansible-navigator`, o usuário padrão de conexão é `root` (o usuário do processo no EE), e que esse `root` usa as chaves SSH do usuário da workstation.

## Correções e complementos (marcados nas lições)

- **Chave `transport`:** o PDF (p. 49) apresenta o plug-in de conexão do `ansible.cfg` como `connection`; no ansible-core 2.16 a chave INI é `transport` (`DEFAULT_TRANSPORT`). Verificado localmente: `connection = local` é ignorado.
- **Comentário inline:** em `ansible.cfg`, `;` comenta inline; `#` só no início da linha (verificado: `timeout = 30 # x` gera erro de tipo).
- **Diretório gravável por todos:** `ansible.cfg` ignorado (verificado localmente; fonte externa).
- **`remote_user` vazio:** curso diz `root` no EE; documentação descreve o padrão do plug-in de conexão. Ambos registrados.
- **Inventário INI × `ansible.cfg` (Cap. 2, verificado):** no inventário, `#` comenta também no fim da linha e `;` inline **quebra** o parse; no `ansible.cfg` é o contrário. Host listado depois de `[grupo:vars]` invalida o arquivo inteiro; grupo filho inexistente em `:children` gera `includes undefined group`.
- **Usuário de conexão (Cap. 2, verificado com `-vvv`):** `ansible_user` > `remote_user` do play > `remote_user` do `ansible.cfg`.
- **Plays seguintes (Cap. 2, verificado):** se todos os hosts de um play falham, os plays seguintes não rodam.
- **`doc -s` (Cap. 2, verificado):** funciona antes (`ansible-navigator -s doc <m>`, forma do curso) e depois do módulo.
- **IDs de regras do ansible-lint 26.10.1 (Cap. 2, verificado):** `yaml[trailing-spaces]`, `fqcn[action-core]`, `no-free-form`, `yaml[octal-values]`, `yaml[empty-lines]`, `no-changed-when`; `skip_list`/`warn_list` no `.ansible-lint` funcionam como descrito; o navigator aceita `ansible-lint.config`.
- **Precedência de variáveis (Cap. 3, verificado):** os 8 níveis da versão do curso, testados um a um com `connection: local`.
- **Correções ao PDF do Cap. 3 (verificadas):** p. 152 `local_users[0][name]` sem aspas falha (`'name' is undefined`); p. 172 fact injetado vence o inventário mas perde para `vars` do play; p. 188 `ansible.cfg` cifrado não é lido (inventário cifrado funciona); p. 197 `ansible.builtin.postgresql_user` não existe (`community.postgresql.postgresql_user`).
- **Outros comportamentos verificados (Cap. 3):** notação de ponto em chave `items` retorna método Python; `"!hardware"` sem aspas quebra o YAML; `.fact` INI gera strings; `inject_facts_as_vars = false` torna `ansible_*` indefinido; cabeçalhos 1.1/1.2; `vault_identity_list`; `decrypt: true/false`; `rekey --new-vault-id`; `decrypt --output` preserva o original; erro `vault-ids default,default` ao duplicar a origem da senha; `inventory --host` mostra valores decifrados.
- Fontes externas marcadas com 📘: `visudo -cf`, `ansible-config dump/list`, `ansible-inventory --graph`, chaves de `settings.json` das extensões, pull policy `tag`, repasse de variáveis `ANSIBLE_*` ao EE (verificado no código do navigator 26.10.0), nome padrão dos artefatos e do log do navigator.

## Validação do Capítulo 1

- [x] Seções 1.1–1.7 representadas, na ordem; ausência de lab de fim de capítulo registrada.
- [x] Identificadores `intro-devenv` e `intro-configure` conferidos; nenhum `lab grade`.
- [x] Quiz 1.2 sem respostas reproduzidas; guided exercises sem passos nem arquivos de solução.
- [x] Sem senhas do laboratório, IPs da sala de aula, e-mail/nome da marca d'água.
- [x] Exemplos validados com ansible-core 2.16.19, ansible-lint 26.10.1 (perfil *production*), ansible-navigator 26.10.0 e yamllint 1.38.0. **Não executados contra hosts.**
- [x] YAML embutido nos Markdown validado por parser; links relativos e âncoras verificados por script.

## Validação do Capítulo 2

- [x] Seções 2.1–2.10 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `develop-inventory`, `develop-singleplay`, `develop-multiplay`, `develop-troubleshoot` e `develop-review` conferidos; `lab grade` só no 2.9.
- [x] Guided exercises e lab sem passos, arquivos de solução ou conteúdo esperado; exemplos com cenários próprios (NTP, banco), diferentes do serviço web dos exercícios.
- [x] Sem senhas do laboratório, IPs da sala de aula, e-mail/nome da marca d'água. IPs de exemplo apenas de documentação (RFC 5737).
- [x] `cap02-inventario-e-playbooks` validado: yamllint, `ansible-inventory --graph/--host`, `--syntax-check`, `--list-hosts`, `ansible-lint` (perfil *production*) com a collection `ansible.posix` (pacote comunitário `ansible` 9, pois o Galaxy está bloqueado no ambiente da sessão). **Não executado contra hosts.**
- [x] Todos os blocos INI dos Markdown do capítulo testados com `ansible-inventory` (o fragmento incremental do Passo 3 de 2.1 está rotulado como continuação).
- [x] YAML embutido validado por parser; links e âncoras verificados por script.

## Validação do Capítulo 3

- [x] Seções 3.1–3.8 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `variables-vars`, `variables-facts`, `variables-vault` e `variables-review` conferidos; `lab grade` só no 3.7.
- [x] GEs e lab sem passos, valores (variáveis, senhas, rótulos) ou soluções; exemplos com cenário próprio (aplicação de estoque).
- [x] Sem senhas do laboratório, IPs da sala de aula, e-mail/nome da marca d'água; a senha do vault do exemplo é fictícia, documentada, e o arquivo de senha está no `.gitignore` (padrão `.vault-*` adicionado nesta sessão).
- [x] `cap03-variaveis-fatos-vault` validado: yamllint, `ansible-inventory --host`, `--syntax-check` (3 playbooks, com decifração), `ansible-lint` (perfil *production*); play de `hostvars` executado localmente. **Demais plays não executados contra hosts.**
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

Aguardar o PDF **`AU294_AAP2.6_C04_Controle_Tarefas_p226-291.pdf`**
(Capítulo 4, p. 226–291). Não avançar sem ele.
