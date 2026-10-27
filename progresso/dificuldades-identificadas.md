# Dificuldades identificadas

Registro de conceitos ou procedimentos que exigiram mais de uma tentativa. Revise
esta lista antes do Capítulo 9 e da preparação para o EX294.

| Data | Capítulo/seção | Dificuldade | Causa raiz (conceito) | Material de reforço | Resolvida? |
|------|----------------|-------------|-----------------------|---------------------|-----------|
| | | | | | |

## Dicas para preencher

- Descreva o **sintoma** ("`ping` deu `UNREACHABLE`") e a **causa conceitual** ("`remote_user` ausente; no EE o padrão era `root`").
- Aponte o link da lição que esclarece o assunto.
- Marque como resolvida só depois de acertar o mesmo tipo de problema em outra atividade.

## Pontos de atenção previstos pelo autor (Capítulo 1)

Não são dificuldades registradas pelo aluno, mas armadilhas comuns para observar:

- Confundir development container com execution environment.
- Ler errado a coluna `Default` do `ansible-navigator config`.
- Esquecer que só **um** `ansible.cfg` é usado (o de maior precedência).
- Indentação do `ansible-navigator.yml`.

## Pontos de atenção previstos pelo autor (Capítulo 2)

- Zeros à esquerda em ranges e nomes de host consultados com `--host`.
- Comentários: `#` no inventário, `;` inline no `ansible.cfg` (comportamentos opostos).
- Host solto listado depois de uma seção `[grupo:vars]`.
- Prioridade do usuário de conexão: `ansible_user` > `remote_user` do play > `ansible.cfg`.
- Indentação de um segundo play (mesma coluna do primeiro).

## Pontos de atenção previstos pelo autor (Capítulo 3)

- Aspas quando o valor começa com `{{`.
- `lista[0]['chave']` com aspas na chave.
- Precedência: variável de play mascarando `group_vars` durante testes.
- Recoletar facts depois de publicar um `.fact`.
- Vault + navigator: `-m stdout --pae false`; arquivo de senha fora do Git.

## Pontos de atenção previstos pelo autor (Capítulo 4)

- `loop` e `when` no nível da task.
- Resultados de loop em `['results']`.
- Handler só com `changed`; nome idêntico no `notify`; ordem da seção `handlers`.
- `debug` no `rescue` precisa de `changed_when: true` para notificar.

## Pontos de atenção previstos pelo autor (Capítulo 5)

- Barra final em `src` do `copy`; `remote_src` para origem no host.
- `lineinfile` com `regexp` para não duplicar.
- Marcadores distintos em `blockinfile`.
- `ansible_managed` com o comentário do formato; `{% %}` só em templates.

## Pontos de atenção previstos pelo autor (Capítulo 6)

- `when` em import (cada task) × include (só o include).
- `import_playbook` só no nível superior; caminhos relativos ao arquivo que importa.
- Aspas em patterns com `!`, `*`, `&`; `--list-hosts` antes de executar.

## Pontos de atenção previstos pelo autor (Capítulo 7)

- Precedência: parâmetro em `roles:` > `vars/main.yml` > `vars` do play > `defaults/main.yml`.
- Seção `roles` roda antes de `tasks`; ordem com `pre_tasks`/`post_tasks` e handlers.
- `-p roles`/`-p collections` (ou `roles_path`/`collections_path`) para o EE enxergar o conteúdo.
- Roles de collection com FQRN via `include_role`/`import_role`.

## Pontos de atenção previstos pelo autor (Capítulo 8, parte A)

- Role de SELinux não reinicia: `selinux_reboot_required` + `block`/`rescue`.
- `ansible_facts['packages']` não se atualiza sozinho após instalar.
- `groups` sem `append` substitui grupos; `%` no sudoers indica grupo; `validate` com `visudo`.

---
[Início](../README.md) | [Diário de laboratórios](diario-de-laboratorios.md)
