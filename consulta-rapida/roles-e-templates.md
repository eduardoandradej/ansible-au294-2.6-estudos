# Roles e templates

Cobertura: **templates Jinja2 e filtros** (Capítulo 5) e **roles** (Capítulo 7).
Lições: [5.3](../capitulos/05-deploy-de-arquivos/5.3-templates-jinja2-e-filtros.md),
[7.1](../capitulos/07-roles-e-collections/7.1-definindo-a-estrutura-de-roles.md),
[7.3](../capitulos/07-roles-e-collections/7.3-criando-roles.md),
[7.5](../capitulos/07-roles-e-collections/7.5-implantando-roles-de-fontes-externas.md).

## Roles (Cap. 7)

| Subdiretório | Conteúdo |
|--------------|----------|
| `tasks/main.yml` | Tasks principais |
| `handlers/main.yml` | Handlers |
| `defaults/main.yml` | Valores padrão (precedência **mínima**) |
| `vars/main.yml` | Variáveis internas (precedência **alta**) |
| `files/` · `templates/` | Arquivos estáticos · templates (`src` relativo à role) |
| `meta/main.yml` | `galaxy_info` e `dependencies` (`allow_duplicates`) |
| `tests/` · `README.md` | Testes · documentação |

| Uso no play | Comportamento |
|-------------|---------------|
| Seção `roles` | Roda **antes** de `tasks`; parâmetros na entrada vencem todas as fontes; mesma role + mesmos parâmetros = uma vez |
| `ansible.builtin.import_role` | Estático; `defaults`, `vars` e handlers visíveis para todo o play |
| `ansible.builtin.include_role` | Dinâmico; variáveis não expostas ao resto do play |

Ordem do play: `pre_tasks` → handlers → `roles` → `tasks` → handlers → `post_tasks` → handlers.

```bash
ansible-galaxy role init roles/<role>
ansible-galaxy role install -r roles/requirements.yml -p roles
ansible-galaxy role list
ansible-galaxy role remove <role>
```

```yaml
---
# roles/requirements.yml
- src: https://git.example.net/infra/ansible-role-x.git
  scm: git
  version: "1.0.0"
  name: x
- src: file:///srv/roles/y.tar
  name: y
```

Busca de roles: `roles/` do playbook → `roles_path` → diretório do playbook.

## Templates Jinja2

| Elemento | Sintaxe |
|----------|---------|
| Valor / expressão | `{{ variavel }}` · `{{ porta + 10 }}` |
| Comentário (não vai para o arquivo) | `{# texto #}` |
| Loop | `{% for x in lista %}` … `{% endfor %}` |
| Loop filtrado | `{% for u in usuarios if not u == "root" %}` |
| Número da iteração | `{{ loop.index }}` (começa em 1) |
| Condição | `{% if condicao %}` … `{% endif %}` |
| Inventário | `groups['grupo']` · `hostvars[host]['ansible_facts'][...]` |
| Aviso de arquivo gerenciado | `# {{ ansible_managed }}` (texto em `ansible_managed =` no `ansible.cfg`) |

## Implantar

```yaml
- name: Publicar arquivo a partir de template
  ansible.builtin.template:
    src: templates/arquivo.conf.j2   # padrão: diretório templates/ do projeto
    dest: /etc/arquivo.conf
    owner: root
    group: root
    mode: '0644'
    # validate: <comando> %s       # checar o arquivo antes de colocá-lo no lugar
```

## Filtros

| Filtro | Efeito |
|--------|--------|
| `to_json` · `to_yaml` | Estrutura → texto JSON/YAML |
| `to_nice_json` · `to_nice_yaml` | Idem, legível |
| `from_json` · `from_yaml` | Texto JSON/YAML → estrutura |
| `lower` | Minúsculas |
| `default('x')` | Valor alternativo se a variável não estiver definida |

Loops e condicionais Jinja2 (`{% %}`) são para **templates**; nos playbooks use
`loop` e `when`.

---
[Índice geral](../README.md)
