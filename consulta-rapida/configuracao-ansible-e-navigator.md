# Configuração: `ansible.cfg` e `ansible-navigator.yml`

Referência condensada da [seção 1.5](../capitulos/01-introducao-ansible/1.5-configurando-ajustes-do-ansible.md).

## Precedência (o primeiro arquivo encontrado vence)

| # | Ansible | ansible-navigator |
|---|---------|-------------------|
| 1 | `$ANSIBLE_CONFIG` | `$ANSIBLE_NAVIGATOR_CONFIG` |
| 2 | `./ansible.cfg` | `./ansible-navigator.yml` |
| 3 | `~/.ansible.cfg` | `~/.ansible-navigator.yml` |
| 4 | `/etc/ansible/ansible.cfg` | — |

📘 `ansible.cfg` em diretório gravável por todos é ignorado.

## `ansible.cfg`

| Seção | Chave | Padrão | Variável de ambiente (📘) |
|-------|-------|--------|---------------------------|
| `[defaults]` | `inventory` | `/etc/ansible/hosts` (📘) | `ANSIBLE_INVENTORY` |
| `[defaults]` | `remote_user` | padrão da conexão (no EE: `root`, segundo o curso) | `ANSIBLE_REMOTE_USER` |
| `[defaults]` | `ask_pass` | `false` | `ANSIBLE_ASK_PASS` |
| `[defaults]` | `host_key_checking` | `True` | `ANSIBLE_HOST_KEY_CHECKING` |
| `[defaults]` | `timeout` | `10` | `ANSIBLE_TIMEOUT` |
| `[defaults]` | `log_path` | desligado | `ANSIBLE_LOG_PATH` |
| `[defaults]` | `private_key_file` | — | `ANSIBLE_PRIVATE_KEY_FILE` |
| `[defaults]` | `transport` (o PDF chama de `connection`) | `ssh` | `ANSIBLE_TRANSPORT` |
| `[privilege_escalation]` | `become` | `false` | `ANSIBLE_BECOME` |
| `[privilege_escalation]` | `become_method` | `sudo` | `ANSIBLE_BECOME_METHOD` |
| `[privilege_escalation]` | `become_user` | `root` | `ANSIBLE_BECOME_USER` |
| `[privilege_escalation]` | `become_ask_pass` | `false` | `ANSIBLE_BECOME_ASK_PASS` |

Comentários: `#` no início da linha; `;` em qualquer posição (comenta o resto da linha).

## `ansible-navigator.yml`

```yaml
---
ansible-navigator:
  execution-environment:
    container-engine: podman        # podman | docker | auto
    enabled: true                   # false = Python/Ansible locais
    image: <registry>/<imagem>:<tag>
    pull:
      policy: missing               # always | missing | never | tag
      arguments:
        - "--tls-verify=false"      # só laboratório
  mode: stdout                      # interactive (padrão) | stdout
  playbook-artifact:
    enable: false                   # obrigatório desligar para prompts de senha
```

| Chave | Opção de linha de comando |
|-------|---------------------------|
| `execution-environment.image` | `--eei` |
| `execution-environment.pull.policy` | `--pp` |
| `execution-environment.container-engine` | `--ce` |
| `execution-environment.enabled` | `--ee` |
| `mode` | `-m` / `--mode` |
| `playbook-artifact.enable` | `--pae` |

## VS Code × terminal

Menu *Run playbook via 'ansible-navigator run'* → configurações da **extensão Ansible**.
Terminal `ansible-navigator run` → **`ansible-navigator.yml`**. Mantenha iguais.

---
[← Comandos](comandos-ansible.md) | [Índice geral](../README.md) | [Troubleshooting →](troubleshooting.md)
