# Prática oficial — Capítulo 3

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, valores,
> arquivos de solução nem respostas. Execute tudo no ambiente oficial da Red Hat, no
> `workstation`, como `student`. Senhas de vault e credenciais aparecem nos
> enunciados e **não** devem ser copiadas para este repositório.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 3.2 | Guided Exercise | `variables-vars` | Não | p. 156–168 |
| 3.4 | Guided Exercise | `variables-facts` | Não | p. 179–187 |
| 3.6 | Guided Exercise | `variables-vault` | Não | p. 199–208 |
| 3.7 | Lab | `variables-review` | **Sim** | p. 209–224 |

Identificadores e avaliação verificados no PDF do Capítulo 3. Como nos capítulos
anteriores, cada atividade abre o projeto em um **development container** no VS Code.

---

## 3.2 Guided Exercise: Using Variables

| Campo | Valor |
|-------|-------|
| Seção | 3.2 |
| Tipo | Guided Exercise |
| Identificador `lab` | `variables-vars` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 156–168 |

**Competência praticada:** um playbook de vários plays em que nomes de tasks e
parâmetros vêm de variáveis de play; depois, as mesmas variáveis são movidas para
`group_vars`, na forma de **diretório por grupo**, e o playbook é reexecutado.

**Domine antes:** [3.1](3.1-usando-variaveis.md): `vars`, `{{ }}` com aspas,
`group_vars/<grupo>/`, precedência.

```bash
lab start variables-vars
lab finish variables-vars
```

**Pontos de atenção:**
- Variáveis aparecem também **nos nomes** de plays e tasks: veja como a saída fica com os valores substituídos.
- Toda vez que um valor **começa** com `{{`, confira as aspas.
- Ao mover variáveis do playbook para `group_vars`, tire-as do playbook: variáveis de play têm precedência maior e mascarariam o teste.
- Confira os resultados nos hosts (contas, serviços) com comandos simples via SSH, como o exercício sugere.

**Critério de prontidão:** você explica, para cada variável, onde ela está definida
e por que aquele valor venceu.

---

## 3.4 Guided Exercise: Gathering Host Information from Facts

| Campo | Valor |
|-------|-------|
| Seção | 3.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `variables-facts` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 179–187 |

**Competência praticada:** despejar e filtrar facts, observar `ansible_local` vazio,
publicar um fato customizado em `/etc/ansible/facts.d/` com um playbook, criar um
atalho com `set_fact` e usar o fato customizado para decidir o que instalar e
configurar, conferindo o serviço antes e depois.

**Domine antes:** [3.3](3.3-coletando-informacoes-com-facts.md): `ansible_facts`,
`.fact` em INI, recoleta, `set_fact`.

```bash
lab start variables-facts
lab finish variables-facts
```

**Pontos de atenção:**
- Compare `ansible_local` **antes** e **depois** de publicar o `.fact`: a diferença só aparece com nova coleta de facts.
- Leia a estrutura de `ansible_local` e monte o caminho até a chave, nível por nível.
- Observe quanto o `set_fact` encurta as expressões das tasks seguintes.
- Use colchetes, não pontos, nos acessos.

**Critério de prontidão:** dado um `.fact` qualquer, você escreve de primeira a
expressão completa até uma chave.

---

## 3.6 Guided Exercise: Protecting Sensitive Data with Ansible Vault

| Campo | Valor |
|-------|-------|
| Seção | 3.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `variables-vault` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 199–208 |

**Competência praticada:** cifrar arquivos com o Vault (inclusive um arquivo não
YAML, entregue decifrado no host), executar playbooks com senha interativa e com
arquivo de senha, usar vault IDs e configurar o projeto para simplificar o uso das
senhas.

**Domine antes:** [3.5](3.5-protegendo-dados-com-ansible-vault.md): subcomandos,
cabeçalho 1.1 × 1.2, `--ask-vault-pass`, `--vault-id`, `vault_identity_list`,
`decrypt: true`.

```bash
lab start variables-vault
lab finish variables-vault
```

**Pontos de atenção:**
- Leia o **cabeçalho** de cada arquivo cifrado e diga se ele tem rótulo.
- Quando houver prompt, lembre por que o exercício usa `--pae false` (além de evitar o travamento, não grava dados decifrados em artefatos).
- Arquivos de senha devem ter permissões restritas: confira com `ls -l`.
- Depois de configurar o `ansible.cfg`, a execução deve funcionar **sem** opções de vault na linha de comando.

**Critério de prontidão:** você executa o mesmo playbook pelas três formas (prompt,
arquivo, `ansible.cfg`) e explica quando usar cada uma.

---

## 3.7 Lab: Developing Automation Content: Variables

| Campo | Valor |
|-------|-------|
| Seção | 3.7 |
| Tipo | Lab (fim de capítulo) |
| Identificador `lab` | `variables-review` |
| Avaliação | **`lab grade variables-review`** |
| Referência | PDF p. 209–224 |

**Competência avaliada:** integrar o capítulo. Um playbook com um play de
configuração de servidor web guiado por **variáveis de play** (pacotes, caminhos de
origem e destino, diretórios), que usa **facts** para gerar conteúdo, seguido de um
segundo play de teste que carrega uma senha de um arquivo **cifrado com vault ID**
via `vars_files` e registra o resultado de uma requisição autenticada. O projeto
deve ficar configurado para achar a senha do vault sozinho.

**Domine antes:** [3.1](3.1-usando-variaveis.md), [3.3](3.3-coletando-informacoes-com-facts.md)
e [3.5](3.5-protegendo-dados-com-ansible-vault.md).

```bash
lab start variables-review
# ... resolva no VS Code, dentro do development container ...
lab grade variables-review
lab finish variables-review
```

**Pontos de atenção (sem solução):**
- Uma variável pode ser **composta** a partir de outra (`"{{ outra }}/arquivo"`): aspas são obrigatórias.
- Nomes de variáveis, tasks, arquivos, rótulo de vault ID e permissões pedidos no enunciado devem ser usados **exatamente**: o `lab grade` pode conferi-los.
- O conteúdo gerado com facts deve usar o FQDN e o IPv4 principal: lembre os caminhos com colchetes.
- O arquivo de senha do vault deve ter permissões restritas e o `ansible.cfg` deve associá-lo ao **rótulo** certo.
- O teste HTTPS usa um certificado não confiável: procure no `ansible-navigator doc` do módulo o parâmetro que desliga a validação.
- Se o `lab grade` reportar FAIL, leia o critério, corrija e rode de novo; só então compare com `solutions`.

**Critério de prontidão:** `lab grade` com todos os critérios PASS **sem** consultar
a solução. Anote o tempo no diário.

---

## Registro

Ao terminar cada atividade, registre no
[diário de laboratórios](../../progresso/diario-de-laboratorios.md) e marque no
[checklist geral](../../progresso/checklist-geral.md).

---
[← 3.5 Ansible Vault](3.5-protegendo-dados-com-ansible-vault.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
