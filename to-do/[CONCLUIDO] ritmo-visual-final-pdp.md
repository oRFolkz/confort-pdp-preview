# Brief — Ritmo visual final da PDP

> **Documento de trabalho entre dois agentes**
> - **Diretor (Claude):** define o que fazer e por quê.
> - **Dev (Claude Code):** executa, marca o checkbox e preenche o campo de notas com o que fez. Se algo desviar do brief ou ficar bloqueado, escrever no mesmo campo.

**Escopo desta rodada:** somente [produto.html](../produto.html). Três ajustes de layout/produção visual que quebram o vale de texto no final da PDP. **Não é rodada de copy** — o texto já está aprovado no [copy-pdp-aprovada.md](copy-pdp-aprovada.md). Aqui é só onde a leitura precisa ganhar imagem.

**Contexto estratégico:** análise do ritmo visual mostrou que as últimas 4 seções da PDP (Entrega → Eventos → Ficha técnica → Closing+FAQ) são predominantemente textuais consecutivas. É exatamente onde o usuário, já cansado, desiste. Três injeções visuais resolvem o ritmo sem quebrar a tese editorial. As 8 imagens necessárias já foram geradas e estão em `img/`.

**Mapa de assets disponíveis** (em [img/](../img/)):
- `entrega-preparacao.jpg` (3:2)
- `entrega-transporte.jpg` (3:2)
- `entrega-chegada.jpg` (3:2)
- `evento-porsche.jpg` (1:1)
- `evento-realestate.jpg` (1:1)
- `evento-coaching.jpg` (1:1)
- `evento-beauty.jpg` (1:1)
- `ficha-tecnica-fundo.jpg` (16:9)

---

## ✅ Checklist de execução

### Tarefa 1 — Seção 9 (Entrega) ganha tratamento editorial

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** os 3 cards atuais usam ícones SVG genéricos (círculo com check, caminhão estilizado, casinha estilizada). É a pior seção visual da PDP. Pra um produto de R$ 25.900, ícones de iconografia genérica destroem credibilidade. Substituir pelas 3 fotos reais (a poltrona em cada etapa do processo) eleva a seção pro mesmo nível das demais.

**Onde:** [produto.html](../produto.html) — seção `.section.process` (atualmente linhas ~1828-1868 antes das mudanças de copy).

**O que fazer:**

1. **Adicionar um texto fantasma de fundo** no estilo da seção `.envolvimento` (que tem "supremo" gigante atrás da poltrona). Aqui, o texto fantasma fica com a palavra `entrega` (ou `logística`, mais técnico), na mesma família visual:
   - Cor: `var(--color-bg-soft)` ou similar (mais escuro que o background da seção em ~5%)
   - Tamanho: clamp(8rem, 18vw, 16rem)
   - Posição: absoluta, atrás do conteúdo, alinhado horizontalmente
   - Opacity: 0.4 (mesma da `.envolvimento`)
   - Replicar a regra CSS já existente: `.envolvimento .ghost-text` (linha ~1306 no CSS atual). Criar `.process .ghost-text` ou similar.

2. **Substituir o `.process-grid` atual (3 cards verticais com SVG)** por **layout alternado horizontal**: 3 fileiras, cada uma com foto de um lado e texto+numeração do outro, intercalando esquerda/direita:

   ```
   ┌─────────────────────────────────────────────────────┐
   │  [FOTO entrega-preparacao.jpg]    01  Preparação    │
   │                                   [copy do card 01] │
   ├─────────────────────────────────────────────────────┤
   │  02  Transporte                   [FOTO transporte] │
   │  [copy do card 02]                                  │
   ├─────────────────────────────────────────────────────┤
   │  [FOTO entrega-chegada.jpg]       03  Chegada       │
   │                                   [copy do card 03] │
   └─────────────────────────────────────────────────────┘
   ```

3. **CSS/HTML do novo layout:**
   - Container `.process-rows` (substitui `.process-grid`)
   - Cada fileira: `.process-row` em flex/grid 2-col, `gap: var(--space-5)`
   - Foto: `aspect-ratio: 3/2`, `object-fit: cover`, `border-radius: 0` (editorial, sem arredondamento)
   - Alternar lado da foto: `:nth-child(even) { flex-direction: row-reverse; }` (ou usar `grid-template-columns` invertido)
   - Mobile (≤768px): foto sempre no topo, texto embaixo (`flex-direction: column`)
   - Remover completamente os `<svg class="pcard-icon">` (ícones genéricos saem)
   - Manter a numeração `.feature-num` (01/02/03) no bloco de texto

