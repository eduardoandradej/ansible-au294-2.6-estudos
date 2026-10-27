# Roteiro de revisão para o EX294

Plano autoral. Será refinado quando os objetivos públicos forem verificados. O
Capítulo 9 (Comprehensive Review) já está integrado: veja a etapa final abaixo.

## Princípios

- O exame é **prático**: treine escrevendo, não lendo.
- Sem internet: domine `ansible-navigator doc` para consultar módulos.
- Leia o `PLAY RECAP` sempre; reexecute para provar a idempotência.
- Comece todo projeto pelo `ansible.cfg` e pela conectividade (`ansible.builtin.ping`).

## Ciclo por capítulo concluído

| Etapa | Atividade |
|-------|-----------|
| 1 | Refazer o guided exercise **sem** roteiro |
| 2 | Responder a `REVISAO.md` sem consulta |
| 3 | Reescrever de memória os arquivos do capítulo (no Cap. 1: `ansible.cfg` e `ansible-navigator.yml`) |
| 4 | Registrar erros em [dificuldades-identificadas.md](../progresso/dificuldades-identificadas.md) |

## Checklist de prontidão (cresce a cada capítulo)

- [ ] Monto um projeto do zero (`ansible.cfg`, `ansible-navigator.yml`, inventário) em menos de 5 minutos.
- [ ] Explico de onde vem cada valor efetivo com `ansible-navigator config`.
- [ ] Preparo um managed host para automação (usuário, chave SSH, `sudoers.d`).
- [ ] Escrevo um inventário com grupos, `:children` e ranges a partir de uma tabela, sem erros de parse.
- [ ] Escrevo um playbook de dois plays com `become` e `remote_user` diferentes, de memória, e ele passa no `ansible-lint`.
- [ ] Diante de uma falha, identifico a camada (escrita, conexão, escalada, task) em menos de 2 minutos.
- [ ] Uso `ansible-navigator doc <módulo> -s` para montar uma task sem consultar a internet.
- [ ] Explico de onde vem o valor de uma variável em um host, percorrendo a precedência.
- [ ] Crio, vejo, edito e troco a senha de um arquivo do vault sem consultar a ajuda; executo com prompt, arquivo e `ansible.cfg`.
- [ ] Publico um fato customizado e o uso na mesma execução.
- [ ] Escrevo de memória uma task com `loop` sobre lista de dicionários e `when` com fact.
- [ ] Uso handlers com `notify`/`flush_handlers` e explico quando cada um roda.
- [ ] Escrevo `block`/`rescue`/`always` com `changed_when`/`failed_when` sem consulta.
- [ ] Escolho o módulo de arquivo certo para cada operação e aplico dono, modo e `setype`.
- [ ] Escrevo um template com facts, `for`, `if` e `default` e o implanto com handler.
- [ ] Reorganizo um playbook longo em arquivos de tasks importados e parametrizados.
- [ ] Escrevo patterns com curinga, `&` e `!` e confiro com `--list-hosts`.
- [ ] Crio uma role com `ansible-galaxy role init`, com `defaults`, template, handler e dependência.
- [ ] Instalo roles e collections por `requirements.yml` no diretório do projeto.
- [ ] Uso uma role de collection pelo FQRN com variáveis em `group_vars`.
- [ ] Aplico uma system role com variáveis em `group_vars` e trato reboot da role de SELinux.
- [ ] Declaro repositório com chave GPG e instalo vários pacotes em uma transação.
- [ ] Crio usuários e grupos, autorizo chaves e configuro sudo com `validate`.
- [ ] Crio e removo jobs cron e `at`; mudo o alvo de boot de forma idempotente.
- [ ] Escrevo `storage_pools` com LVs, XFS, montagem e swap.
- [ ] Escrevo `network_connections` com IP estático e DNS.
- [ ] Marco todo o [mapa de objetivos](../capitulos/09-revisao-geral/9.1-mapa-de-objetivos.md) sem consulta.
- [ ] Concluo os quatro labs `comprehensive-review` com `lab grade` PASS dentro do tempo indicado.
- [ ] Resolvo o [simulado autoral](../capitulos/09-revisao-geral/REVISAO.md) em até 90 minutos.

## Etapa final (após o Capítulo 9)

| Semana | Atividade |
|--------|-----------|
| 1 | Labs `comprehensive-review1` a `4` no tempo indicado; anotar no diário |
| 2 | Refazer os labs de fim de capítulo (2.9, 3.7, 4.7, 5.5, 6.5, 7.9, 8.13) só pela especificação |
| 3 | Simulado autoral; revisar [dificuldades-identificadas.md](../progresso/dificuldades-identificadas.md) |
| 4 | Conferir os objetivos públicos atuais do EX294 e cobrir lacunas |

---
[← Matriz de competências](matriz-de-competencias.md) | [Índice geral](../README.md)
