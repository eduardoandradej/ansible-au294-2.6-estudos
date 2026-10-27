# Prática oficial — Capítulo 2

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, arquivos
> de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais estão no enunciado de cada atividade
> e **não** devem ser copiadas para este repositório.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 2.2 | Guided Exercise | `develop-inventory` | Não | p. 70–75 |
| 2.4 | Guided Exercise | `develop-singleplay` | Não | p. 86–93 |
| 2.6 | Guided Exercise | `develop-multiplay` | Não | p. 103–109 |
| 2.8 | Guided Exercise | `develop-troubleshoot` | Não | p. 119–126 |
| 2.9 | Lab | `develop-review` | **Sim** | p. 127–139 |

Identificadores e avaliação verificados no PDF do Capítulo 2. Todas as atividades
abrem a pasta do projeto em um **development container** no VS Code, como no
Capítulo 1, e terminam fechando a conexão remota antes do `lab finish`.

---

## 2.2 Guided Exercise: Building an Ansible Inventory

| Campo | Valor |
|-------|-------|
| Seção | 2.2 |
| Tipo | Guided Exercise |
| Identificador `lab` | `develop-inventory` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 70–75 |

**Competência praticada:** transformar uma tabela de servidores (função, cidade,
ambiente) em um inventário INI com vários grupos, um range e um grupo pai
(`:children`), e conferir o resultado com as variações de `ansible-navigator inventory`.

**Domine antes:** [2.1](2.1-construindo-um-inventario.md): grupos, `:children`,
ranges, `all`/`ungrouped`, `--list`/`--graph`/TUI.

```bash
lab start develop-inventory
lab finish develop-inventory
```

**Pontos de atenção:**
- Monte o inventário **a partir da tabela**, antes de olhar o conteúdo esperado. Depois compare.
- O exercício pede `-i` explicitamente em todos os comandos de consulta: repare por quê.
- Confira o grupo pai com `--graph <grupo>`: os filhos aparecem com `@`.
- Verifique se `ungrouped` está vazio e explique o motivo.
- Na TUI, lembre a regra dos dois-pontos para linhas acima de 9.

**Critério de prontidão:** você escreve um inventário equivalente para outra tabela
de servidores em poucos minutos e explica cada grupo.

---

## 2.4 Guided Exercise: Developing Playbooks

| Campo | Valor |
|-------|-------|
| Seção | 2.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `develop-singleplay` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 86–93 |

**Competência praticada:** escrever um playbook de um play que deixa um serviço web
funcionando (pacote, conteúdo, serviço, firewall), validar a sintaxe, executar,
rever um artefato com `replay`, provar a idempotência com uma segunda execução e
testar o serviço de fora.

**Domine antes:** [2.3](2.3-desenvolvendo-playbooks.md): estrutura do play,
FQCN, `--syntax-check`, artefatos e `replay`.

```bash
lab start develop-singleplay
lab finish develop-singleplay
```

**Pontos de atenção:**
- Leia primeiro o `inventory`, o `ansible.cfg` e o `ansible-navigator.yml` do projeto: o `ansible.cfg` liga a escalada de privilégio **globalmente**. Compare com a abordagem "por play" de 2.5.
- Conte os espaços: play (2), lista de tasks (4), módulo (6), parâmetros (8).
- Um dos módulos não é `ansible.builtin`: identifique de qual collection ele vem e por que está disponível.
- Avisos de *deprecation* na verificação de sintaxe podem ser ignorados, segundo o curso.
- Compare as duas execuções: o que mudou no `PLAY RECAP` e por quê.

**Critério de prontidão:** você reescreve o play de memória e explica cada parâmetro.

---

## 2.6 Guided Exercise: Developing Playbooks with Multiple Plays

| Campo | Valor |
|-------|-------|
| Seção | 2.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `develop-multiplay` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 103–109 |

**Competência praticada:** um playbook com dois plays: o primeiro configura um host
com escalada de privilégio (pacotes em lista, conteúdo, firewall, serviço); o
segundo, em outro host e **sem** escalada, testa o primeiro pela rede e mostra o
resultado com `debug`.

**Domine antes:** [2.5](2.5-playbooks-com-multiplos-plays.md): plays sequenciais,
`become` por play, parâmetros em lista, módulos web.

