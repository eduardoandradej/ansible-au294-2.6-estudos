# Revisão — Capítulo 7

Questões **autorais**. Elas não reproduzem o quiz oficial, o lab nem perguntas de
exame. Responda por escrito antes de abrir as respostas.

## Parte 1 — Conceitos

1. Cite três vantagens de organizar automação em roles.
2. Qual a função de `meta/main.yml`? E de `galaxy_info` dentro dele?
3. Diferencie `defaults/main.yml` e `vars/main.yml` quanto a uso e precedência.
4. Com `import_role`, as variáveis da role ficam visíveis para tasks anteriores no play? E com `include_role`?
5. Em que ordem rodam `post_tasks`, `roles`, `pre_tasks` e `tasks`?
6. Por que fixar `version` no `roles/requirements.yml`?
7. Qual a fonte de conteúdo recomendada pela Red Hat, e qual exige mais cautela?
8. Por que as collections foram criadas?

## Parte 2 — Escreva o arquivo, a task ou o comando

9. O comando que cria o esqueleto da role `banner_login` dentro de `roles/`.
10. Um play que aplique a role `banner_login` pela seção `roles`, passando `banner_login_texto: Acesso restrito`.
11. Uma task que importe estaticamente a role `banner_login`.
12. O `meta/main.yml` (só a parte de dependências) de uma role que depende de `ferramentas_admin`.
13. Uma entrada de `roles/requirements.yml` para um `.tar` em `file:///srv/roles/banner.tar`, com nome local `banner_login`.
14. O comando que instala as roles de `roles/requirements.yml` em `roles/`.
15. A linha do `ansible.cfg` que faça o Ansible buscar collections no projeto e depois na imagem do EE.
16. Uma task que use a role `redhat.rhel_system_roles.timesync` da forma recomendada para roles de collections.
17. O comando que instala as collections de `collections/requirements.yml` no projeto.

## Parte 3 — Diagnóstico

18. A role foi instalada sem `-p` e o `ansible-navigator` diz que ela não existe. Por quê?
19. Um play define `vars: { banner_login_texto: Olá }`, mas a role continua usando outro texto, definido em `vars/main.yml` dela. Explique e corrija.
20. Uma task escrita acima de `roles:` roda depois da role. Por quê, e como deixar a ordem explícita?
21. `ansible.posix.firewalld` falha com "couldn't resolve module". O que verificar?
22. A mesma role aparece duas vezes em `roles:` com os mesmos parâmetros e só roda uma vez. É erro?
23. Você colocou o token do automation hub no `ansible.cfg` do projeto. Qual o risco e a correção?

---

<details>
<summary>Respostas comentadas</summary>

1. Qualquer três entre: estrutura padrão, reuso entre projetos, customização por variáveis, versionamento independente, colaboração em paralelo, gerenciamento de dependências, publicação em automation hub.
2. Metadados e dependências da role. `galaxy_info` documenta autor, descrição, licença e plataformas; o Ansible o ignora ao processar dependências.
3. `defaults`: valores feitos para serem sobrescritos, precedência mínima. `vars`: constantes e lógica interna, precedência alta (vence play e inventário).
4. Com `import_role`, sim (é estática). Com `include_role`, não: suas variáveis não são expostas ao resto do play.
5. `pre_tasks` → `roles` → `tasks` → `post_tasks` (cada bloco seguido dos handlers notificados nele).
6. Sem versão, instala-se a mais recente; uma mudança incompatível do autor pode quebrar o playbook.
7. Private automation hub é a recomendada; o Ansible Galaxy exige cautela (sem auditoria nem suporte da Red Hat).
8. Para separar o ciclo de vida dos módulos e plug-ins do núcleo, permitindo que cada fornecedor publique no seu ritmo, com nomes únicos por namespace.
9. `ansible-galaxy role init roles/banner_login`
10. Exemplo:
    ```yaml
    - name: Aplicar o banner
      hosts: all
      become: true
      roles:
        - role: banner_login
          banner_login_texto: Acesso restrito
    ```
11. Exemplo:
    ```yaml
    - name: Importar a role do banner
      ansible.builtin.import_role:
        name: banner_login
    ```
12. Exemplo:
    ```yaml
    dependencies:
      - role: ferramentas_admin
    ```
13. Exemplo:
    ```yaml
    - src: file:///srv/roles/banner.tar
      name: banner_login
    ```
14. `ansible-galaxy role install -r roles/requirements.yml -p roles`
15. `collections_path = ./collections:/usr/share/ansible/collections` (na seção `[defaults]`).
16. Exemplo:
    ```yaml
    - name: Configurar sincronização de horário
      ansible.builtin.include_role:
        name: redhat.rhel_system_roles.timesync
    ```
17. `ansible-galaxy collection install -r collections/requirements.yml -p collections`
18. Foi para o primeiro diretório do `roles_path` (por padrão `~/.ansible/roles`), fora do projeto, que o execution environment não enxerga.
19. `vars/main.yml` da role tem precedência maior que o `vars` do play. Passe o valor como parâmetro em `roles:` (vence tudo) ou, se a variável deve ser ajustável, mova-a para `defaults/main.yml`.
20. A seção `roles` sempre roda antes de `tasks`. Troque a seção `roles` por `import_role`/`include_role` dentro de `tasks`, na posição desejada.
21. Se `ansible.posix` está instalada em um diretório do `collections_path` (por exemplo `./collections`) ou embutida no EE: `ansible-navigator collections list`.
22. Não: uma role roda uma vez por conjunto único de parâmetros. Para repetir, os parâmetros precisam mudar.
23. O token pode vazar pelo controle de versão. Remova-o do arquivo e use `ANSIBLE_GALAXY_SERVER_<ID>_TOKEN` como variável de ambiente.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 21–23 | Siga para o Capítulo 8 |
| 16–20 | Refaça a Parte C das lições onde errou |
| < 16 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
