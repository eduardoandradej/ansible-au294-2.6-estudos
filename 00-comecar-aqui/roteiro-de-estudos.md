# Roteiro de estudos

Estimativas autorais para quem já tem base de RHCSA. Ajuste ao seu ritmo.

| Etapa | Conteúdo | Esforço sugerido | Status do repositório |
|-------|----------|------------------|-----------------------|
| 0 | [Comece aqui](README.md) + [Fundamentos](../01-fundamentos-essenciais/README.md) | 2–3 h | ✅ |
| 1 | [Capítulo 1](../capitulos/01-introducao-ansible/README.md) — introdução, ambiente, configuração | 4–5 h | ✅ |
| 2 | [Capítulo 2](../capitulos/02-desenvolvendo-automacao/README.md) — inventários e playbooks | 6–8 h | ✅ |
| 3 | [Capítulo 3](../capitulos/03-variaveis-e-vault/README.md) — variáveis, facts, Vault | 6–8 h | ✅ |
| 4 | [Capítulo 4](../capitulos/04-controle-de-tarefas/README.md) — loops, condicionais, handlers, falhas | 6–8 h | ✅ |
| 5 | [Capítulo 5](../capitulos/05-deploy-de-arquivos/README.md) — arquivos e templates Jinja2 | 4–6 h | ✅ |
| 6 | [Capítulo 6](../capitulos/06-automacao-em-escala/README.md) — include/import e host patterns | 4–5 h | ✅ |
| 7 | [Capítulo 7](../capitulos/07-roles-e-collections/README.md) — roles e collections | 6–8 h | ✅ |
| 8 | [Capítulo 8](../capitulos/08-administracao-linux/README.md) — administração de RHEL com Ansible | 10–12 h | ✅ |
| 9 | Capítulo 9 — revisão geral | 6–8 h | ⏳ |

## Rotina recomendada por capítulo

1. Leia a lição até a Parte D sem pressa; desenhe o modelo mental de memória.
2. Leia `PRATICA-OFICIAL.md` e faça a atividade no ambiente oficial.
3. Registre erros e aprendizados no [diário](../progresso/diario-de-laboratorios.md).
4. Responda a Parte H das lições e a `REVISAO.md` **sem consulta**.
5. Releia o `RESUMO.md` na véspera do próximo capítulo.
6. A cada três capítulos, refaça um guided exercise anterior sem roteiro.

## Hábitos que ajudam no EX294

- Escreva YAML **à mão**, sem copiar; erros de indentação somem com a repetição.
- Rode `ansible-navigator run --syntax-check` e `ansible-lint` antes de cada execução real.
- Leia sempre o `PLAY RECAP`: `changed` na segunda execução indica algo não idempotente.
- Use `ansible-navigator doc <módulo>` em vez de buscar na internet (no exame não há internet).

---
[← Como usar este repositório](como-usar-este-repositorio.md) | [Índice](README.md) | [Próximo: Ambiente oficial →](ambiente-oficial.md)
