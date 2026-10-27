# Glossário

Termos em ordem alfabética. Cobertura atual: **Capítulos 1 a 3** e fundamentos.

| Termo | Definição |
|-------|-----------|
| **Ad hoc command** | Execução de uma única task pela linha de comando (`ansible <padrão> -m <módulo>`), sem playbook |
| **Agentless** | Arquitetura sem agente residente nos managed hosts; o control node conecta, envia o módulo, executa e remove |
| **Ansible (pacote comunitário)** | `ansible-core` + seleção de collections da comunidade, com ciclo de release próprio |
| **Ansible Automation Platform (AAP)** | Produto empresarial da Red Hat, por assinatura: automation controller, UI/API, RBAC, conteúdo certificado, EEs e development tools suportados. AAP 2.6 ⇔ ansible-core 2.16 |
| **Ansible Content Collection** | Formato de distribuição de módulos, plug-ins, roles e documentação, independente do motor |
| **Ansible development tools** | Conjunto de CLIs para criar conteúdo: `ansible-lint`, `ansible-navigator`, `ansible-builder` e outras; RPM `ansible-dev-tools` |
| **Ansible Vault** | Recurso do Ansible para cifrar variáveis e arquivos (AES-256), decifrados na execução com a senha certa |
| **`ansible-builder`** | Constrói execution environments personalizados |
| **`ansible-core`** | Motor e linguagem do Ansible, CLIs e módulos `ansible.builtin`. Antes de 2.11 chamava-se `ansible-base` |
| **`ansible-lint`** | Analisador estático de conteúdo Ansible (erros comuns e padrões obsoletos) |
| **`ansible-navigator`** | *Automation content navigator*: executa e inspeciona conteúdo dentro de execution environments |
| **`ansible-navigator.yml`** | Arquivo de configuração do `ansible-navigator` (YAML ou JSON) |
| **`ansible.cfg`** | Arquivo INI de configuração do Ansible (`[defaults]`, `[privilege_escalation]`...) |
| **`ansible_host`** | Variável de inventário com o endereço real de conexão de um host |
| **`ansible_local`** | Chave de `ansible_facts` onde ficam os facts customizados de `/etc/ansible/facts.d/*.fact` |
| **`ansible_user`** | Variável de inventário com o usuário de conexão; vence o `remote_user` do play e do `ansible.cfg` |
| **Automation controller** | Componente do AAP (antigo Ansible Tower) para gerenciar e escalar automação entre equipes |
| **Automation execution environment (EE)** | Imagem de container (base RHEL UBI) com `ansible-core`, Python e collections, onde os playbooks rodam |
| **`become`** | Escalada de privilégio após conectar (padrão: `sudo` para `root`) |
| **Check mode (`--check`)** | Execução simulada (*dry run*): informa o que mudaria sem alterar os hosts |
| **Children (`:children`)** | Sufixo de seção INI que define um grupo cujos membros são outros grupos |
| **Control node** | Máquina de onde o Ansible é executado e onde ficam os arquivos do projeto |
| **Dev Containers** | Extensão do VS Code para desenvolver dentro de um container |
| **Development container** | Container onde o VS Code roda o ambiente de desenvolvimento (imagem `ansible-dev-tools`), via extensão Dev Containers |
| **Drift** | Divergência entre o estado real de um sistema e o estado declarado |
| **Extra vars (`-e`)** | Variáveis passadas na linha de comando; maior precedência de todas |
| **Fact** | Variável com informação descoberta no managed host pelo `ansible.builtin.setup` |
| **Fact customizado** | Fact declarado pelo próprio host em um arquivo `.fact` (INI, JSON ou script executável) |
| **FQCN** | *Fully qualified collection name*: `namespace.collection.modulo`, ex.: `ansible.builtin.ping` |
| **Gathering Facts** | Task automática no início de cada play que executa `ansible.builtin.setup` e coleta facts |
| **Git (staging area)** | Área intermediária onde ficam as alterações marcadas para o próximo commit |
| **`group_vars` / `host_vars`** | Diretórios com arquivos YAML de variáveis por grupo / por host, ao lado do inventário ou do playbook |
| **Grupo `all` / `ungrouped`** | Grupos implícitos: todos os hosts / hosts sem nenhum outro grupo |
| **Host pattern** | Expressão em `hosts:` (ou no comando ad hoc) que seleciona hosts do inventário |
| **`hostvars`** | Variável mágica com as variáveis de todos os hosts do inventário |
| **Idempotência** | Propriedade de produzir o mesmo resultado em execuções repetidas, sem mudanças se o estado já está correto |
| **Infraestrutura como código (IaC)** | Descrever o estado desejado da infraestrutura em arquivos versionáveis aplicados por ferramenta |
| **`inject_facts_as_vars`** | Opção do `ansible.cfg` que mantém a forma antiga `ansible_*` dos facts (padrão `true`) |
| **Inventário dinâmico** | Inventário gerado em tempo de execução por um plug-in que consulta fonte externa |
| **Inventory** | Lista de managed hosts e grupos; estática ou dinâmica |
| **Jinja2** | Motor de templates usado pelo Ansible para avaliar `{{ }}`, filtros e lógica simples |
| **Magic variables** | Variáveis definidas pelo Ansible (`inventory_hostname`, `group_names`, `groups`, `hostvars`); nomes reservados |
| **Managed host** | Sistema configurado pelo Ansible |
| **Module** | Programa pequeno que garante um aspecto do estado de um host |
| **`no_log`** | Palavra-chave que oculta argumentos e resultado de uma task na saída e nos logs |
| **Play** | Associação entre um conjunto de hosts e uma lista ordenada de tasks |
| **PLAY RECAP** | Resumo final por host: `ok`, `changed`, `unreachable`, `failed`, `skipped`, `rescued`, `ignored` |
| **Playbook** | Arquivo YAML com um ou mais plays |
| **Playbook artifact** | JSON gerado pelo `ansible-navigator run` com o registro de uma execução |
| **Plug-in** | Código que estende o motor (conexão, inventário, saída...) |
| **Precedência de variáveis** | Ordem que decide qual valor vale quando a mesma variável é definida em vários lugares |
| **Pull policy** | Quando o navigator baixa a imagem do EE: `always`, `missing`, `never` (📘 `tag`) |
| **Range (inventário)** | Notação `[início:fim(:passo)]` para gerar vários hostnames ou endereços |
| **`register`** | Palavra-chave que guarda o retorno de uma task em uma variável |
| **`remote_user`** | Usuário da conexão SSH; definido no `ansible.cfg` ou no play |
| **Replay** | `ansible-navigator replay <artefato>`: reexibe uma execução a partir do JSON do artefato |
| **`set_fact`** | Módulo que cria variáveis por host durante a execução |
| **Snippet (`doc -s`)** | Esqueleto de task com todos os parâmetros de um módulo, gerado por `ansible-navigator doc -s` |
| **Task** | Ação nomeada que chama um módulo com argumentos |
| **Terraform** | Ferramenta de IaC focada em provisionar infraestrutura (Day 0), com *state file*; complementar ao Ansible |
| **`UNREACHABLE` × `FAILED`** | Falha de conexão com o host × task executada que falhou |
| **`vars` / `vars_files`** | Variáveis definidas no play / carregadas de arquivos YAML externos pelo play |
| **Vault ID** | Rótulo associado a uma senha do vault (`rotulo@origem`), gravado no cabeçalho do arquivo cifrado (formato 1.2) |
| **WinRM / PSRP** | Protocolos usados para gerenciar hosts Windows |
| **Working tree** | Cópia de trabalho dos arquivos de um repositório Git |

---
[← Troubleshooting](troubleshooting.md) | [Índice geral](../README.md)
