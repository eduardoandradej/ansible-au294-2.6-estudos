# Prática oficial — Capítulo 9

> Ponte para os labs de revisão geral. **Não** reproduz especificações, valores,
> credenciais, arquivos de solução nem respostas. Execute tudo no ambiente oficial da
> Red Hat, no `workstation`, como `student`. Usuários, senhas, endereços e URLs estão
> no enunciado de cada lab e **não** devem ser copiados para este repositório.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | Tempo indicado | PDF |
|-------|------|---------------------|-------------|----------------|-----|
| 9.2 | Lab | `comprehensive-review1` | **Sim** | 25 min | p. 574–586 |
| 9.3 | Lab | `comprehensive-review2` | **Sim** | 25 min | p. 587–594 |
| 9.4 | Lab | `comprehensive-review3` | **Sim** | 40 min | p. 595–605 |
| 9.5 | Lab | `comprehensive-review4` | **Sim** | 25 min | p. 606–614 |

Identificadores, avaliação e tempos verificados no PDF do Capítulo 9. Os labs de
revisão trazem **especificações** (o que entregar), não passos: é o formato mais
próximo de um exame prático. O curso orienta: se precisar de mais tempo que o
indicado, volte ao conteúdo e pratique mais.

## Cobertura por lab

| Lab | Capítulos exercitados |
|-----|-----------------------|
| 9.2 | 1 (ambiente, extensões, development container, `ansible-navigator.yml`, Git), 2 (inventário, playbook, troubleshooting), 3 (variáveis, facts), 4 (condicionais) |
| 9.3 | 2, 4 (handlers, `block`/`rescue`, `force_handlers`), 5 (templates, cópia de arquivos), 6 (`import_playbook`) |
| 9.4 | 3 (Vault), 5 (sudoers), 8 (role de armazenamento, usuários e sudo, role de rede, cron) |
| 9.5 | 7 (converter playbook em role, `defaults`, handlers, `meta`, README, limpeza da estrutura) |

---

## 9.2 Lab: Deploying Ansible

| Campo | Valor |
|-------|-------|
| Seção | 9.2 |
| Tipo | Lab de revisão geral |
| Identificador `lab` | `comprehensive-review1` |
| Avaliação | **`lab grade comprehensive-review1`** |
| Tempo indicado | 25 minutos |
| Referência | PDF p. 574–586 |

**Competência avaliada:** preparar do zero um ambiente de desenvolvimento
consistente (extensões do VS Code, development container, configuração do
`ansible-navigator`, clone de repositório Git) e, nele, criar, corrigir e evoluir
playbooks orientados por variáveis e condições, mantendo o repositório remoto em dia.

**Revise antes:** [1.3](../01-introducao-ansible/1.3-configurando-o-ambiente-de-desenvolvimento.md),
[1.5](../01-introducao-ansible/1.5-configurando-ajustes-do-ansible.md),
[2.1](../02-desenvolvendo-automacao/2.1-construindo-um-inventario.md),
[2.7](../02-desenvolvendo-automacao/2.7-troubleshooting-de-playbooks-e-hosts.md),
[3.3](../03-variaveis-e-vault/3.3-coletando-informacoes-com-facts.md),
[4.1](../04-controle-de-tarefas/4.1-loops-e-tarefas-condicionais.md).

```bash
lab start comprehensive-review1
# ... resolva conforme as especificações ...
lab grade comprehensive-review1
lab finish comprehensive-review1
```

**Pontos de atenção (sem solução):**
- Configure as extensões e o development container exatamente com os valores das tabelas do enunciado.
- O inventário precisa ser o padrão do projeto: lembre onde isso se configura.
- No playbook com erros, leia a mensagem e corrija por camada (YAML, nomes de módulo, variáveis).
- A condição sobre swap depende de um fact: descubra o nome e a unidade antes de escrever o `when`.
- O último critério é o Git: commit **e** push.

---

## 9.3 Lab: Creating Playbooks

| Campo | Valor |
|-------|-------|
| Seção | 9.3 |
| Tipo | Lab de revisão geral |
| Identificador `lab` | `comprehensive-review2` |
| Avaliação | **`lab grade comprehensive-review2`** |
| Tempo indicado | 25 minutos |
| Referência | PDF p. 587–594 |

**Competência avaliada:** escrever um playbook idempotente que configura servidores
web com template, cópia de arquivo e handler; um playbook de verificação com
`block`/`rescue`; e um playbook principal que importa os dois.

