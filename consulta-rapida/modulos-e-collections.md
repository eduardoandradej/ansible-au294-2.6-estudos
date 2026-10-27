# Módulos e collections

Cobertura atual: **Capítulos 1 a 3**. O Capítulo 7 aprofunda collections.

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
| `community.postgresql.postgresql_user` | Usuários do PostgreSQL (collection da comunidade; o PDF o cita como `ansible.builtin`) | 3.5 |
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
ansible-navigator doc ansible.builtin.user -s -m stdout  # snippet de task
ansible-navigator collections                            # TUI por collection
```

⏳ Seções sobre instalação de collections, `requirements.yml` e conteúdo certificado
serão adicionadas com o Capítulo 7.

---
[Índice geral](../README.md)
