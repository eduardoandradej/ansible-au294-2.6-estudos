# Prática oficial — Capítulo 8

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, valores,
> arquivos de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais estão no enunciado de cada atividade
> e **não** devem ser copiadas para este repositório.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 8.2 | Guided Exercise | `system-roles` | Não | p. 463–470 |
| 8.4 | Guided Exercise | `system-software` | Não | p. 484–492 |
| 8.6 | Guided Exercise | `system-user` | Não | p. 500–508 |
| 8.8 | Guided Exercise | `system-process` | Não | p. 516–524 |
| 8.10 | Guided Exercise | `system-storage` | Não | p. 534–540 |
| 8.12 | Guided Exercise | `system-network` | Não | p. 549–555 |
| 8.13 | Lab | `system-review` | **Sim** | p. 556–568 |

Identificadores verificados nos PDFs 08A e 08B. Cada atividade abre o projeto em um
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

## 8.8 Guided Exercise: Automating the Boot Process and Scheduled Processes

| Campo | Valor |
|-------|-------|
| Seção | 8.8 |
| Tipo | Guided Exercise |
| Identificador `lab` | `system-process` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 516–524 |

**Competência praticada:** criar e remover um job cron em arquivo de sistema, agendar
um comando único com `at`, mudar o alvo de boot padrão e reiniciar os managed hosts
com o módulo próprio.

**Domine antes:** [8.7](8.7-automatizando-boot-e-agendamentos.md).

```bash
lab start system-process
lab finish system-process
```

**Pontos de atenção:**
- Para remover um job cron, a task precisa identificar o mesmo job (`name`, `cron_file`, `user`) com `state: absent`.
- Confira no host o arquivo em `/etc/cron.d/` e a fila do `at`.
- O reboot faz o playbook esperar o host voltar: não interrompa.

**Critério de prontidão:** você cria e remove o mesmo job sem duplicações.

---

## 8.10 Guided Exercise: Automating Storage Tasks

| Campo | Valor |
|-------|-------|
| Seção | 8.10 |
| Tipo | Guided Exercise |
| Identificador `lab` | `system-storage` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 534–540 |

**Competência praticada:** usar a role de armazenamento para criar volume group,
volumes lógicos com file systems e montagens persistentes, e conferir o resultado
com um playbook de verificação fornecido.

**Domine antes:** [8.9](8.9-automatizando-armazenamento.md).

```bash
lab start system-storage
lab finish system-storage
```

**Pontos de atenção:**
- Use os nomes, tamanhos e pontos de montagem exatos do enunciado; unidades em minúsculas.
- `disks` aceita só dispositivos sem partição: confira qual é o disco certo.
- Reexecute: a role deve ficar sem mudanças.

**Critério de prontidão:** você escreve o `storage_pools` sem consultar a lição.

---

## 8.12 Guided Exercise: Automating Network Configuration Tasks

| Campo | Valor |
|-------|-------|
| Seção | 8.12 |
| Tipo | Guided Exercise |
| Identificador `lab` | `system-network` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 549–555 |

**Competência praticada:** consultar a documentação da role de rede no
`ansible-navigator`, definir as conexões em `group_vars` e aplicar a role para
configurar uma interface, confirmando o endereço resultante.

**Domine antes:** [8.11](8.11-automatizando-rede.md).

```bash
lab start system-network
lab finish system-network
```

**Pontos de atenção:**
- Identifique a interface correta antes (facts ou playbook fornecido); não mexa na interface de gerenciamento.
- `network_provider: nm` e `state: up` para ativar na hora.
- Use o endereço do enunciado; não o copie para este repositório.

**Critério de prontidão:** você explica cada chave da conexão que escreveu.

---

## 8.13 Lab: Automating Linux Administration Tasks

| Campo | Valor |
|-------|-------|
| Seção | 8.13 |
| Tipo | Lab (fim de capítulo) |
| Identificador `lab` | `system-review` |
| Avaliação | **`lab grade system-review`** |
| Referência | PDF p. 556–568 |

**Competência avaliada:** combinar o capítulo em vários playbooks: repositório com
chave GPG e instalação de pacote, grupo e usuários, volumes lógicos com a role de
armazenamento, job cron em arquivo de sistema e configuração de interface com a role
de rede, com variáveis de role em `group_vars`.

**Domine antes:** todas as lições do capítulo.

```bash
lab start system-review
# ... resolva no VS Code, dentro do development container ...
lab grade system-review
lab finish system-review
```

**Pontos de atenção (sem solução):**
- Nomes de arquivos de playbook e de variáveis são avaliados: siga o enunciado exatamente.
- Use os playbooks auxiliares fornecidos para descobrir o disco e a interface certos antes de escrever as variáveis.
- Expressões de horário do cron (intervalos, passos, dias da semana) merecem atenção campo a campo.
- Execute cada playbook e confira o efeito no host antes do `lab grade`.
- Se o `lab grade` reportar FAIL, leia o critério, corrija e rode de novo; só então compare com `solutions`.

**Critério de prontidão:** `lab grade` com todos os critérios PASS **sem** consultar
a solução. Anote o tempo no diário.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 8.11 Rede](8.11-automatizando-rede.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
