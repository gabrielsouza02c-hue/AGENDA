# Ficha de treino — Meso 1

App de treino de página única. Abre no celular, funciona offline, salva tudo no
próprio aparelho (`localStorage`). Não tem servidor, não tem build, não manda
dado para lugar nenhum.

**Repositório privado**: o arquivo contém histórico de saúde pessoal — cirurgia,
pesagens, medidas e cargas. Não tornar público sem antes remover os blocos
`SEED_SESSIONS` e `SEED_BODY`.

## Como usar

Abre o `index.html` no navegador do celular e adiciona à tela de início. Ele abre
em tela cheia, com ícone próprio.

## O que tem dentro

| Aba | O que faz |
|---|---|
| **Treino** | Abre no treino do dia. Carga e reps editáveis por série, timer de descanso, gerador de registro em texto. |
| **Histórico** | Curva de carga por exercício, variação em kg e %, tabela de todas as sessões. |
| **Corpo** | Simetria de quadríceps (perna operada / perna sã), marcos da reabilitação com contagem regressiva, gráficos de peso e cintura. |
| **Dieta** | Contador de proteína do dia contra a meta, com refeições de toque rápido. |

## Estrutura do mesociclo

Cinco treinos, segunda a sexta, mais dois de viagem sem equipamento:

- **P1** (seg) — Perna 1: extensores e core
- **B** (ter) — Empurrar: peito superior, ombro, tríceps
- **A** (qua) — Puxar: espessura de costas, bíceps, posterior
- **P2** (qui) — Perna 2: flexores, unilateral e core
- **U** (sex) — Upper misto: segunda dose de peito e costas
- **H1 / H2** — versões de hotel, só peso corporal e mochila

## Como o código está organizado

Tudo em um arquivo só, sem dependências externas. Dentro do `<script>`:

- `WORKOUTS` — a definição dos treinos. É aqui que se muda exercício, faixa de
  repetições, RIR, descanso e carga prescrita.
- `coachKg` + `coachOn` — carga prescrita e a data em que foi prescrita. Ela só
  sobrescreve o que está salvo no aparelho enquanto for **mais nova** que o
  último registro. Assim uma prescrição antiga nunca apaga uma progressão nova.
- `SEED_SESSIONS` / `SEED_BODY` — histórico embutido, aplicado uma única vez por
  `SEED_REV`. Ao mudar o seed, subir a revisão.
- `bumpTarget()` — a dupla progressão: bateu o topo da faixa em todas as séries,
  sinaliza para subir a carga.
- `lineChart()` — gráficos em SVG puro, sem biblioteca.

## Regras clínicas embutidas

O aviso no topo de cada treino e as observações por exercício vêm da carta médica
de 06/08/2026. As datas de vencimento das restrições estão em `MARCOS`. Ao mudar
qualquer parâmetro de perna, conferir se ainda bate com a prescrição:
1 a 4 séries, 8 a 12 repetições, 60% a 80% de 1RM, 1 a 2 min de intervalo,
2 a 3 vezes por semana com 48 a 72h entre sessões.
