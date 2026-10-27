# Módulos e collections

Cobertura atual: **Capítulos 1 a 7**.

## Conceitos já vistos

| Conceito | Resumo |
|----------|--------|
| `ansible.builtin` | Collection embutida no `ansible-core`: os módulos essenciais |
| Outras collections | Distribuídas à parte; no AAP, vêm prontas no execution environment ou são instaladas conforme a necessidade |
| FQCN | Nome completo do módulo (`ansible.builtin.ping`); recomendado pelo `ansible-lint` |

## Módulos citados até agora

| Módulo | Para que serve | Onde aparece |
|--------|----------------|--------------|
| `ansible.builtin.ping` | Testa conexão + Python no managed host (não é ICMP) | 1.1, GE 1.6, [projeto-base](../exemplos-originais/cap01-projeto-base/verificar-conectividade.yml) |
| `ansible.builtin.debug` | Imprime mensagens (`msg`) ou variáveis (`var`); `verbosity` controla quando aparece | 1.4, 2.7 |
| `ansible.builtin.setup` | Coleta facts (executado pelo `Gathering Facts`); `gather_subset`, `filter` | 2.3, 3.3 |
| `ansible.builtin.set_fact` | Cria variáveis por host durante a execução | 3.3 |
| `ansible.builtin.dnf` | Pacotes com DNF (`state: present`/`latest`/`absent`; `name` aceita lista) | 2.3, 2.5 |
| `ansible.builtin.package` | Pacotes com o gerenciador detectado no host | 2.5 |
| `ansible.builtin.copy` | Copia arquivo (`src`) ou grava conteúdo (`content`) no host | 2.3, 2.5 |
| `ansible.builtin.file` | Permissões, dono, diretórios, links | 2.5 |
| `ansible.builtin.lineinfile` | Garante (ou remove) uma linha em um arquivo | 2.5 |
| `ansible.builtin.systemd_service` / `ansible.builtin.service` | Estado e habilitação de serviços | 2.3, 2.5 |
| `ansible.builtin.user` | Contas de usuário | 2.3, 2.5 |
| `ansible.builtin.uri` / `ansible.builtin.get_url` | Requisições HTTP / download de arquivos | 2.5 |
| `ansible.builtin.wait_for` | Aguarda porta/arquivo/condição | exemplo do Cap. 2 |
| `ansible.builtin.reboot` | Reinicia o host e espera voltar | 2.5 |
| `ansible.builtin.command` / `shell` / `raw` | Comandos arbitrários (evitar; `creates`/`removes`) | 2.5 |
| `ansible.builtin.import_playbook` | Importa plays de outro playbook (nível superior) | 6.1 |
| `ansible.builtin.import_tasks` | Importa tasks (estático) | 6.1 |
| `ansible.builtin.include_tasks` | Inclui tasks (dinâmico) | 6.1 |
| `ansible.builtin.import_role` | Importa uma role como task (estático) | 7.1, 7.3 |
| `ansible.builtin.include_role` | Inclui uma role como task (dinâmico) | 7.1, 7.3, 7.7 |
| `ansible.builtin.template` | Publica arquivo gerado de um template Jinja2 | 5.3 |
| `ansible.builtin.fetch` | Traz arquivos dos hosts para o control node (`flat`) | 5.1 |
| `ansible.builtin.blockinfile` | Bloco de várias linhas com marcadores | 5.1 |
| `ansible.builtin.stat` | Estado e atributos de um arquivo (`['stat']`) | 5.1 |
| `ansible.builtin.find` | Procura arquivos por critérios (`['files']`) | 5.1 |
| `ansible.builtin.fail` | Falha a task com uma mensagem (com `when`) | 4.5 |
| `ansible.builtin.meta` | Ações internas, como `flush_handlers` | 4.3 |
| `ansible.builtin.service_facts` | Coleta o estado dos serviços em `ansible_facts['services']` | 4.1 |
| `ansible.builtin.group` | Grupos locais | exemplos do Cap. 4 |
| `ansible.posix.firewalld` | Regras do firewalld (`permanent`, `immediate`) | 2.3, 2.5 |
| `ansible.posix.synchronize` | Sincroniza conteúdo com rsync | 2.5 |

## Onde obter collections

| Fonte | Suporte |
|-------|---------|
| `ansible.builtin` (no `ansible-core`) | Sempre disponível |
| EE `ee-supported-rhel9` | Inclui várias collections além de `ansible.builtin` |
| Automation hub (console.redhat.com) | Collections certificadas, com suporte Red Hat |
| Private automation hub | Curadoria da organização |
| Ansible Galaxy | Comunidade, sem suporte formal da Red Hat |

## Consultar documentação de módulos

```bash
ansible-navigator doc -l -m stdout                       # lista
ansible-navigator doc ansible.builtin.user -m stdout     # documentação + EXAMPLES
ansible-navigator -s doc ansible.builtin.user           # snippet de task
ansible-navigator collections                            # TUI por collection
```

## Instalar e usar collections (Cap. 7)

Lição: [7.7](../capitulos/07-roles-e-collections/7.7-roles-e-modulos-de-collections.md).

```ini
[defaults]
collections_path = ./collections:/usr/share/ansible/collections
```

```yaml
---
# collections/requirements.yml
collections:
  - name: community.crypto
  - name: ansible.posix
    version: 1.5.4
  - name: /tmp/exemplo-colecao-1.0.0.tar.gz
  - name: git+https://git.example.net/infra/colecao.git
    version: main
```

```bash
ansible-galaxy collection install -r collections/requirements.yml -p collections
ansible-galaxy collection list
ansible-navigator collections list
```

| Regra | Detalhe |
|-------|---------|
| Nomes | FQCN `ns.colecao` · FQMN `ns.colecao.modulo` · FQRN `ns.colecao.role` |
| Ordem do `collections_path` | Primeiro encontrado vence (projeto antes da imagem) |
| Sem `-p` nem `collections_path` | Vai para `~/.ansible/collections`, fora do EE |
| Fontes no `ansible.cfg` | `[galaxy] server_list` + `[galaxy_server.<id>]` (`url`, `auth_url`) |
| Token do hub | `ANSIBLE_GALAXY_SERVER_<ID>_TOKEN`, nunca no arquivo versionado |
| Role de collection | `include_role`/`import_role` com FQRN, não a seção `roles` |
| Produção | EE customizado (`ansible-builder`) com as collections embutidas |

---
[Índice geral](../README.md)