```bash
lab start develop-multiplay
lab finish develop-multiplay
```

**Pontos de atenção:**
- O segundo play começa na **mesma coluna** do primeiro `- name:` do arquivo.
- Observe por que o segundo play não precisa de `become`.
- A task de teste usa `register` e `debug` (prévia do Capítulo 3): veja o que a variável registrada contém.
- No `PLAY RECAP`, compare `changed` dos dois hosts e explique a diferença.

**Critério de prontidão:** você explica a ordem de execução dos plays e o que
aconteceria se o host do primeiro play estivesse inalcançável.

---

## 2.8 Guided Exercise: Troubleshooting Playbooks and Managed Hosts

| Campo | Valor |
|-------|-------|
| Seção | 2.8 |
| Tipo | Guided Exercise |
| Identificador `lab` | `develop-troubleshoot` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 119–126 |

**Competência praticada:** corrigir os problemas que o `ansible-lint` aponta em um
playbook no VS Code, ativar o log em texto do Ansible, usar o log para achar a causa
de uma falha de task e diagnosticar uma falha de conexão com verbosidade alta e
revisão do inventário.

**Domine antes:** [2.7](2.7-troubleshooting-de-playbooks-e-hosts.md): regras do
lint, `log_path`, `UNREACHABLE` × `FAILED`, `-vvvv`.

```bash
lab start develop-troubleshoot
lab finish develop-troubleshoot
```

**Pontos de atenção:**
- Espere o development container baixar o EE e o lint rodar antes de concluir que "não há erros".
- Corrigir um erro de lint pode **revelar** outros: o arquivo só é analisado por inteiro depois que a estrutura fica válida.
- Corrija as causas; não desligue regras.
- Quando o playbook falhar, abra o arquivo de log antes de mexer no código.
- Em um `UNREACHABLE`, leia o **nome do host** que aparece na mensagem com atenção, letra por letra.
- Antes de culpar o playbook, prove a conexão com um teste simples (`ansible.builtin.ping`).

**Critério de prontidão:** diante de uma falha, você diz em qual camada ela está
(escrita, conexão, escalada, task) antes de abrir o playbook.

---

## 2.9 Lab: Developing Automation Content

| Campo | Valor |
|-------|-------|
| Seção | 2.9 |
| Tipo | Lab (fim de capítulo) |
| Identificador `lab` | `develop-review` |
| Avaliação | **`lab grade develop-review`** |
| Referência | PDF p. 127–139 |

**Competência avaliada:** integrar o capítulo inteiro. O `lab start` cria o projeto
com `ansible.cfg`, `ansible-navigator.yml` e devcontainer. Você cria um inventário
com hosts em grupos e fora de grupos, corrige problemas de lint em um playbook
existente, escreve um playbook com dois plays (configuração de um servidor web com
pacotes, firewall, serviço e conteúdo; depois um teste de acesso a partir de outro
host, sem escalada) e executa os playbooks na ordem pedida.

**Domine antes:** todas as lições do capítulo, especialmente
[2.1](2.1-construindo-um-inventario.md), [2.5](2.5-playbooks-com-multiplos-plays.md)
e [2.7](2.7-troubleshooting-de-playbooks-e-hosts.md).

```bash
lab start develop-review
# ... resolva no VS Code, dentro do development container ...
lab grade develop-review
lab finish develop-review
```

**Pontos de atenção (sem solução):**
- Um dos hosts deve ficar **fora** de qualquer grupo: lembre onde ele precisa ficar no arquivo INI.
- "Não atualizar pacotes já instalados" corresponde a um valor específico de `state`.
- Os nomes das tasks pedidos no enunciado devem ser usados **exatamente**: o `lab grade` pode conferi-los.
- Respeite a ordem de execução dos playbooks pedida no enunciado.
- O segundo play testa um host do grupo web **a partir de outro host**: pense em qual módulo faz uma requisição HTTP e verifica o código de status.
- Se o `lab grade` reportar FAIL, leia o critério, corrija e rode `lab grade` de novo. Só então compare com a pasta `solutions`.

**Critério de prontidão:** `lab grade` com todos os critérios PASS **sem** consultar
a solução. Anote o tempo gasto no diário.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 2.7 Troubleshooting](2.7-troubleshooting-de-playbooks-e-hosts.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
