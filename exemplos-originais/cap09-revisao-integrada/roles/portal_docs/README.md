# portal_docs

Role autoral (AU294, Cap. 9). Instala nginx e firewalld, publica uma página gerada
por template e abre a porta configurada no firewall. O rótulo SELinux da porta fica
a cargo do play (system role `redhat.rhel_system_roles.selinux`).

| Variável | Padrão | Uso |
|----------|--------|-----|
| `portal_docs_pacotes` | `nginx`, `firewalld` | Pacotes instalados |
| `portal_docs_porta` | `8080` | Porta do site |
| `portal_docs_raiz` | `/srv/portal` | Diretório publicado |
| `portal_docs_titulo` | `Portal de documentação` | Título da página |
| `portal_docs_secoes` | `[]` | Lista de seções exibidas |

Requer a collection `ansible.posix`. Sem dependências de roles.
