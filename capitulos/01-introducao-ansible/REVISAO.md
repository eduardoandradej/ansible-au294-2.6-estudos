# Revisão — Capítulo 1

Questões **autorais**. Elas não reproduzem o quiz oficial nem perguntas de exame.
Responda por escrito (ou no terminal, com um `lab start` ativo) antes de abrir as
respostas.

## Parte 1 — Conceitos

1. Explique "agentless" e cite o que um managed host Linux precisa ter para ser gerenciado.
2. Qual a relação entre playbook, play, task e módulo? Em que ordem as tasks de um play são executadas?
3. O que é idempotência e por que ela permite reaplicar um playbook para corrigir *drift*?
4. Diferencie `ansible-core`, o pacote comunitário `ansible` e o Red Hat Ansible Automation Platform.
5. Por que o Ansible foi dividido em motor + collections a partir da 2.10? Cite os três problemas do modelo anterior.
6. Qual versão do `ansible-core` corresponde ao AAP 2.6?
7. Qual a diferença entre o development container e o automation execution environment?
8. Para que servem `ansible-lint`, `ansible-navigator` e `ansible-builder`?
9. Em que situação Terraform e Ansible trabalham juntos, e como a saída de um vira entrada do outro?

## Parte 2 — Configuração (escreva o arquivo ou o comando)

10. Escreva um `ansible.cfg` que use o inventário `./hosts`, conecte como `deploy` por chave SSH e **não** faça escalada por padrão.
11. Escreva um `ansible-navigator.yml` que use Podman, a imagem `registry.example.net/ee/minimal:2.6`, baixe a imagem só se faltar, saia em `stdout` e não gere artefatos.
12. Gere um `ansible.cfg` de referência com todas as opções comentadas.
13. Abra a configuração efetiva do Ansible em modo interativo, mesmo que o projeto use `mode: stdout`.
14. Instale sua chave pública no usuário `deploy` do host `app01.example.net`.
15. Execute um playbook `site.yml` desligando os artefatos **só nesta execução**.
16. No Git, prepare apenas `ansible.cfg`, grave com uma mensagem e envie ao remoto.

## Parte 3 — Diagnóstico

17. Você editou `./ansible.cfg`, mas `ansible-navigator config` mostra que o `Source` de *Default remote user* é `/etc/ansible/custom.cfg`. O que provavelmente está acontecendo?
18. Um playbook com `become: true` falha com `Missing sudo password`. Liste duas correções possíveis e o impacto de segurança de cada uma.
19. Um playbook pede senha, mas a execução trava sem mostrar o prompt. Quais configurações do navigator você verifica?
20. Depois de copiar o projeto para `/srv/shared` (permissão `777`), o Ansible passou a conectar como outro usuário e a ignorar o inventário. Explique.
21. O playbook roda pelo menu do VS Code, mas falha no terminal integrado com outra imagem de EE. Por quê?

---

<details>
<summary>Respostas comentadas</summary>

1. Não há agente residente: o control node conecta (SSH no Linux), envia o módulo, executa e remove. O managed host Linux precisa de **SSH acessível** e **Python**; para tarefas privilegiadas, um usuário com `sudo` (ou outro método de `become`).
2. Playbook (arquivo YAML) contém plays; cada play liga hosts a uma lista de tasks; cada task chama um módulo. As tasks rodam **em ordem**, de cima para baixo; uma falha interrompe o play **para aquele host**.
3. Executar várias vezes leva ao mesmo estado e, se o estado já está correto, nada muda (`ok`). Ao reaplicar, só o que divergiu é corrigido, o que torna a reexecução segura.
4. `ansible-core`: motor, linguagem, CLIs e `ansible.builtin`. Pacote `ansible`: `ansible-core` + seleção de collections da comunidade. AAP: produto empresarial por assinatura (automation controller, UI/API, RBAC, conteúdo certificado, suporte, development tools e EEs suportados).
5. Para entregar conteúdo de forma independente do motor. Problemas: atualizações raras (só com releases maiores), pacote inchado (todos recebiam tudo) e rigidez de versões (não dava para atualizar conteúdo sem trocar o motor).
6. **2.16** (o AAP 2.5 também usa 2.16; o 2.4 usava 2.15).
7. O development container hospeda o ambiente de edição e as ferramentas (imagem `ansible-dev-tools`); o EE é onde o playbook roda (`ansible-core` + collections), igual do notebook ao automation controller.
8. `ansible-lint`: análise estática antes do commit. `ansible-navigator`: executar e inspecionar conteúdo em EEs. `ansible-builder`: construir EEs personalizados.
9. Terraform provisiona (Day 0); Ansible configura e mantém (Day 1/2). As saídas do Terraform (IPs, nomes) podem gerar dinamicamente o inventário do Ansible.
10. Exemplo:
    ```ini
    [defaults]
    inventory = ./hosts
    remote_user = deploy
    ask_pass = false

    [privilege_escalation]
    become = false
    ```
    (A seção `[privilege_escalation]` é opcional, porque `become = false` já é o padrão.)
11. Exemplo:
    ```yaml
    ---
    ansible-navigator:
      execution-environment:
        container-engine: podman
        enabled: true
        image: registry.example.net/ee/minimal:2.6
        pull:
          policy: missing
      mode: stdout
      playbook-artifact:
        enable: false
    ```
12. `ansible-config init --disabled > ansible.cfg` (ou `ansible-navigator config init --disabled --mode stdout ... > ansible.cfg`).
13. `ansible-navigator config -m interactive`
14. `ssh-copy-id deploy@app01.example.net` (gere antes o par com `ssh-keygen`, se necessário).
15. `ansible-navigator run site.yml --pae false`
16. `git add ansible.cfg && git commit -m "Define usuário remoto deploy" && git push`
17. A variável de ambiente **`ANSIBLE_CONFIG`** está apontando para `/etc/ansible/custom.cfg`, que tem prioridade sobre o `./ansible.cfg`. Confira com `env | grep ANSIBLE_CONFIG` e remova com `unset ANSIBLE_CONFIG` (ou ajuste o valor).
18. (a) Configurar `NOPASSWD` para o usuário de automação em `/etc/sudoers.d/` (validando com `visudo -cf`): mais prático, mas a chave SSH dessa conta passa a equivaler a `root`. (b) `become_ask_pass = true` ou `-K` na execução: mais controle, mas exige interação (modo `stdout`, artefatos desligados) e dificulta execuções não assistidas.
19. `mode` deve ser `stdout` e `playbook-artifact.enable` deve ser `false` (ou `-m stdout --pae false`).
20. O diretório é **gravável por todos**: por segurança, o Ansible ignora o `ansible.cfg` ali (aviso de *world writable directory*). Sem o arquivo do projeto, voltam os padrões (sem inventário do projeto; no EE, `root` como usuário). Corrija com `chmod o-w /srv/shared` ou aponte com `ANSIBLE_CONFIG`.
21. O menu usa as **configurações da extensão Ansible** do VS Code; o terminal usa o **`ansible-navigator.yml`** do projeto. Estão divergentes: iguale imagem, engine e política de pull nos dois.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 19–21 | Siga para o Capítulo 2 |
| 15–18 | Refaça a Parte C das lições onde errou |
| < 15 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
