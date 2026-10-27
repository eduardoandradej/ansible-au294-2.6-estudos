# Módulos e collections

Cobertura atual: **Capítulo 1** (conceitos). O Capítulo 7 aprofunda collections.

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
| `ansible.builtin.debug` | Imprime mensagens/valores na saída | GE 1.4, projeto-base |

## Consultar documentação de um módulo

```bash
ansible-navigator doc ansible.builtin.ping -m stdout
```

⏳ Seções sobre instalação de collections, `requirements.yml` e conteúdo certificado
serão adicionadas com o Capítulo 7.

---
[Índice geral](../README.md)
