# Revisão — Capítulo 4

Questões **autorais**. Elas não reproduzem o lab oficial nem perguntas de exame.
Responda por escrito antes de abrir as respostas.

## Parte 1 — Conceitos

1. Que tipos de dados um loop pode percorrer, segundo o curso?
2. Qual a diferença entre `loop` e `with_items`? Por que a Red Hat recomenda `loop`?
3. Como é a estrutura de uma variável registrada em uma task com loop?
4. Onde fica o `when` em uma task e por quê?
5. Quando um handler é executado e em que ordem?
6. O que `force_handlers` garante e o que ele **não** faz?
7. Qual a diferença entre `failed_when` e `ansible.builtin.fail`?
8. Explique `block`, `rescue` e `always`.

## Parte 2 — Escreva a task ou o play

9. Uma task que garanta os grupos `dev`, `ops` e `audit` com `ansible.builtin.group`, usando `loop`.
10. Uma task que crie os usuários de uma lista `contas` (dicionários com `nome` e `uid`).
11. Uma task que instale `tuned` somente se a variável `perfil_desempenho` estiver definida.
12. Uma condição que seja verdadeira em RedHat 10 **ou** em Fedora 42, com parênteses.
13. Uma task que copie `files/chrony.conf` para `/etc/chrony.conf` e notifique `Reiniciar chronyd`, e o handler correspondente.
14. Uma task que rode `/usr/local/bin/checar-disco` e nunca reporte `changed`.
15. Um bloco que execute `/opt/deploy.sh`, rode `/opt/rollback.sh` se falhar e sempre garanta o serviço `app` ativo.
16. Uma task que falhe com mensagem clara se `ansible_facts['memtotal_mb']` for menor que 2048.

## Parte 3 — Diagnóstico

17. A task com `loop` falha com `'item' is undefined`. Onde está o erro mais provável?
18. Depois de `register: r` em um loop, `{{ r['stdout'] }}` não existe. Por quê?
19. O handler nunca roda, embora a task de configuração mostre `changed`. O que verificar?
20. O playbook termina "verde", mas um pacote obrigatório não foi instalado. Qual palavra-chave provavelmente está escondendo o problema?
21. Um teste logo após mudar a configuração falha porque o serviço ainda não foi reiniciado. Como resolver sem mover o teste para outro play?
22. Um handler notificado não roda porque uma task posterior falhou. O que fazer?

---

<details>
<summary>Respostas comentadas</summary>

1. Itens de uma lista, um dicionário com duas ou mais chaves, o valor de uma variável registrada, uma sequência numérica e estruturas mais complexas.
2. `with_items` é a sintaxe antiga (antes do Ansible 2.5) e achata listas aninhadas; `loop` é a forma recomendada, mais simples e consistente.
3. Um dicionário com `changed`, `msg` e `results`; `results` é uma lista com um dicionário por item (com `item` e o retorno do módulo).
4. No nível da task, ao lado de `name` e do módulo, porque é uma palavra-chave da task e não um argumento do módulo.
5. Quando notificado por uma task `changed`; por padrão, depois de todas as tasks do play (ou num `flush_handlers`), na ordem da seção `handlers`.
6. Garante que handlers **já notificados** rodem mesmo se uma task posterior falhar; não cria novas notificações.
7. `failed_when` define a condição de falha na própria task; `ansible.builtin.fail` é uma task dedicada (com `when`) que falha com mensagem e permite inserir passos antes da falha.
8. `block` contém as tasks principais; `rescue` roda se alguma delas falhar; `always` roda sempre, depois de `block`/`rescue`.
9. Exemplo:
   ```yaml
   - name: Garantir os grupos de trabalho
     ansible.builtin.group:
       name: "{{ item }}"
       state: present
     loop:
       - dev
       - ops
       - audit
   ```
10. Exemplo:
    ```yaml
    - name: Garantir as contas
      ansible.builtin.user:
        name: "{{ item['nome'] }}"
        uid: "{{ item['uid'] }}"
        state: present
      loop: "{{ contas }}"
    ```
11. Exemplo:
    ```yaml
    - name: Instalar tuned quando houver perfil definido
      ansible.builtin.dnf:
        name: tuned
        state: present
      when: perfil_desempenho is defined
    ```
12. Exemplo:
    ```yaml
    when: >
      ( ansible_facts['distribution'] == "RedHat" and
        ansible_facts['distribution_major_version'] == "10" )
      or
      ( ansible_facts['distribution'] == "Fedora" and
        ansible_facts['distribution_major_version'] == "42" )
    ```
13. Exemplo:
    ```yaml
    tasks:
      - name: Publicar a configuração do chrony
        ansible.builtin.copy:
          src: files/chrony.conf
          dest: /etc/chrony.conf
          mode: '0644'
        notify: Reiniciar chronyd

    handlers:
      - name: Reiniciar chronyd
        ansible.builtin.systemd_service:
          name: chronyd
          state: restarted
    ```
14. Exemplo:
    ```yaml
    - name: Checar o disco
      ansible.builtin.command:
        cmd: /usr/local/bin/checar-disco
      changed_when: false
    ```
15. Exemplo:
    ```yaml
    - name: Implantar com recuperação
      block:
        - name: Executar o deploy
          ansible.builtin.command:
            cmd: /opt/deploy.sh
      rescue:
        - name: Desfazer o deploy
          ansible.builtin.command:
            cmd: /opt/rollback.sh
      always:
        - name: Garantir o serviço da aplicação
          ansible.builtin.systemd_service:
            name: app
            state: started
    ```
16. Exemplo:
    ```yaml
    - name: Exigir pelo menos 2 GiB de RAM
      ansible.builtin.fail:
        msg: "Memória insuficiente: {{ ansible_facts['memtotal_mb'] }} MiB"
      when: ansible_facts['memtotal_mb'] < 2048
    ```
17. `loop` indentado como parâmetro do módulo (ou ausente). `loop` fica no nível da task.
18. Com loop, os resultados ficam em `r['results']`, um por item: `r['results'][0]['stdout']`.
19. Se o nome no `notify` é idêntico ao `name` do handler, se a seção `handlers` está no nível do play e se nenhuma task falhou antes do fim do play.
20. `ignore_errors: true`.
21. `ansible.builtin.meta: flush_handlers` antes do teste.
22. `force_handlers: true` no play (ou corrigir a task que falha).

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 20–22 | Siga para o Capítulo 5 |
| 15–19 | Refaça a Parte C das lições onde errou |
| < 15 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
