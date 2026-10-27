# Glossário

Termos em ordem alfabética. Cobertura atual: **Capítulo 1** e fundamentos.

| Termo | Definição |
|-------|-----------|
| **Agentless** | Arquitetura sem agente residente nos managed hosts; o control node conecta, envia o módulo, executa e remove |
| **Ansible (pacote comunitário)** | `ansible-core` + seleção de collections da comunidade, com ciclo de release próprio |
| **Ansible Automation Platform (AAP)** | Produto empresarial da Red Hat, por assinatura: automation controller, UI/API, RBAC, conteúdo certificado, EEs e development tools suportados. AAP 2.6 ⇔ ansible-core 2.16 |
| **Ansible Content Collection** | Formato de distribuição de módulos, plug-ins, roles e documentação, independente do motor |
| **Ansible development tools** | Conjunto de CLIs para criar conteúdo: `ansible-lint`, `ansible-navigator`, `ansible-builder` e outras; RPM `ansible-dev-tools` |
| **`ansible-builder`** | Constrói execution environments personalizados |
| **`ansible.cfg`** | Arquivo INI de configuração do Ansible (`[defaults]`, `[privilege_escalation]`...) |
| **`ansible-core`** | Motor e linguagem do Ansible, CLIs e módulos `ansible.builtin`. Antes de 2.11 chamava-se `ansible-base` |
| **`ansible-lint`** | Analisador estático de conteúdo Ansible (erros comuns e padrões obsoletos) |
| **`ansible-navigator`** | *Automation content navigator*: executa e inspeciona conteúdo dentro de execution environments |
| **`ansible-navigator.yml`** | Arquivo de configuração do `ansible-navigator` (YAML ou JSON) |
| **Automation controller** | Componente do AAP (antigo Ansible Tower) para gerenciar e escalar automação entre equipes |
| **Automation execution environment (EE)** | Imagem de container (base RHEL UBI) com `ansible-core`, Python e collections, onde os playbooks rodam |
| **`become`** | Escalada de privilégio após conectar (padrão: `sudo` para `root`) |
| **Control node** | Máquina de onde o Ansible é executado e onde ficam os arquivos do projeto |
| **Development container** | Container onde o VS Code roda o ambiente de desenvolvimento (imagem `ansible-dev-tools`), via extensão Dev Containers |
| **Dev Containers** | Extensão do VS Code para desenvolver dentro de um container |
| **Drift** | Divergência entre o estado real de um sistema e o estado declarado |
| **FQCN** | *Fully qualified collection name*: `namespace.collection.modulo`, ex.: `ansible.builtin.ping` |
| **Git (staging area)** | Área intermediária onde ficam as alterações marcadas para o próximo commit |
| **Idempotência** | Propriedade de produzir o mesmo resultado em execuções repetidas, sem mudanças se o estado já está correto |
| **Infraestrutura como código (IaC)** | Descrever o estado desejado da infraestrutura em arquivos versionáveis aplicados por ferramenta |
| **Inventory** | Lista de managed hosts e grupos; estática ou dinâmica |
| **Managed host** | Sistema configurado pelo Ansible |
| **Module** | Programa pequeno que garante um aspecto do estado de um host |
| **Play** | Associação entre um conjunto de hosts e uma lista ordenada de tasks |
| **Playbook** | Arquivo YAML com um ou mais plays |
| **Playbook artifact** | JSON gerado pelo `ansible-navigator run` com o registro de uma execução |
| **Plug-in** | Código que estende o motor (conexão, inventário, saída...) |
| **Pull policy** | Quando o navigator baixa a imagem do EE: `always`, `missing`, `never` (📘 `tag`) |
| **Task** | Ação nomeada que chama um módulo com argumentos |
| **Terraform** | Ferramenta de IaC focada em provisionar infraestrutura (Day 0), com *state file*; complementar ao Ansible |
| **WinRM / PSRP** | Protocolos usados para gerenciar hosts Windows |
| **Working tree** | Cópia de trabalho dos arquivos de um repositório Git |

---
[← Troubleshooting](troubleshooting.md) | [Índice geral](../README.md)
