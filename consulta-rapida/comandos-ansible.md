# Comandos Ansible — consulta rápida

Agrupados por tarefa. Cobertura atual: **Capítulos 1 a 7** e parte A do Capítulo 8. Ampliado a cada capítulo.

## Ferramentas e versões

| Tarefa | Comando |
|--------|---------|
| Instalar development tools (RHEL 10 + AAP 2.6) | `sudo subscription-manager repos --enable ansible-automation-platform-2.6-for-rhel-10-x86_64-rpms` · `sudo dnf install ansible-dev-tools` |
| Versão do navigator | `ansible-navigator --version` |
| Versão do lint | `ansible-lint --version` |
| Versão do ansible-core local e arquivo de config em uso (📘) | `ansible --version` |

## ansible-navigator

| Tarefa | Comando |
|--------|---------|
| Executar playbook | `ansible-navigator run <playbook>.yml` |
| Saída em texto | `... -m stdout` (`--mode stdout`) |
| Forçar TUI | `... -m interactive` |
| Sem artefato nesta execução | `... --pae false` |
| Escolher imagem do EE | `... --eei <registry>/<imagem>:<tag>` |
| Política de pull | `... --pp always\|missing\|never\|tag` |
| Engine de containers | `... --ce podman` |
| Listar/baixar imagens de EE | `ansible-navigator images` |
| Configuração efetiva | `ansible-navigator config` · na TUI: `:f <texto>`, número da linha, `Esc`, `:q` |
| Gerar `ansible.cfg` de referência | `ansible-navigator config init --disabled --eei <img> --pp never --mode stdout > ansible.cfg` |
| Documentação de módulo | `ansible-navigator doc <fqcn> -m stdout` |
| Snippet de task com todos os parâmetros | `ansible-navigator -s doc <fqcn>` |
| Listar módulos do EE | `ansible-navigator doc -l -m stdout` |
| Explorar collections do EE | `ansible-navigator collections` |
| Ver configurações do próprio navigator (📘) | `ansible-navigator settings --effective -m stdout` |

## Inventário (Cap. 2)

| Tarefa | Comando |
|--------|---------|
| Árvore de grupos e hosts | `ansible-navigator inventory -m stdout --graph [grupo]` |
| JSON completo | `ansible-navigator inventory -m stdout --list` |
| Variáveis de um host | `ansible-navigator inventory -m stdout --host <host>` |
| TUI (`:0` grupos, `:1` hosts) | `ansible-navigator inventory` |
| Inventário específico | `... -i <caminho>` |

## Execução e diagnóstico de playbooks (Cap. 2)

| Tarefa | Comando |
|--------|---------|
| Verificar sintaxe | `ansible-navigator run <pb>.yml --syntax-check` |
| Simular (dry run) | `ansible-navigator run <pb>.yml --check` |
| Mais detalhes | `ansible-navigator run <pb>.yml -v` … `-vvvvvv` |
| Passo a passo | `ansible-navigator run <pb>.yml -m stdout --pae false --step` |
| Começar em uma task | `ansible-navigator run <pb>.yml --start-at-task "<nome>"` |
| Listar tasks | `ansible-navigator run <pb>.yml --list-tasks` |
| Listar hosts por play | `ansible-navigator run <pb>.yml --list-hosts` |
| Restringir hosts na execução | `ansible-navigator run <pb>.yml --limit <pattern>` (ou `-l`) |
| Rever execução anterior | `ansible-navigator replay <pb>-artifact-<data>.json [-m stdout]` |
| Comando ad hoc | `ansible <padrão> -m <fqcn> [-a '<args>'] [-i <inv>]` |
| Ad hoc dentro do EE (📘) | `ansible-navigator exec -- ansible <padrão> -m <fqcn>` |

## Variáveis e Vault (Cap. 3)

