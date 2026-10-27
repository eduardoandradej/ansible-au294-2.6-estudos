# F4 — Primeiros comandos

> Lição autoral de fundamentos. Os comandos são usados a partir das seções
> [1.3](../capitulos/01-introducao-ansible/1.3-configurando-o-ambiente-de-desenvolvimento.md)
> e [1.5](../capitulos/01-introducao-ansible/1.5-configurando-ajustes-do-ansible.md).

## Mapa das CLIs

| Comando | Vem de | Para que serve | No curso |
|---------|--------|----------------|----------|
| `ansible-navigator` | Development tools | Executar playbooks, ver configuração, imagens e documentação **dentro de um execution environment** | **Principal** |
| `ansible-playbook` | `ansible-core` | Executar playbooks no Python local (ou dentro do EE, chamado pelo navigator) | Por baixo do navigator |
| `ansible-config` | `ansible-core` | Ver/gerar configuração (`init`, `dump`, `list`) | Cap. 1 |
| `ansible-lint` | Development tools | Verificar conteúdo contra erros e boas práticas | Desde o Cap. 1 |
| `ansible-builder` | Development tools | Construir execution environments | Citado no Cap. 1 |
| `ansible` | `ansible-core` | Executar um módulo avulso (*ad hoc*) | Cap. 2 (diagnóstico pontual) |

## Subcomandos do `ansible-navigator` que aparecem cedo

```bash
ansible-navigator --version                # versão da ferramenta
ansible-navigator images                   # imagens de EE disponíveis/baixadas
ansible-navigator config                   # configuração efetiva do Ansible (com origem)
ansible-navigator run site.yml             # executa um playbook
ansible-navigator run site.yml -m stdout   # idem, saída em texto (sem TUI)
ansible-navigator doc ansible.builtin.ping -m stdout   # documentação de um módulo
```

## Modo interativo × stdout

| Modo | Quando usar |
|------|-------------|
| `interactive` (padrão) | Explorar resultados, configuração e imagens em uma TUI (números para detalhar, `Esc` volta, `:q` sai) |
| `stdout` | Scripts, pipelines, quando o playbook pede senha, ou quando você quer a saída tradicional |

## Comandos do `ansible-core` úteis para diagnosticar (📘 fonte externa)

Quando o `ansible-core` está instalado localmente (fora do EE):

```bash
ansible --version                   # versões e "config file = ..." em uso
ansible-config dump --only-changed  # só o que foi alterado, com a origem
ansible-config list                 # todas as opções, com variável de ambiente e chave INI
```

## Fixação

1. Qual comando mostra de qual arquivo veio o valor de `remote_user`?
2. Por que o curso prefere `ansible-navigator run` a `ansible-playbook`?

<details>
<summary>Respostas</summary>

1. `ansible-navigator config` (ou, localmente, `ansible-config dump --only-changed`).
2. Porque o navigator executa dentro de um **execution environment**: as mesmas versões de `ansible-core`, Python e collections no notebook, no CI e no automation controller.

</details>

---
[← F3 Automação e idempotência](automacao-idempotencia.md) | [Índice](README.md) | [Próximo: Capítulo 1 →](../capitulos/01-introducao-ansible/README.md)
