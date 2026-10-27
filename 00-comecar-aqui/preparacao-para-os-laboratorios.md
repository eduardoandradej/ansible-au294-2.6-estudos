# Preparação para os laboratórios

Resumo autoral da seção *Performing Lab Exercises* (PDF p. 10–11).

## Tipos de atividade

| Tipo | Como é | `lab grade` |
|------|--------|-------------|
| **Guided exercise** | Prática passo a passo logo após uma seção conceitual | Não |
| **Quiz** | Verificação de conhecimento, quando a prática não é viável | Não (não usa `lab`) |
| **End-of-chapter lab** | Passos de alto nível baseados nos guided exercises do capítulo, sem cada comando; traz uma solução comentada | **Sim** |
| **Comprehensive review lab** | Ao final do curso; você recebe uma **especificação** do que entregar, sem os passos; a solução básica não cobre todos os detalhes | **Sim** |

## O comando `lab`

```bash
lab start  <atividade>   # prepara o ambiente
lab grade  <atividade>   # avalia (só labs de fim de capítulo e comprehensive review)
lab finish <atividade>   # limpa o que a atividade criou
```

| Ação | O que faz |
|------|-----------|
| `start` | Verifica os recursos necessários; pode configurar, criar recursos e checar serviços. Permite fazer qualquer atividade a qualquer momento, sem as anteriores |
| `grade` | Avalia o trabalho e lista cada critério como **PASS** ou **FAIL**. Corrija as falhas e rode de novo |
| `finish` | Remove o que foi configurado. A atividade pode ser repetida quantas vezes quiser |

Cada atividade tem um nome único no curso. O comando aceita **Tab completion**:
`lab start` + Tab duas vezes lista as atividades disponíveis.

## Rotina segura

1. Leia a lição e o bloco correspondente em `PRATICA-OFICIAL.md`.
2. `lab start <atividade>` no `workstation`, como `student`.
3. Faça a atividade **digitando**, não colando; leia cada saída.
4. Se houver `lab grade`, rode-o e só depois consulte a solução.
5. `lab finish <atividade>` **sempre**, para não contaminar a próxima atividade.
6. Registre no [diário](../progresso/diario-de-laboratorios.md).

## Identificadores verificados até agora

| Capítulo | Atividades |
|----------|-----------|
| 1 | `intro-devenv` (GE 1.4), `intro-configure` (GE 1.6) — sem `lab grade` |
| 2 | `develop-inventory` (GE 2.2), `develop-singleplay` (GE 2.4), `develop-multiplay` (GE 2.6), `develop-troubleshoot` (GE 2.8) — sem `lab grade`; `develop-review` (Lab 2.9) — **com** `lab grade` |
| 3 | `variables-vars` (GE 3.2), `variables-facts` (GE 3.4), `variables-vault` (GE 3.6) — sem `lab grade`; `variables-review` (Lab 3.7) — **com** `lab grade` |
| 4 | `control-flow` (GE 4.2), `control-handlers` (GE 4.4), `control-errors` (GE 4.6) — sem `lab grade`; `control-review` (Lab 4.7) — **com** `lab grade` |
| 5 | `files-manage` (GE 5.2), `files-templates` (GE 5.4) — sem `lab grade`; `files-review` (Lab 5.5) — **com** `lab grade` |
| 6 | `scale-files` (GE 6.2), `scale-hosts` (GE 6.4) — sem `lab grade`; `scale-review` (Lab 6.5) — **com** `lab grade` |
| 7–9 | ⏳ Aguardando PDF |

---
[← Ambiente oficial](ambiente-oficial.md) | [Índice](README.md) | [Próximo: Fundamentos essenciais →](../01-fundamentos-essenciais/README.md)