| Tarefa | Comando |
|--------|---------|
| Extra var | `ansible-navigator run <pb>.yml -e chave=valor` |
| Onde a variável é definida | `grep -Rw <var>:` |
| Criar / cifrar arquivo | `ansible-vault create <f>` · `ansible-vault encrypt <f>...` |
| Cifrar valor | `ansible-vault encrypt_string --stdin-name <var>` |
| Ver / editar / decifrar | `ansible-vault view <f>` · `edit <f>` · `decrypt <f> --output=<novo>` |
| Trocar senha | `ansible-vault rekey <f>` |
| Cifrar com vault ID | `ansible-vault encrypt <f> --vault-id <rótulo>@<origem>` |
| Executar pedindo senha | `ansible-navigator run <pb>.yml -m stdout --pae false --ask-vault-pass` |
| Executar com arquivo de senha | `ansible-navigator run <pb>.yml --vault-password-file=<f>` |
| Executar com vault IDs | `ansible-navigator run <pb>.yml --vault-id a@<f1> --vault-id b@<f2>` |

## Roles e collections (Cap. 7)

| Tarefa | Comando |
|--------|---------|
| Criar esqueleto de role | `ansible-galaxy role init roles/<role>` |
| Instalar roles do projeto | `ansible-galaxy role install -r roles/requirements.yml -p roles` |
| Listar / remover / buscar roles | `ansible-galaxy role list` · `role remove <role>` · `role search <termo> --platforms EL` |
| Instalar collections do projeto | `ansible-galaxy collection install -r collections/requirements.yml -p collections` |
| Instalar collection de arquivo | `ansible-galaxy collection install <arquivo>.tar.gz -p collections` |
| Listar collections | `ansible-galaxy collection list` · `ansible-navigator collections list` |
| Documentação no EE (TUI) | `ansible-navigator collections -m interactive` |
| Montar diretório extra no EE | `ansible-navigator run <pb>.yml --volume <local>:<no-container>` |

## Administração Linux (Cap. 8, parte A)

| Tarefa | Comando |
|--------|---------|
| Instalar system roles (AAP) | `ansible-galaxy collection install -p collections/ -r collections/requirements.yml` |
| Instalar system roles (RPM) | `sudo dnf install rhel-system-roles` |
| Registrar (sem Ansible, RHEL 10 com SCA) | `sudo subscription-manager register` · `sudo subscription-manager attach --auto` |
| Habilitar repositórios (sem Ansible) | `sudo subscription-manager repos --enable <repo>` |
| Listar lookups | `ansible-navigator doc -l -t lookup` |

## ansible-core (local)

| Tarefa | Comando |
|--------|---------|
| Gerar `ansible.cfg` comentado | `ansible-config init --disabled > ansible.cfg` |
| Só o que foi alterado (📘) | `ansible-config dump --only-changed` |
| Todas as opções, com env e chave INI (📘) | `ansible-config list` |
| Checar sintaxe (📘) | `ansible-playbook --syntax-check <playbook>.yml` |
| Ver inventário resolvido (📘) | `ansible-inventory --graph` |

## Qualidade

| Tarefa | Comando |
|--------|---------|
| Lint de um playbook | `ansible-lint <playbook>.yml` |
| Lint do projeto inteiro | `ansible-lint` (na raiz do projeto) |
| Validar YAML (📘) | `yamllint <arquivo>.yml` |

## SSH e privilégio (managed hosts)

| Tarefa | Comando |
|--------|---------|
| Gerar par de chaves | `ssh-keygen` |
| Instalar chave pública | `ssh-copy-id <remote_user>@<host>` |
| Testar login sem senha | `ssh <remote_user>@<host> true` |
| Validar arquivo sudoers (📘) | `sudo visudo -cf /etc/sudoers.d/<arquivo>` |

## Git

| Tarefa | Comando |
|--------|---------|
| Identidade | `git config --global user.name '...'` · `git config --global user.email ...` |
| Clonar | `git clone <url>` |
| Estado | `git status` · `git diff` · `git log --oneline` |
| Preparar / desfazer preparo | `git add <arq>` · `git restore --staged <arq>` |
| Gravar | `git commit -m "mensagem"` |
| Enviar / receber | `git push` · `git pull` |

## Registry e containers

| Tarefa | Comando |
|--------|---------|
| Login | `podman login <registry>` |
| Imagens locais | `podman images` |

---
[Índice geral](../README.md) | [Configuração →](configuracao-ansible-e-navigator.md)
