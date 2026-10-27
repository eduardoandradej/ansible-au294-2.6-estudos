# Comandos Ansible — consulta rápida

Agrupados por tarefa. Cobertura atual: **Capítulo 1**. Ampliado a cada capítulo.

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
| Ver configurações do próprio navigator (📘) | `ansible-navigator settings --effective -m stdout` |

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
