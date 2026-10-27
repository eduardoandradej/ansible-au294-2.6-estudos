# Sobre o curso

| Campo | Valor (verificado no PDF p. 1–8) |
|-------|----------------------------------|
| Título | Red Hat Enterprise Linux Automation with Ansible |
| Código | AU294 |
| Produto | Red Hat Ansible Automation Platform 2.6 |
| Material | Student Workbook, edição 2 (data da edição 2026-09-09; publicação 2026-08-27) |
| Identificador do material | `AU294-RHAAP2.6-en-2-20260909` |
| Páginas | 615 |
| Plataforma gerenciada | RHEL 10 · ansible-core 2.16 (citado no Capítulo 1) |

## O que o curso promete

Usar o Ansible para automatizar provisionamento, configuração, deploy de aplicações
e orquestração. O aluno instala e configura as ferramentas de desenvolvimento e as
usa para escrever e executar playbooks que automatizam tarefas comuns de
administração Linux.

Objetivos oficiais, reescritos com palavras próprias:

1. **Ambiente profissional de desenvolvimento:** development tools, VS Code com as extensões do Ansible, Git e automation execution environments, para criar e testar conteúdo de forma consistente.
2. **Playbooks bem estruturados:** sintaxe YAML, lógica condicional, loops, handlers e tratamento de erros, incluindo diagnóstico.
3. **Reutilização e escala:** roles e conteúdo curado de Ansible Content Collections.
4. **Administração de RHEL 10:** storage, usuários, rede e processos agendados com as RHEL System Roles suportadas.
5. **Segurança dos fluxos:** precedência de variáveis, proteção de dados sensíveis com Ansible Vault e host patterns para mirar exatamente os hosts certos.

## Público

Administradores Linux, engenheiros DevOps e SRE, engenheiros de automação de
infraestrutura e desenvolvedores responsáveis por gerência de configuração, deploy
repetível, provisionamento de ambientes e integração com pipelines CI/CD.

## Pré-requisito oficial

Certificação **RHCSA (EX200)** ou conhecimento equivalente de RHEL. Este
repositório faz pontes com tarefas de RHCSA (usuários, `sudo`, serviços, storage,
rede) sempre que ajudam a entender a automação.

## Estrutura oficial

| Cap. | Título original | Tema |
|------|-----------------|------|
| 1 | An Introduction to Ansible | Conceitos, ambiente de desenvolvimento, configuração |
| 2 | Introduction to Developing Automation Content | Inventários, playbooks, múltiplos plays, troubleshooting |
| 3 | Developing Automation Content: Variables | Variáveis, facts, Ansible Vault |
| 4 | Developing Automation Content: Task Control | Loops, condicionais, handlers, falhas |
| 5 | Developing Automation Content: Deploying Files | Arquivos, templates Jinja2 e filtros |
| 6 | Developing Automation Content at Scale | Include/import, host patterns |
| 7 | Reusing Code with Ansible Roles and Content Collections | Roles e collections |
| 8 | Automating Linux Administration Tasks | System roles, software, usuários, boot, storage, rede |
| 9 | Comprehensive Review | Labs de revisão integrada |

## Convenções da apostila

A apostila usa quatro tipos de destaque: **References** (onde encontrar
documentação), **Note** (dica; ignorar não causa problema), **Important** (detalhe
fácil de perder; ignorar causa frustração, não perda de dados) e **Warning**
(ignorar provavelmente causa perda de dados). Neste repositório, os equivalentes
são 📘 (fonte externa), notas em citação e ⚠️ (alerta).

---
[← Comece aqui](README.md) | [Índice](README.md) | [Próximo: Como usar este repositório →](como-usar-este-repositorio.md)
