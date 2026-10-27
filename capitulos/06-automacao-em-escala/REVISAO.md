# Revisão — Capítulo 6

Questões **autorais**. Elas não reproduzem o lab oficial nem perguntas de exame.
Use o inventário da [lição 6.3](6.3-selecionando-hosts-com-host-patterns.md#parte-b--modelo-mental-e-arquitetura)
nas questões de host patterns. Responda por escrito antes de abrir as respostas.

## Parte 1 — Conceitos

1. Cite quatro benefícios do design modular segundo o curso.
2. Qual a diferença entre importar e incluir conteúdo?
3. Por que não é possível usar loop com `import_tasks`?
4. Como um `when` se comporta em `import_tasks` e em `include_tasks`?
5. O que acontece com `--list-tasks` e `--start-at-task` quando as tasks vêm de um arquivo incluído?
6. Por que o curso recomenda escolher alvos com host patterns em vez de `when`?
7. Quando usar `ansible_host`?
8. Para que serve `--list-hosts`?

## Parte 2 — Escreva o arquivo, a task ou o pattern

9. Um playbook principal que importe `plays/rede.yml` e `plays/banco.yml`, nessa ordem.
10. Uma task que importe `tasks/usuarios.yml`.
11. Uma task que inclua `tasks/rhel10.yml` só em hosts com versão principal 10.
12. Um arquivo de tasks parametrizado por `pacote` que garanta o pacote instalado.
13. Uma task que importe o arquivo do item 12 para o pacote `tmux`.
14. Pattern: hosts de `app` e de `cache`.
15. Pattern: hosts de `servicos` que também estão em `sp`.
16. Pattern: todos os hosts que começam com `db`.
17. Comando: executar `site.yml` só nos hosts do grupo `rj`, sem editar o playbook.

## Parte 3 — Diagnóstico

18. O playbook falha antes de começar com erro sobre um arquivo importado. O que verificar?
19. `import_playbook` dentro de `tasks:` gera erro. Por quê?
20. Você precisa escolher o arquivo de tasks conforme uma variável registrada. `import_tasks` não funciona. Por quê, e o que usar?
21. `hosts: !cache*` dá erro de YAML. Corrija.
22. `hosts: 192.0.2.40` não atinge o host que tem esse IP. Explique.

---

<details>
<summary>Respostas comentadas</summary>

1. Qualidade de código e menos erros; manutenção simplificada; reuso e consistência; colaboração entre equipes.
2. Importar é estático (o conteúdo entra no parse, antes da execução); incluir é dinâmico (o conteúdo é processado quando a execução chega ao include).
3. Porque o import é resolvido no parse, antes da execução; loops só existem durante a execução. Para loops, use `include_tasks`.
4. Em `import_tasks`, a condição é aplicada a cada task importada. Em `include_tasks`, vale só para a task de include: decide se o arquivo entra.
5. `--list-tasks` mostra só a task de include, não as tasks do arquivo; `--start-at-task` não pode começar numa task de arquivo incluído.
6. Por segurança e confiabilidade (menos risco de rodar no host errado) e clareza (fica evidente quem é alvo).
7. Quando o nome do inventário não serve para conectar: resolve para outro IP, não está no DNS ou a política de rede exige um IP específico.
8. Para ver, por play, quais hosts o pattern casa, sem executar nenhuma task.
9. Exemplo:
   ```yaml
   ---
   - name: Rede
     ansible.builtin.import_playbook: plays/rede.yml

   - name: Banco
     ansible.builtin.import_playbook: plays/banco.yml
   ```
10. Exemplo:
    ```yaml
    - name: Importar os usuários
      ansible.builtin.import_tasks: tasks/usuarios.yml
    ```
11. Exemplo:
    ```yaml
    - name: Incluir ajustes do RHEL 10
      ansible.builtin.include_tasks: tasks/rhel10.yml
      when: ansible_facts['distribution_major_version'] == "10"
    ```
12. Exemplo:
    ```yaml
    ---
    - name: "Garantir o pacote: {{ pacote }}"
      ansible.builtin.dnf:
        name: "{{ pacote }}"
        state: present
    ```
13. Exemplo:
    ```yaml
    - name: Importar a instalação do tmux
      ansible.builtin.import_tasks: tasks/pacote.yml
      vars:
        pacote: tmux
    ```
14. `app,cache`
15. `servicos,&sp`
16. `'db*'`
17. `ansible-navigator run -m stdout site.yml --limit rj`
18. Se o caminho do arquivo está certo (relativo ao arquivo que importa) e se o arquivo tem sintaxe válida: imports falham imediatamente nesses casos.
19. `import_playbook` só pode ficar no nível superior do playbook; plays não podem ser aninhados.
20. O import é resolvido no parse, quando a variável registrada ainda não existe. Use `include_tasks`.
21. `hosts: '!cache*'` (entre aspas). Lembre que o pattern só com exclusão normalmente aparece combinado, por exemplo `'all,!cache*'`.
22. Um IP só funciona como pattern se estiver listado explicitamente no inventário.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 20–22 | Siga para o Capítulo 7 |
| 15–19 | Refaça a Parte C das lições onde errou |
| < 15 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
