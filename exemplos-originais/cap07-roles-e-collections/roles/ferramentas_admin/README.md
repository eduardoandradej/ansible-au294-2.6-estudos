# ferramentas_admin

Role autoral (AU294, Cap. 7). Instala pacotes de administração e publica
`/etc/profile.d/admin.sh`.

| Variável | Padrão | Uso |
|----------|--------|-----|
| `ferramentas_admin_pacotes` | `tmux`, `vim-enhanced`, `bash-completion` | Pacotes instalados |
| `ferramentas_admin_historico` | `5000` | Valor de `HISTSIZE` |
| `ferramentas_admin_responsavel` | `Equipe de Plataforma` | Texto do cabeçalho do perfil |

Sem dependências. Exemplo de uso:

```yaml
- name: Preparar as estações
  hosts: estacoes_admin
  become: true
  roles:
    - role: ferramentas_admin
      ferramentas_admin_historico: 10000
```
