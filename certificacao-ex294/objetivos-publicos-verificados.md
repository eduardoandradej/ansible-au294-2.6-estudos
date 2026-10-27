# EX294 — objetivos públicos verificados

**Status:** 🟡 parcial — lista oficial de objetivos **ainda não conferida**.

## O que foi verificado (2026-10-27)

| Fato | Fonte | Situação |
|------|-------|----------|
| O AU294 cita como pré-requisito a RHCSA (EX200) ou conhecimento equivalente | Apostila, PDF p. 8 | ✅ verificado no PDF |
| O AU294 2.6 é baseado em RHEL 10, ansible-core 2.16 e development tools, alinhado ao AAP 2.5 e 2.6 | 📘 Anúncio do curso no Red Hat Learning Community (resultado de busca) | 🟡 visto apenas no resumo da busca |
| A página oficial do EX294 descreve o exame como *Advanced System Administrator in Ansible*, que conta para as credenciais *Red Hat Certified Engineer in Ansible* e *Red Hat Certified Architect in Ansible* | 📘 Página do exame (resultado de busca) | 🟡 visto apenas no resumo da busca |
| Os objetivos do exame seguem a versão mais recente do produto | 📘 Página do exame (resultado de busca) | 🟡 visto apenas no resumo da busca |

A página oficial
(<https://www.redhat.com/en/services/training/ex294-red-hat-certified-engineer-rhce-exam-red-hat-enterprise-linux>)
**não pôde ser acessada** a partir do ambiente desta sessão (falha de DNS). Por
isso, a lista de objetivos **não** foi transcrita: seria preciso inventá-la de
memória, o que este repositório não faz.

## Nova tentativa (2026-10-27, a pedido do usuário)

| Tentativa | Resultado |
|-----------|-----------|
| Acesso direto a `www.redhat.com` e `redhat.com` | ❌ Bloqueado pela política de rede do ambiente (proxy respondeu 403) |
| Busca na web restrita a `redhat.com` | 🟡 Encontrou duas páginas oficiais do EX294 (uma com sufixo `...-red-hat-enterprise-linux-9`), mas só resumos automáticos, contraditórios sobre qual é a versão atual |
| Busca na web aberta | 🟡 Apenas sites de terceiros (guias e cursos), com listas de versões diferentes do exame |

Pistas **não verificadas** que aparecem nos resumos de busca (não usar como
objetivos oficiais):

- Uma das páginas oficiais citaria itens alinhados ao AU294 2.6, como configurar o
  `ansible-navigator` e executar playbooks em um development container.
- Resumos mencionam componentes centrais (inventários, módulos, variáveis, facts,
  loops, condicionais, plays, tratamento de falhas, arquivos de configuração, roles),
  roles e Ansible Content Collections, templates Jinja2 e Ansible Vault, e reforçam
  que o candidato deve dominar as tarefas de RHCSA.
- O exame é prático (baseado em desempenho).

Conclusão: a lista oficial **continua não conferida**. Para concluir, é preciso
liberar `www.redhat.com` na política de rede do ambiente (ou colar aqui o texto da
seção de objetivos da página oficial) e repetir a conferência.

## Próxima ação

Liberar o acesso a `www.redhat.com` (ou receber o texto oficial), conferir a página
do EX294 e registrar aqui os objetivos atuais, com a data da consulta. Depois, preencher a [matriz de competências](matriz-de-competencias.md).

---
[Índice geral](../README.md) | [Matriz de competências →](matriz-de-competencias.md)