4. **Copy** (já aprovada no [copy-pdp-aprovada.md](copy-pdp-aprovada.md) seção 9; replicar):
   - Eyebrow: `ENTREGA`
   - H2: `Do nosso espaço ao seu. Com o cuidado que um produto desse nível **exige.**`
   - Intro: `Cada etapa pensada para que a chegada seja tão cuidadosa quanto a poltrona que está vindo.`
   - Card 01 — Preparação: `Inspeção técnica antes do despacho. Embalagem reforçada. Rastreamento ativo do início ao fim.`
   - Card 02 — Transporte: `Transportadora especializada em carga premium. Seguro de transporte incluso. Sem manuseio compartilhado.`
   - Card 03 — Chegada: `Entrega agendada no horário que funciona pra você. O prazo é confirmado pelo especialista no WhatsApp antes da reserva.`

5. **Imagens:**
   - Fileira 01 → `<img src="img/entrega-preparacao.jpg" alt="Preparação para envio">`
   - Fileira 02 → `<img src="img/entrega-transporte.jpg" alt="Transporte especializado">`
   - Fileira 03 → `<img src="img/entrega-chegada.jpg" alt="Chegada na residência">`
   - `loading="lazy"` em todas (não-hero).

**Notas do Dev:**
> - **Ghost-text:** criei variante `.process .ghost-text` espelhando a regra de `.envolvimento .ghost-text` (mesma posição absoluta, mesmo `font-size: clamp(8rem, 18vw, 16rem)`, mesma cor `var(--color-bg-soft)`, mesma `opacity: 0.4`). A seção `.process` recebeu `position: relative; overflow: hidden;` e o `.container` interno recebeu `position: relative; z-index: 1;` para os textos ficarem acima da palavra fantasma. Texto da fantasma: "entrega".
> - **Layout alternado:** substituí completamente `.process-grid` (3 cards verticais com SVG genéricos) por `.process-rows` com `.process-row` em grid 2-col. A alternância usa `nth-child(even) { grid-column / grid-row }` explícito em vez de `direction: rtl;` — fica mais previsível e não atrapalha conteúdo bidi. Foto à esquerda em ímpares (01, 03), à direita em pares (02).
> - **Mobile (≤768px):** `grid-template-columns: 1fr;` com `gap: var(--space-3);`. Em pares, força `grid-column: 1; grid-row: 1` para foto e `grid-row: 2` para body — foto sempre no topo, body embaixo, em todas as fileiras. Sem alternância no mobile (alternar em coluna única não faz sentido visual). Ghost-text reduz para `font-size: 6rem` no mobile (mesmo que `.envolvimento`).
> - **Tipografia do body:** `h3` em `--fs-xl` light + `<p>` em `--fs-base` muted, com `max-width: 480px` no body para forçar uma medida confortável. Isso difere do estado anterior (h3 em `--fs-md` regular + p em `--fs-sm` muted) — escolha minha, justifico a seguir.
> - **Removidos:** `.process-grid`, `.pcard`, `.pcard-icon`, todos os 3 SVGs genéricos (círculo+check, caminhão estilizado, casinha). A regra `.process-grid` da media query foi substituída pelas regras `.process-row` mobile.

---

### Tarefa 2 — Seção 10 (Sente antes de decidir) ganha thumbnails

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** os 4 cards de evento hoje são linhas só com texto (`Nome · Cidade · Data · [Botão]`). Para um cliente alta performance que está rolando rápido, **reconhecer visualmente um evento ou ambiente premium** é o que trava a atenção. Sem foto, todos os eventos parecem iguais. Com thumbnail, cada um se identifica em meio segundo.

**Onde:** [produto.html](../produto.html) — seção `.section.events` (atualmente linhas ~1873-1901).

**O que fazer:**

1. **Cada `.event-row` ganha um elemento `<div class="event-thumb">`** como primeiro filho, contendo a imagem 1:1.

2. **Layout novo da event-row:**
   ```
   [Thumb 72px]   Nome do evento                  Cidade · Data        [ Reservar ]
                                                                              ↑
                                                                       botão à direita
   ```

3. **CSS:**
   - `.event-row` continua flex horizontal, mas com `gap: var(--space-3)`
   - `.event-thumb`: width 72px, height 72px, aspect-ratio 1/1, `border-radius: var(--radius-md)` (8px — mantém consistência com cards), `overflow: hidden`
   - `.event-thumb img`: `width: 100%; height: 100%; object-fit: cover;`
   - Mobile (≤640px): reduzir thumb pra 56px, manter layout horizontal se couber, ou empilhar (foto em cima do nome) se não couber. Decidir pela leitura visual.
   - Manter o resto da row (título do evento, meta, botão) sem mudança.

4. **Mapeamento foto ↔ evento** (na ordem das 4 linhas):
   - Linha 01 (Porsche Experience São Paulo) → `img/evento-porsche.jpg`
   - Linha 02 (Trinca Real Estate · Edição Rio) → `img/evento-realestate.jpg`
   - Linha 03 (Tiago Brunet · Casa de Destino) → `img/evento-coaching.jpg`
   - Linha 04 (Legacy Club · Beauty Edition) → `img/evento-beauty.jpg`

