# Roles e templates

Cobertura: **templates Jinja2 e filtros** (Capítulo 5). ⏳ Roles chegam com o
Capítulo 7. Lição: [5.3](../capitulos/05-deploy-de-arquivos/5.3-templates-jinja2-e-filtros.md).

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
