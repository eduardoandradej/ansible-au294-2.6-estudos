# Glossário

Termos em ordem alfabética. Cobertura atual: **Capítulos 1 a 7** e fundamentos.

| Termo | Definição |
|-------|-----------|
| **`--limit` (`-l`)** | Opção que restringe os hosts atingidos em uma execução, sem editar o playbook |
| **`--list-hosts`** | Opção que mostra os hosts casados por cada play, sem executar tasks |
| **Ad hoc command** | Execução de uma única task pela linha de comando (`ansible <padrão> -m <módulo>`), sem playbook |
| **Agentless** | Arquitetura sem agente residente nos managed hosts; o control node conecta, envia o módulo, executa e remove |
| **Ansible (pacote comunitário)** | `ansible-core` + seleção de collections da comunidade, com ciclo de release próprio |
| **Ansible Automation Platform (AAP)** | Produto empresarial da Red Hat, por assinatura: automation controller, UI/API, RBAC, conteúdo certificado, EEs e development tools suportados. AAP 2.6 ⇔ ansible-core 2.16 |
| **Ansible Content Collection** | Formato de distribuição de módulos, plug-ins, roles e documentação, independente do motor |
| **Ansible development tools** | Conjunto de CLIs para criar conteúdo: `ansible-lint`, `ansible-navigator`, `ansible-builder` e outras; RPM `ansible-dev-tools` |
| **Ansible Vault** | Recurso do Ansible para cifrar variáveis e arquivos (AES-256), decifrados na execução com a senha certa |
| **`ansible-builder`** | Constrói execution environments personalizados |
| **`ansible-core`** | Motor e linguagem do Ansible, CLIs e módulos `ansible.builtin`. Antes de 2.11 chamava-se `ansible-base` |
| **`ansible-galaxy`** | Comando que cria, instala, lista e remove roles e collections |
| **`ansible-lint`** | Analisador estático de conteúdo Ansible (erros comuns e padrões obsoletos) |
| **`ansible-navigator`** | *Automation content navigator*: executa e inspeciona conteúdo dentro de execution environments |
| **`ansible-navigator.yml`** | Arquivo de configuração do `ansible-navigator` (YAML ou JSON) |
| **`ansible.cfg`** | Arquivo INI de configuração do Ansible (`[defaults]`, `[privilege_escalation]`...) |
| **`ansible_host`** | Variável de inventário com o endereço real de conexão de um host |
| **`ansible_local`** | Chave de `ansible_facts` onde ficam os facts customizados de `/etc/ansible/facts.d/*.fact` |
| **`ansible_managed`** | Variável especial com o texto (definido no `ansible.cfg`) que indica que um arquivo é gerenciado pelo Ansible |
| **`ansible_user`** | Variável de inventário com o usuário de conexão; vence o `remote_user` do play e do `ansible.cfg` |
| **Arquivo de tasks** | Arquivo YAML com uma lista de tasks (sem play), usado com `import_tasks`/`include_tasks` |
| **Automation controller** | Componente do AAP (antigo Ansible Tower) para gerenciar e escalar automação entre equipes |
| **Automation execution environment (EE)** | Imagem de container (base RHEL UBI) com `ansible-core`, Python e collections, onde os playbooks rodam |
| **`become`** | Escalada de privilégio após conectar (padrão: `sudo` para `root`) |
| **`block` / `rescue` / `always`** | Agrupamento de tasks; `rescue` roda se o `block` falhar; `always` roda sempre |
| **`changed_when`** | Condição personalizada para a task reportar `changed` |
| **Check mode (`--check`)** | Execução simulada (*dry run*): informa o que mudaria sem alterar os hosts |
| **Children (`:children`)** | Sufixo de seção INI que define um grupo cujos membros são outros grupos |
| **`collections_path`** | Configuração com a lista ordenada de diretórios onde o Ansible procura collections |
| **Control node** | Máquina de onde o Ansible é executado e onde ficam os arquivos do projeto |
| **`defaults/main.yml`** | Arquivo de variáveis padrão de uma role, com a menor precedência |
| **Dependência de role** | Role listada em `dependencies` do `meta/main.yml`, executada antes da role que a declara |
| **Dev Containers** | Extensão do VS Code para desenvolver dentro de um container |
| **Development container** | Container onde o VS Code roda o ambiente de desenvolvimento (imagem `ansible-dev-tools`), via extensão Dev Containers |
| **Drift** | Divergência entre o estado real de um sistema e o estado declarado |
| **Extra vars (`-e`)** | Variáveis passadas na linha de comando; maior precedência de todas |
| **Fact** | Variável com informação descoberta no managed host pelo `ansible.builtin.setup` |
| **Fact customizado** | Fact declarado pelo próprio host em um arquivo `.fact` (INI, JSON ou script executável) |
| **`failed_when`** | Condição personalizada para a task ser considerada falha |
| **Filtro (Jinja2)** | Função aplicada com `|` que transforma um valor (`to_nice_yaml`, `lower`, `default`...) |
| **`flush_handlers`** | Ação de `ansible.builtin.meta` que executa naquele ponto os handlers já notificados |
| **`force_handlers`** | Palavra-chave de play que faz handlers já notificados rodarem mesmo após falha |
| **FQCN** | *Fully qualified collection name*: `namespace.collection.modulo`, ex.: `ansible.builtin.ping` |
| **FQRN** | Nome qualificado de role de collection: `namespace.collection.role` |
| **Gathering Facts** | Task automática no início de cada play que executa `ansible.builtin.setup` e coleta facts |
| **Git (staging area)** | Área intermediária onde ficam as alterações marcadas para o próximo commit |
| **`group_vars` / `host_vars`** | Diretórios com arquivos YAML de variáveis por grupo / por host, ao lado do inventário ou do playbook |
| **Grupo `all` / `ungrouped`** | Grupos implícitos: todos os hosts / hosts sem nenhum outro grupo |
| **Handler** | Task que só roda quando notificada por uma task `changed`, normalmente no fim do play |
| **Host pattern** | Expressão em `hosts:` (ou no comando ad hoc) que seleciona hosts do inventário |
| **`hostvars`** | Variável mágica com as variáveis de todos os hosts do inventário |
| **Idempotência** | Propriedade de produzir o mesmo resultado em execuções repetidas, sem mudanças se o estado já está correto |
| **`ignore_errors`** | Palavra-chave de task que mantém a execução após a falha dela |
| **`import_playbook`** | Módulo que importa os plays de outro playbook, no nível superior |
| **`import_role` / `include_role`** | Módulos que usam uma role como task, de forma estática / dinâmica |
| **`import_tasks`** | Módulo que importa tasks de forma estática, no parse do playbook |
| **`include_tasks`** | Módulo que inclui tasks de forma dinâmica, quando a execução chega ao include |
| **Infraestrutura como código (IaC)** | Descrever o estado desejado da infraestrutura em arquivos versionáveis aplicados por ferramenta |
| **`inject_facts_as_vars`** | Opção do `ansible.cfg` que mantém a forma antiga `ansible_*` dos facts (padrão `true`) |
| **Inventário dinâmico** | Inventário gerado em tempo de execução por um plug-in que consulta fonte externa |
| **Inventory** | Lista de managed hosts e grupos; estática ou dinâmica |
| **`item`** | Variável que guarda o valor da iteração atual de um loop |
| **Jinja2** | Motor de templates usado pelo Ansible para avaliar `{{ }}`, filtros e lógica simples |
| **`loop`** | Palavra-chave de task que itera sobre uma lista |
| **`loop.index`** | Número da iteração atual de um `{% for %}` em um template (começa em 1) |
| **Magic variables** | Variáveis definidas pelo Ansible (`inventory_hostname`, `group_names`, `groups`, `hostvars`); nomes reservados |
| **Managed host** | Sistema configurado pelo Ansible |
| **Marcador (`blockinfile`)** | Linhas de comentário que delimitam um bloco gerenciado e garantem sua idempotência |
| **Module** | Programa pequeno que garante um aspecto do estado de um host |
| **`no_log`** | Palavra-chave que oculta argumentos e resultado de uma task na saída e nos logs |
| **`notify`** | Palavra-chave de task que notifica handlers quando ela reporta `changed` |
| **Play** | Associação entre um conjunto de hosts e uma lista ordenada de tasks |
| **PLAY RECAP** | Resumo final por host: `ok`, `changed`, `unreachable`, `failed`, `skipped`, `rescued`, `ignored` |
| **Playbook** | Arquivo YAML com um ou mais plays |
| **Playbook artifact** | JSON gerado pelo `ansible-navigator run` com o registro de uma execução |
| **Plug-in** | Código que estende o motor (conexão, inventário, saída...) |
| **`pre_tasks` / `post_tasks`** | Seções de play que rodam antes das roles / depois das tasks |
| **Precedência de variáveis** | Ordem que decide qual valor vale quando a mesma variável é definida em vários lugares |
| **Private automation hub** | Hub local da organização para conteúdo confiável; fonte recomendada pela Red Hat |
| **Pull policy** | Quando o navigator baixa a imagem do EE: `always`, `missing`, `never` (📘 `tag`) |
| **Range (inventário)** | Notação `[início:fim(:passo)]` para gerar vários hostnames ou endereços |
| **`register`** | Palavra-chave que guarda o retorno de uma task em uma variável |
| **`remote_src`** | Parâmetro do `copy` que indica que a origem está no managed host |
| **`remote_user`** | Usuário da conexão SSH; definido no `ansible.cfg` ou no play |
| **Replay** | `ansible-navigator replay <artefato>`: reexibe uma execução a partir do JSON do artefato |
| **`requirements.yml`** | Manifesto de roles (`roles/`) ou collections (`collections/`) a instalar com `ansible-galaxy` |
| **Role** | Unidade de reuso com estrutura padrão (`tasks`, `handlers`, `defaults`, `vars`, `files`, `templates`, `meta`) |
| **`set_fact`** | Módulo que cria variáveis por host durante a execução |
| **Snippet (`doc -s`)** | Esqueleto de task com todos os parâmetros de um módulo, gerado por `ansible-navigator doc -s` |
| **Task** | Ação nomeada que chama um módulo com argumentos |
| **Template** | Arquivo-modelo Jinja2 (normalmente `.j2`) renderizado por host pelo módulo `ansible.builtin.template` |
| **Terraform** | Ferramenta de IaC focada em provisionar infraestrutura (Day 0), com *state file*; complementar ao Ansible |
| **`UNREACHABLE` × `FAILED`** | Falha de conexão com o host × task executada que falhou |
| **`vars` / `vars_files`** | Variáveis definidas no play / carregadas de arquivos YAML externos pelo play |
| **`vars/main.yml` (role)** | Arquivo de variáveis internas de uma role, com precedência alta |
| **Vault ID** | Rótulo associado a uma senha do vault (`rotulo@origem`), gravado no cabeçalho do arquivo cifrado (formato 1.2) |
| **`when`** | Palavra-chave de task (ou bloco) com a condição para executá-la |
| **WinRM / PSRP** | Protocolos usados para gerenciar hosts Windows |
| **`with_items`** | Sintaxe antiga de loop (antes do Ansible 2.5); achata listas aninhadas |
| **Working tree** | Cópia de trabalho dos arquivos de um repositório Git |

---
[← Troubleshooting](troubleshooting.md) | [Índice geral](../README.md)