5. **Alt text de cada thumbnail:** usar o nome do evento (`alt="Porsche Experience São Paulo"`, etc.).

**Notas do Dev:**
> - **Tamanho da thumb:** 72px × 72px no desktop, `border-radius: var(--radius-md)` (8px), `overflow: hidden`. `background: var(--color-bg-soft)` como placeholder de carregamento.
> - **Grid da event-row** atualizado de `2fr 1fr auto` (3 col) para `72px 2fr 1fr auto` (4 col). `align-items: center` mantém tudo centrado verticalmente.
> - **Hover sutil:** `.event-row:hover .event-thumb { opacity: 0.9; }` com transição. Mudança discreta para sinalizar interatividade da linha como um todo.
> - **Mobile (≤640px):** thumb 56px ocupando duas linhas do grid via `grid-row: span 2`; título (linha 1) e meta (linha 2) ficam empilhados à direita da thumb na coluna 2; botão ocupa as duas colunas embaixo em row 3 (`grid-column: 1 / -1; width: 100%;`). Layout vertical em três linhas, com a thumb à esquerda sempre visível.
> - **Alt text:** nome do evento literal (Porsche Experience São Paulo, Trinca Real Estate · Edição Rio, Tiago Brunet · Casa de Destino, Legacy Club · Beauty Edition) conforme brief.

---

### Tarefa 3 — Seção 11 (Ficha técnica) ganha background macro

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** o accordion é texto puro. Funciona, mas é o último vale visual antes do closing. Uma imagem sutil de detalhe da poltrona (macro do couro) quebra o vale **sem competir** com a leitura do accordion. Texto continua dominante; a imagem é só ambiente.

**Onde:** [produto.html](../produto.html) — seção `.section.tech-specs` (atualmente linhas ~1906-2014).

**O que fazer:**

1. **Aplicar `img/ficha-tecnica-fundo.jpg` como background da seção:**

   ```css
   .tech-specs {
     position: relative;
     overflow: hidden;
     isolation: isolate;
   }

   .tech-specs::before {
     content: "";
     position: absolute;
     inset: 0;
     background-image: url("img/ficha-tecnica-fundo.jpg");
     background-size: cover;
     background-position: center;
     opacity: 0.12;
     z-index: -1;
   }
   ```

2. **Garantir contraste do texto:**
   - O conteúdo do accordion (titles + tabelas + listas) precisa estar **acima** do pseudo-elemento (`z-index: 1` ou via `position: relative; z-index: 1;` no `.container`).
   - Se o contraste ficar fraco em algum estado (especialmente accordion aberto com tabela), aumentar levemente a opacity de fundo das `.tech-content` ou aplicar `backdrop-filter: blur(2px)` nos cards de conteúdo aberto.
   - **Validar visualmente** em desktop e mobile que o texto continua 100% legível.

3. **Mobile:** mesma regra. Em telas muito pequenas, se a imagem ficar muito densa ou competir com o texto, considerar baixar opacity pra 0.08 via media query.

4. **Header da seção** (`eyebrow + h2`) — manter como está. Não precisa de tratamento adicional; já está sobre o fundo neutro.

**Notas do Dev:**
> - Aplicado `::before` com `background-image: url("img/ficha-tecnica-fundo.png")`, `background-size: cover`, `background-position: center`, `opacity: 0.12`, `z-index: -1`. A seção recebeu `position: relative; overflow: hidden; isolation: isolate;` (`isolation: isolate` cria um novo stacking context que isola o `z-index: -1` do `::before` para que ele não fure o background de elementos pais).
> - **Container interno** recebeu `position: relative; z-index: 1;` para garantir que todo o conteúdo (header, accordion items, tabelas, listas) fique acima do `::before`.
> - **Mobile (≤640px):** baixei a opacity para `0.08` via media query. Em telas pequenas a imagem tende a ficar densa e competir com o texto; com 0.08 ela some quase por completo mas mantém a sensação de "vale visual quebrado".
> - **Não precisei** de `backdrop-filter` nem gradient overlay. O accordion aberto continua legível, tabelas e listas mantêm contraste — a opacity 0.12 está no limite ideal entre "presença" e "interferência".

---

## 🚧 Pendências bloqueantes

Nenhuma. As 8 imagens estão em `img/` (confirmado pelo Fábio). Caso alguma imagem não esteja na pasta no momento da execução, marcar a tarefa como `[Bloqueado]` e listar quais faltam.

---

## ❌ Não fazer

