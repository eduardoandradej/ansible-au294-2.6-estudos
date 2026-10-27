# Prática oficial — Capítulo 8

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, valores,
> arquivos de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais estão no enunciado de cada atividade
> e **não** devem ser copiadas para este repositório.

> 🟡 **Capítulo parcial:** esta página cobre a parte A (PDF 08A, seções 8.1–8.6). As
> atividades 8.8, 8.10, 8.12 e o lab 8.13 entram com o PDF 08B.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 8.2 | Guided Exercise | `system-roles` | Não | p. 463–470 |
| 8.4 | Guided Exercise | `system-software` | Não | p. 484–492 |
| 8.6 | Guided Exercise | `system-user` | Não | p. 500–508 |
| 8.8–8.13 | ⏳ Aguardando PDF 08B | — | — | p. 509–569 |

Identificadores verificados no PDF 08A. Cada atividade abre o projeto em um
**development container** no VS Code.

---

## 8.2 Guided Exercise: Using System Roles

| Campo | Valor |
|-------|-------|
| Seção | 8.2 |
| Tipo | Guided Exercise |
| Identificador `lab` | `system-roles` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 463–470 |

**Competência praticada:** instalar a collection de system roles, usar uma delas
junto com tasks próprias para configurar sincronização de horário e fuso horário,
achar as variáveis na documentação da role e definir valores diferentes por grupo
de hosts (data centers distintos).

**Domine antes:** [8.1](8.1-usando-system-roles.md) e
[7.7](../07-roles-e-collections/7.7-roles-e-modulos-de-collections.md).

```bash
lab start system-roles
lab finish system-roles
```

**Pontos de atenção:**
- Leia o README da role e localize as variáveis pedidas antes de escrever o playbook.
- Valores por grupo vão em `group_vars/<grupo>/`; confira os nomes dos grupos no inventário.
- Lembre a ordem `roles` → `tasks` → handlers ao combinar a role com tasks.
- Verifique o resultado em um host de cada grupo.

**Critério de prontidão:** você explica de onde veio cada valor aplicado em cada host.

---

## 8.4 Guided Exercise: Automating Software and Subscription Tasks

| Campo | Valor |
|-------|-------|
| Seção | 8.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `system-software` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 484–492 |

**Competência praticada:** configurar um repositório e importar sua chave GPG,
instalar um pacote dele e observar o comportamento de `ansible_facts['packages']`
antes e depois de recoletar os facts de pacotes.

**Domine antes:** [8.3](8.3-automatizando-software-e-assinaturas.md).

```bash
lab start system-software
lab finish system-software
```

**Pontos de atenção:**
- Ordem: chave GPG e repositório antes da instalação.
- Compare o que o fact mostra antes e depois de rodar `package_facts` novamente.
- Ao reexecutar, observe quais tasks ficam `ok` e quais mudam.

**Critério de prontidão:** você explica por que o fact de pacotes pode estar
desatualizado e como resolver.

---

## 8.6 Guided Exercise: Automating User Management and Authentication Tasks

| Campo | Valor |
|-------|-------|
| Seção | 8.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `system-user` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 500–508 |

**Competência praticada:** criar grupo e usuários a partir de um arquivo de
variáveis, autorizar chaves SSH, conceder sudo a um grupo, restringir o login direto
do root e reiniciar o `sshd` por handler, verificando o acesso por SSH.

**Domine antes:** [8.5](8.5-automatizando-usuarios-e-autenticacao.md) e
[4.3 — handlers](../04-controle-de-tarefas/4.3-implementando-handlers.md).

```bash
lab start system-user
lab finish system-user
```

**Pontos de atenção:**
- Revise o arquivo de variáveis fornecido: a estrutura dos dados define como escrever o loop.
- `groups` com `append: true` para não perder grupos existentes.
- Use `validate` ao mexer no sudoers; `%` indica grupo.
- A mudança no `sshd_config` só vale depois do reinício do serviço.

**Critério de prontidão:** você prevê quais logins funcionam e quais falham depois do
playbook.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 8.5 Usuários e autenticação](8.5-automatizando-usuarios-e-autenticacao.md) | [Índice do capítulo](README.md) | [Próximo: ⏳ 8.7 (PDF 08B)](README.md)
