# Roteiro de revisão para o EX294

Plano autoral. Será refinado quando os objetivos públicos forem verificados e
quando o Capítulo 9 (Comprehensive Review) for recebido.

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
- [ ] ⏳ Demais itens com os próximos capítulos.

---
[← Matriz de competências](matriz-de-competencias.md) | [Índice geral](../README.md)
