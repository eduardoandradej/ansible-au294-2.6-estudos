# Prática oficial — Capítulo 7

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, valores,
> arquivos de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. As credenciais (inclusive senhas de Vault) estão no
> enunciado de cada atividade e **não** devem ser copiadas para este repositório.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 7.2 | Quiz | — (sem comando `lab`) | — | p. 396–399 |
| 7.4 | Guided Exercise | `roles-create` | Não | p. 406–412 |
| 7.6 | Guided Exercise | `roles-external` | Não | p. 420–425 |
| 7.8 | Guided Exercise | `roles-collections` | Não | p. 434–440 |
| 7.9 | Lab | `roles-review` | **Sim** | p. 441–451 |

Identificadores e avaliação verificados no PDF do Capítulo 7. Cada atividade com
`lab` abre o projeto em um **development container** no VS Code.

---

## 7.2 Quiz: Defining Role Structure

| Campo | Valor |
|-------|-------|
| Seção | 7.2 |
| Tipo | Quiz (7 questões de múltipla escolha) |
| Identificador `lab` | Não se aplica |
| Avaliação | Autoavaliação (a solução está no próprio PDF) |
| Referência | PDF p. 396–399 |

**Competência avaliada:** propósito das roles, conteúdo e subdiretórios,
precedência de variáveis, `import_role` × `include_role` e ordem das seções de um
play.

**Domine antes:** [7.1](7.1-definindo-a-estrutura-de-roles.md), Partes C e I.

**Pontos de atenção:**
- Uma questão pede **duas** alternativas: leia o enunciado inteiro.
- Releia a tabela de ordem de execução (`pre_tasks`, `roles`, `tasks`, `post_tasks`, handlers).
- Responda **antes** de abrir a página de solução.

---

## 7.4 Guided Exercise: Creating Roles

| Campo | Valor |
|-------|-------|
| Seção | 7.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `roles-create` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 406–412 |

**Competência praticada:** criar uma role com `ansible-galaxy role init`, enxugar a
estrutura, colocar arquivo estático, template, handler e tasks nos lugares certos,
documentar a role (`meta/main.yml` e `README.md`) e usá-la em um playbook para
configurar um serviço de rede, conferindo o resultado com playbooks de verificação
fornecidos.

**Domine antes:** [7.3](7.3-criando-roles.md).

```bash
lab start roles-create
lab finish roles-create
```

**Pontos de atenção:**
- Remova só os subdiretórios que o enunciado indica como desnecessários.
- `src` de `copy`/`template` em task de role é relativo a `files/` e `templates/` da role.
- No `meta/main.yml`, valores numéricos que o lint espera como texto vão entre aspas.
- Observe no output o prefixo `nome_da_role :` em cada task e no handler.

**Critério de prontidão:** você monta a estrutura da role de memória e explica onde
cada arquivo entra.

---

## 7.6 Guided Exercise: Deploying Roles from External Content Sources

| Campo | Valor |
|-------|-------|
| Seção | 7.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `roles-external` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 420–425 |

**Competência praticada:** configurar o `roles_path` do projeto, escrever um
`roles/requirements.yml` para uma role empacotada em arquivo, instalar com
`ansible-galaxy`, consultar o `README.md` da role para achar a variável de
customização e usá-la em um playbook que também lê um arquivo protegido por Vault.

**Domine antes:** [7.5](7.5-implantando-roles-de-fontes-externas.md) e
[3.5 — Ansible Vault](../03-variaveis-e-vault/3.5-protegendo-dados-com-ansible-vault.md).

```bash
lab start roles-external
lab finish roles-external
```

**Pontos de atenção:**
- Confira com `ansible-galaxy role list` antes e depois da instalação.
- O diretório `roles/` do projeto não é um local de busca padrão: o `ansible.cfg` precisa incluí-lo.
- A senha do Vault está no enunciado; não a anote neste repositório.

**Critério de prontidão:** você instala uma role a partir de um requirements e acha
as variáveis dela no README sem ajuda.

---

## 7.8 Guided Exercise: Obtaining Roles and Modules from Ansible Content Collections

| Campo | Valor |
|-------|-------|
| Seção | 7.8 |
| Tipo | Guided Exercise |
| Identificador `lab` | `roles-collections` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 434–440 |

**Competência praticada:** configurar o `collections_path`, instalar uma collection
a partir de um arquivo, explorar a documentação no modo interativo do
`ansible-navigator`, chamar uma role da collection pelo FQRN e passar variáveis por
`group_vars`, verificando o resultado.

**Domine antes:** [7.7](7.7-roles-e-modulos-de-collections.md).

```bash
lab start roles-collections
lab finish roles-collections
```

**Pontos de atenção:**
- No modo interativo, repare que a mesma collection pode aparecer duas vezes (projeto × imagem) e qual está *shadowed*.
- Procure as variáveis da role na documentação antes de escrever o `group_vars`.
- Rode `--syntax-check` antes de executar; avisos de depreciação podem aparecer.

**Critério de prontidão:** você explica por que a versão do projeto prevalece sobre
a da imagem.

---

## 7.9 Lab: Reusing Code with Ansible Roles and Content Collections

| Campo | Valor |
|-------|-------|
| Seção | 7.9 |
| Tipo | Lab (fim de capítulo) |
| Identificador `lab` | `roles-review` |
| Avaliação | **`lab grade roles-review`** |
| Referência | PDF p. 441–451 |

**Competência avaliada:** combinar tudo do capítulo: instalar uma collection de
arquivo e uma role de repositório Git, criar uma role nova com dependência,
posicionar tasks, template e variáveis de grupo, escrever o playbook e resolver um
problema de execução usando uma role de sistema da collection.

**Domine antes:** todas as lições do capítulo e
[4.3 — handlers](../04-controle-de-tarefas/4.3-implementando-handlers.md).

```bash
lab start roles-review
# ... resolva no VS Code, dentro do development container ...
lab grade roles-review
lab finish roles-review
```

**Pontos de atenção (sem solução):**
- A dependência em `meta/main.yml` usa os mesmos dados de origem do requirements (nome, `src`, `scm`).
- Arquivos fornecidos no projeto precisam ir para o local exato da hierarquia da role ou de `group_vars`; confira os nomes pedidos.
- Leia o enunciado sobre handlers: há uma exigência de comportamento do play.
- A primeira execução pode falhar de propósito; entenda a causa antes de mudar o playbook.
- Se o `lab grade` reportar FAIL, leia o critério, corrija e rode de novo; só então compare com `solutions`.

**Critério de prontidão:** `lab grade` com todos os critérios PASS **sem** consultar
a solução. Anote o tempo no diário.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 7.7 Collections](7.7-roles-e-modulos-de-collections.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
