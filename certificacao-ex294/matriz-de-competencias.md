# Matriz de competências (curso → prática)

Relaciona as competências **trabalhadas no curso** com o material deste repositório.
A coluna de objetivos do EX294 será preenchida quando os objetivos públicos forem
verificados ([ver status](objetivos-publicos-verificados.md)).

| Competência (redação autoral) | Capítulo | Material | Objetivo EX294 |
|-------------------------------|----------|----------|----------------|
| Explicar arquitetura agentless, control node e managed hosts | 1 | [1.1](../capitulos/01-introducao-ansible/1.1-automatizando-tarefas-com-ansible.md) | ⏳ a verificar |
| Distinguir ansible-core, pacote comunitário e AAP; papel das collections | 1 | [1.1](../capitulos/01-introducao-ansible/1.1-automatizando-tarefas-com-ansible.md) | ⏳ a verificar |
| Preparar o ambiente de desenvolvimento (development tools, VS Code, Git) | 1 | [1.3](../capitulos/01-introducao-ansible/1.3-configurando-o-ambiente-de-desenvolvimento.md) | ⏳ a verificar |
| Configurar `ansible.cfg` (inventário, usuário remoto, escalada de privilégio) | 1 | [1.5](../capitulos/01-introducao-ansible/1.5-configurando-ajustes-do-ansible.md) | ⏳ a verificar |
| Preparar managed hosts: chave SSH e `sudo` para a conta de automação | 1 | [1.5](../capitulos/01-introducao-ansible/1.5-configurando-ajustes-do-ansible.md) | ⏳ a verificar |
| Configurar o `ansible-navigator` e execution environments | 1 | [1.5](../capitulos/01-introducao-ansible/1.5-configurando-ajustes-do-ansible.md) | ⏳ a verificar |
| Criar e consultar inventários estáticos (grupos, `:children`, ranges, variáveis de conexão) | 2 | [2.1](../capitulos/02-desenvolvendo-automacao/2.1-construindo-um-inventario.md) | ⏳ a verificar |
| Escrever e executar playbooks de um play com módulos `ansible.builtin` e de collections | 2 | [2.3](../capitulos/02-desenvolvendo-automacao/2.3-desenvolvendo-playbooks.md) | ⏳ a verificar |
| Playbooks com vários plays, `remote_user` e `become` por play; consultar `ansible-navigator doc` | 2 | [2.5](../capitulos/02-desenvolvendo-automacao/2.5-playbooks-com-multiplos-plays.md) | ⏳ a verificar |
| Diagnosticar playbooks e hosts (lint, sintaxe, verbosidade, `debug`, conexão, escalada) e usar comandos ad hoc | 2 | [2.7](../capitulos/02-desenvolvendo-automacao/2.7-troubleshooting-de-playbooks-e-hosts.md) | ⏳ a verificar |
| Definir e usar variáveis (inventário, `group_vars`/`host_vars`, `vars`/`vars_files`, `-e`) e explicar a precedência | 3 | [3.1](../capitulos/03-variaveis-e-vault/3.1-usando-variaveis.md) | ⏳ a verificar |
| Usar facts, facts customizados, `set_fact` e variáveis mágicas | 3 | [3.3](../capitulos/03-variaveis-e-vault/3.3-coletando-informacoes-com-facts.md) | ⏳ a verificar |
| Proteger dados com Ansible Vault (arquivos, valores, vault IDs) e executar playbooks com conteúdo cifrado | 3 | [3.5](../capitulos/03-variaveis-e-vault/3.5-protegendo-dados-com-ansible-vault.md) | ⏳ a verificar |
| Usar loops (`loop`, listas de dicionários, `register` com `results`) e condicionais (`when`) | 4 | [4.1](../capitulos/04-controle-de-tarefas/4.1-loops-e-tarefas-condicionais.md) | ⏳ a verificar |
| Implementar handlers e antecipá-los com `flush_handlers` | 4 | [4.3](../capitulos/04-controle-de-tarefas/4.3-implementando-handlers.md) | ⏳ a verificar |
| Tratar falhas (`ignore_errors`, `force_handlers`, `failed_when`, `changed_when`, blocos) | 4 | [4.5](../capitulos/04-controle-de-tarefas/4.5-tratando-falhas-de-tarefas.md) | ⏳ a verificar |
| Arquivos e templates Jinja2 | 5 | ⏳ Aguardando PDF | ⏳ |
| Include/import e host patterns | 6 | ⏳ Aguardando PDF | ⏳ |
| Roles e collections | 7 | ⏳ Aguardando PDF | ⏳ |
| Administração de RHEL e system roles | 8 | ⏳ Aguardando PDF | ⏳ |

---
[← Objetivos públicos](objetivos-publicos-verificados.md) | [Índice geral](../README.md) | [Roteiro de revisão →](roteiro-de-revisao.md)