**Revise antes:** [4.3](../04-controle-de-tarefas/4.3-implementando-handlers.md),
[4.5](../04-controle-de-tarefas/4.5-tratando-falhas-de-tarefas.md),
[5.1](../05-deploy-de-arquivos/5.1-automatizando-gerenciamento-de-arquivos.md),
[5.3](../05-deploy-de-arquivos/5.3-templates-jinja2-e-filtros.md),
[6.1](../06-automacao-em-escala/6.1-incluindo-e-importando-arquivos.md).

```bash
lab start comprehensive-review2
lab grade comprehensive-review2
lab finish comprehensive-review2
```

**Pontos de atenção (sem solução):**
- Nomes de playbooks, blocos e tasks pedidos pelo enunciado fazem parte da avaliação.
- Dono, grupo e modo dos arquivos implantados são exigidos.
- O destino da cópia usa um fact: confira o diretório de destino antes.
- O play de verificação roda no próprio execution environment: pense em quais keywords do play isso afeta.

---

## 9.4 Lab: Managing Linux Hosts and Using System Roles

| Campo | Valor |
|-------|-------|
| Seção | 9.4 |
| Tipo | Lab de revisão geral |
| Identificador `lab` | `comprehensive-review3` |
| Avaliação | **`lab grade comprehensive-review3`** |
| Tempo indicado | 40 minutos |
| Referência | PDF p. 595–605 |

**Competência avaliada:** automatizar armazenamento com a role `storage`, usuário
com senha vinda de arquivo do Vault e sudo validado, interface de rede com a role
`network` e um job cron de manutenção, verificando cada resultado e a idempotência.

**Revise antes:** [3.5](../03-variaveis-e-vault/3.5-protegendo-dados-com-ansible-vault.md),
[8.5](../08-administracao-linux/8.5-automatizando-usuarios-e-autenticacao.md),
[8.7](../08-administracao-linux/8.7-automatizando-boot-e-agendamentos.md),
[8.9](../08-administracao-linux/8.9-automatizando-armazenamento.md),
[8.11](../08-administracao-linux/8.11-automatizando-rede.md).

```bash
lab start comprehensive-review3
lab grade comprehensive-review3
lab finish comprehensive-review3
```

**Pontos de atenção (sem solução):**
- É o lab mais longo: planeje um playbook por especificação e rode cada um antes de seguir.
- Tamanhos da role `storage` em minúsculas; confira os pontos de montagem.
- A senha vem de uma variável já em hash, dentro de um arquivo do Vault: lembre como carregar o arquivo e como informar a senha do Vault na execução.
- Sudo: dono, grupo, modo e `validate`.
- Use o playbook auxiliar para achar a interface pelo MAC antes de escrever as variáveis de rede.
- Horário do cron: confira cada campo.

---

## 9.5 Lab: Creating Roles

| Campo | Valor |
|-------|-------|
| Seção | 9.5 |
| Tipo | Lab de revisão geral |
| Identificador `lab` | `comprehensive-review4` |
| Avaliação | **`lab grade comprehensive-review4`** |
| Tempo indicado | 25 minutos |
| Referência | PDF p. 606–614 |

**Competência avaliada:** converter um playbook monolítico em uma role reutilizável,
distribuindo tasks, variáveis e handlers nos arquivos corretos, documentando
`meta/main.yml` e `README.md`, removendo o que não é usado e validando com um
playbook que aplica a role.

**Revise antes:** [7.1](../07-roles-e-collections/7.1-definindo-a-estrutura-de-roles.md),
[7.3](../07-roles-e-collections/7.3-criando-roles.md).

```bash
lab start comprehensive-review4
lab grade comprehensive-review4
lab finish comprehensive-review4
```

**Pontos de atenção (sem solução):**
- Leia o playbook original inteiro e classifique cada parte: task, handler ou variável.
- O enunciado indica em qual arquivo as variáveis devem ser declaradas (precedência importa).
- Metadados e README seguem textos dados no enunciado; valores numéricos de versão vão entre aspas.
- Depois de remover diretórios não usados, execute de novo para garantir que nada necessário foi apagado.

---

## Critério de prontidão do curso

Todos os quatro labs com `lab grade` PASS, **sem** consultar as soluções, **dentro
do tempo indicado**. Registre os tempos no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md); se algum
estourar, use a tabela de cobertura para voltar às lições certas e repita.

---
[← 9.1 Mapa de objetivos](9.1-mapa-de-objetivos.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
