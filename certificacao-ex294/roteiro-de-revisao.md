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
- [ ] ⏳ Demais itens com os próximos capítulos.

---
[← Matriz de competências](matriz-de-competencias.md) | [Índice geral](../README.md)