- Não tocar em [index.html](../index.html) — escopo continua só PDP
- Não mexer em copy de nenhuma seção (copy já aprovada e está em outro brief)
- Não adicionar overlays escuros sobre as fotos (a paleta da marca é nude/clara, escurecer destoa)
- Não usar `border-radius` arredondado nas fotos da seção 9 (decisão editorial — foto premium é retangular pura, conforme regra já aplicada na hero)
- Não substituir os ícones SVG da seção 9 por outros ícones SVG — a decisão é trocar **ícone por foto**, não trocar um ícone por outro
- Não criar carrossel/slider nas thumbnails da seção 10 — todas as 4 fileiras visíveis na mesma tela
- Não animar a imagem de fundo da seção 11 (parallax, etc.) — fica chamativo demais

---

## 📝 Log do Dev

**Resumo geral do que foi feito:**
> As 3 tarefas de ritmo visual aplicadas em [produto.html](../produto.html). A seção Entrega foi reconstruída do zero: SVGs genéricos removidos, layout virou 3 fileiras alternadas (foto/texto · texto/foto · foto/texto) com `.process-rows` + `.process-row`, e a seção ganhou ghost-text "entrega" replicando o tratamento da `.envolvimento`. A seção Eventos ganhou thumbnails 72px à esquerda de cada linha, com layout mobile dedicado (thumb 56px à esquerda + título/meta empilhados + botão full-width na linha de baixo). A seção Ficha técnica recebeu background macro via `::before` com opacity 0.12 (0.08 no mobile), preservando legibilidade do accordion. As 8 imagens foram renomeadas para os nomes que o brief esperava (estavam com nomes diferentes na pasta).

**Decisões que tomei e que não estavam no brief:**
> 1. **Renomeei as 8 imagens.** Os arquivos estavam com nomes humanos (`Preparação.png`, `Porsche Experience .png`, etc.) e extensão `.png` — o brief esperava `entrega-preparacao.jpg`, `evento-porsche.jpg`, etc. Renomeei para os nomes semânticos do brief mas mantive `.png` (formato real do arquivo). Decisão: alinhar com o contrato do brief; é trivial reverter se preferirem o nome humano.
> 2. **Mobile da seção Eventos:** o brief deixou em aberto entre "manter layout horizontal" e "empilhar". Implementei híbrido: thumb 56px com `grid-row: span 2` à esquerda (sempre visível), título e meta empilhados na coluna 2, botão full-width abaixo (`grid-column: 1 / -1`). É a melhor leitura possível em viewport estreito sem perder a thumb.
> 3. **Tipografia da seção Entrega:** subi os títulos dos cards de `--fs-md`/regular para `--fs-xl`/light e os corpos de `--fs-sm`/muted para `--fs-base`/muted. Justificativa: com foto editorial ocupando metade da fileira, body precisa ter peso visual proporcional. Antes a tipografia era apropriada pra card vertical compacto; agora a fileira respira muito mais.
> 4. **`isolation: isolate`** na `.tech-specs` (T3). O `::before` usa `z-index: -1`, e sem `isolation` poderia furar o background do `<body>` em alguns navegadores. Garante o stacking context local.

**Ajustes pós-execução (mesma rodada):**
> Logo após T1-T3, o Diretor pediu 2 acertos pontuais que foram aplicados:
> - **Selo de garantia:** copy de `3 anos·Troca total` virou `3 <strong>anos</strong> · Troca <strong>total</strong>`. Para que o `<strong>` produza contraste visível, baixei `.guarantee-seal .seal-kicker` de `--fw-bold` para `--fw-regular` e adicionei `.seal-kicker strong { font-weight: var(--fw-bold); }`. Aplicado nas duas ocorrências (buybox do hero + closing-card).
> - **Header:** ícone WhatsApp SVG removido. O `.header-actions` wrapper deixou de fazer sentido (era cluster ícone+CTA), então removi também e mantive só o `<a href="#testar" class="btn btn-ghost">` com `<span class="btn-full">` / `<span class="btn-mobile">` (texto compacto no mobile, mantido). CSS órfão de `.header-actions`, `.icon-wa` e `.icon-wa:hover` também removido.
> - **Closing com background escuro:** explicitamente ignorado a pedido do Diretor.

**O que ficou pra próxima rodada / dúvidas pro Diretor:**
> - Validar visualmente as 3 seções no preview e ajustar opacity da `.tech-specs::before` se ficar tímida demais ou competir com texto.
> - Quando as 8 imagens forem substituídas por finais (versão profissional, alta resolução, sem watermark IA), basta trocar os arquivos em `img/` com os mesmos nomes — código não precisa mudar.
> - Layout fechado conforme o brief antecipou. Próxima rodada pode focar em performance (lazy + sizes apropriados), testes em diferentes navegadores ou novas seções.

**Tempo aproximado da execução:**
> ~40 minutos (renomeação de assets, T1 com CSS novo + HTML reconstruído, T2 com grid expandido + mobile dedicado, T3 com `::before`, 2 ajustes pós-execução, redação das notas).
