# Projeto-base do Capítulo 1

Projeto mínimo que materializa as seções
[1.1](../../capitulos/01-introducao-ansible/1.1-automatizando-tarefas-com-ansible.md) e
[1.5](../../capitulos/01-introducao-ansible/1.5-configurando-ajustes-do-ansible.md).

| Arquivo | Papel |
|---------|-------|
| [ansible.cfg](ansible.cfg) | Inventário, usuário remoto `automacao`, chave SSH, `become` desligado por padrão |
| [ansible-navigator.yml](ansible-navigator.yml) | Podman, imagem `ee-supported-rhel9` do AAP 2.6, pull `missing`, `stdout`, sem artefatos |
| [inventory](inventory) | Grupos `web` e `db` com hosts fictícios |
| [verificar-conectividade.yml](verificar-conectividade.yml) | `ansible.builtin.ping` + `ansible.builtin.debug` em todos os hosts, sem alterar nada |

## Executar (em um ambiente seu, com hosts reais)

```bash
ansible-navigator run verificar-conectividade.yml
```

Resultado esperado: `ok` para cada host nas duas tasks e `changed=0` no `PLAY RECAP`.
Se aparecer `unreachable`, siga o
[troubleshooting](../../consulta-rapida/troubleshooting.md#conexão-e-privilégio).

## Status

✅ Validado: YAML, leitura do `ansible.cfg`, inventário, `--syntax-check`,
`ansible-lint` (perfil *production*) e configuração do navigator.
⚠️ Não executado contra hosts.
