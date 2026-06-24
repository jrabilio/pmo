# PMO NTICS : painel mensal (estrutura leve)

Pacote pronto para o GitHub Pages. A casca pesa 109 KB (antes eram 1.951 KB). As 14 fotos saíram para `assets/` e nunca mais recarregam na sua sessão. Os dados do mês ficam isolados em `dados/`.

## Estrutura

- `index.html` : a casca (estrutura, CSS, lógica, motor do Plano B). Quase nunca muda.
- `dados/junho.js` : o mês de junho. Define `window.BASELINE` (o plano congelado) e `window.DET` (o vivo). É o único arquivo que muda no dia a dia.
- `assets/` : as 14 fotos dos coordenadores (uma vez só, sem duplicar).
- `Clareza_da_Semana___22_06_a_28_06_2026.html` : o infográfico semanal, aberto pelo Hands On em página própria.

Importante: por ser multi-arquivo, isto NÃO renderiza no preview do chat. Renderiza servido pelo GitHub Pages, ou abrindo `index.html` com a pasta inteira ao lado.

## Como publicar no GitHub Pages

Opção mais simples (interface web): no repositório jrabilio.github.io, use "Add file > Upload files", arraste a pasta inteira (index.html, dados/, assets/ e o Clareza), e faça o commit. O Pages publica em alguns segundos.

Opção por git (mais leve ainda): copie estes arquivos para a pasta local do repositório e rode `git add .`, `git commit -m "painel mensal leve"`, `git push`.

## Workflow mensal (isolar o mês, integrar ao anual)

Cada mês é um arquivo de dados independente. O anual consolidado (o Gantt de 12 meses) vive na casca e não depende do mês corrente.

Para virar para julho:
1. Gere `dados/julho.js` no mesmo formato de `dados/junho.js` (window.BASELINE + window.DET), a partir do pull ao vivo do ClickUp.
2. No `index.html`, troque `<script src="dados/junho.js">` por `<script src="dados/julho.js">`.
3. Pronto. A casca não muda.

## Como funciona o baseline (Plano B)

`window.BASELINE` é o plano congelado do mês. Ele NÃO muda ao longo do mês.

- Refresh (durante o mês): atualize só `window.DET` com uma chamada `filter_tasks` (folder 90115187061, due_date do mês, subtasks=false, include_closed=true, order_by=due_date). O desvio (escorregou, concluída, saiu do plano) aparece comparando o DET novo contra o BASELINE intacto.
- Congelar de novo (só na reunião de portfólio): copie o `window.DET` atual para dentro de `window.BASELINE`.

O baseline de junho aqui é o teste de mecanismo (5.7). O primeiro baseline de verdade será o de julho, congelado na reunião.

## Pendência única para endurecer o motor

A chave da tarefa-mãe ainda é sintética (projeto + nome). Quando o pull de julho trouxer o id real do ClickUp, troque a origem da chave (em `detKey`, na casca, e na geração do baseline) para o id. O resto do motor já está pronto.
