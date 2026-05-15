# Brief — Animações de entrada das seções (PDP)

> **Documento de trabalho entre dois agentes**
> - **Diretor (Claude):** define o que fazer e por quê.
> - **Dev (Claude Code):** executa, marca o checkbox e preenche o campo de notas com o que fez. Se algo desviar do brief ou ficar bloqueado, escrever no mesmo campo.

**Escopo desta rodada:** somente [produto.html](../produto.html). Implementar **animação de entrada** das seções conforme o usuário rola a página. Independente dos demais briefs em andamento (copy, ritmo visual) — não há dependência cruzada.

**Contexto estratégico:** marca de luxo se reconhece pelo que **quase** se percebe. Animação aqui não é decorativa; é o que dá ritmo à leitura sem se sobrepor a ela. A regra é **fade + subida sutil + stagger interno** como padrão geral, e **clip-path reveal** aplicado **cirurgicamente** em 3-4 fotos chamadas (não em todas). Tudo respeitando `prefers-reduced-motion`.

---

## ✅ Checklist de execução

### Tarefa 1 — Implementar reveal padrão em todas as seções

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** cada `<section>` precisa entrar com fade + subida sutil quando o usuário rola e ela aparece no viewport. Isso dá cadência à leitura sem chamar atenção. Padrão de marcas de luxo (Hermès, Bottega, Aman 2024).

**O que fazer:**

1. **Adicionar CSS base** no bloco `<style>` (próximo aos outros utilitários):

   ```css
   /* Reveal padrão — seção inteira */
   .reveal {
     opacity: 0;
     transform: translateY(24px);
     transition:
       opacity   500ms cubic-bezier(0.22, 1, 0.36, 1),
       transform 500ms cubic-bezier(0.22, 1, 0.36, 1);
     will-change: opacity, transform;
   }
   .reveal.is-visible {
     opacity: 1;
     transform: none;
   }

   /* Stagger — filhos entram em sequência */
   .reveal-stagger > * {
     opacity: 0;
     transform: translateY(16px);
     transition:
       opacity   450ms cubic-bezier(0.22, 1, 0.36, 1),
       transform 450ms cubic-bezier(0.22, 1, 0.36, 1);
   }
   .reveal-stagger.is-visible > *:nth-child(1) { transition-delay:   0ms; }
   .reveal-stagger.is-visible > *:nth-child(2) { transition-delay:  80ms; }
   .reveal-stagger.is-visible > *:nth-child(3) { transition-delay: 160ms; }
   .reveal-stagger.is-visible > *:nth-child(4) { transition-delay: 240ms; }
   .reveal-stagger.is-visible > *:nth-child(5) { transition-delay: 320ms; }
   .reveal-stagger.is-visible > *:nth-child(6) { transition-delay: 400ms; }
   .reveal-stagger.is-visible > * {
     opacity: 1;
     transform: none;
   }

   /* Acessibilidade — respeita preferência do usuário */
   @media (prefers-reduced-motion: reduce) {
     .reveal,
     .reveal-stagger > *,
     .reveal-image img {
       opacity: 1 !important;
       transform: none !important;
       transition: none !important;
       clip-path: none !important;
     }
   }
   ```

2. **Aplicar a classe `.reveal`** em **todas as `<section>`** da PDP:
   - `.hero` (atenção: ver "exceção do hero" abaixo)
   - `.envolvimento`
   - `.transformation`
   - `.experience`
   - `.features`
   - `.bundle`
   - `.testimonials`
   - `.presence`
   - `.process`
   - `.events`
   - `.tech-specs`
   - `.closing`

3. **Exceção do hero:** o hero é o que carrega na primeira tela. Aplicar `.reveal` nele faz com que o usuário veja a tela branca por 500ms antes do conteúdo aparecer — ruim. **Opção 1 (recomendada):** não aplicar `.reveal` no hero — ele já vem visível desde o load. **Opção 2:** aplicar mas adicionar `.is-visible` já no HTML (não esperar IntersectionObserver). Decidir pela leitura visual.

4. **Aplicar `.reveal-stagger`** em containers que têm múltiplos filhos visuais sequenciais. Lista mínima:
   - `.three-cols` (cards de transformação — 4 cards)
   - `.features-list` (lista de features tabs)
   - `.bundle-grid` (cards "O que vem junto" — 4 cards)
   - `.testi-row` (cards de depoimentos)
   - `.stats-row` (3 stats)
   - `.process-rows` (3 fileiras da nova entrega; nome final pode variar conforme o brief de ritmo visual)
   - `.events > div` (4 linhas de evento)
   - `.tech-list` (3 entradas do accordion)
   - `.faq-item`'s parent (5 perguntas)

5. **JavaScript** (adicionar no `<script>` final, junto com os outros listeners):

   ```javascript
   (function () {
     // Se o usuário pediu reduced-motion, materializar tudo na hora
     if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
       document.querySelectorAll('.reveal, .reveal-stagger, .reveal-image')
         .forEach(el => el.classList.add('is-visible'));
       return;
     }

     const io = new IntersectionObserver(entries => {
       entries.forEach(entry => {
         if (entry.isIntersecting) {
           entry.target.classList.add('is-visible');
           io.unobserve(entry.target);
         }
       });
     }, {
       threshold: 0.15,
       rootMargin: '0px 0px -10% 0px'
     });

     document.querySelectorAll('.reveal, .reveal-stagger, .reveal-image')
       .forEach(el => io.observe(el));
   })();
   ```

   **Importante:**
   - `threshold: 0.15` — dispara quando 15% do elemento está visível.
   - `rootMargin: '0px 0px -10% 0px'` — atrasa um pouco o dispara (margem inferior negativa). Faz a animação não disparar enquanto a seção ainda está "começando" a aparecer.
   - `io.unobserve` — uma vez disparada, para de observar. Não anima novamente em scroll de volta.

**Notas do Dev:**
> - **Hero:** Opção 1 (recomendada). Não apliquei `.reveal` na `<section class="hero">` — ela já vem visível desde o load para evitar o flash de 500ms na primeira tela.
> - **CSS base** colado dentro do bloco `<style>` em uma seção própria "REVEAL" logo após a media query de reduced-motion existente (a do `.logos-track`).
> - **Containers reveal-stagger aplicados** em 9 lugares: `.three-cols`, `.features-list`, `.bundle-grid`, `.testi-row`, `.stats-row`, `.process-rows`, `.tech-list`, `<div>` wrapper dos 4 event-rows e `<div>` wrapper dos 5 `<details>` do FAQ (esses dois últimos não tinham classe, ganharam `class="reveal-stagger"` direto).
> - **Espaçamento:** nenhum container precisou de ajuste — a animação muda só opacity+transform, não afeta layout.
> - **Performance:** `will-change: opacity, transform` (e `clip-path` nas reveal-image) já cuidam do compositing. IntersectionObserver com `io.unobserve` após disparo garante zero overhead pós-animação.

---

### Tarefa 2 — Aplicar clip-path reveal em fotos chamadas (cirúrgico)

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** essa é a animação **expressiva** da página. A foto se revela de baixo pra cima, como uma cortina abrindo. **Aplicada em TODAS as fotos vira pesado** — destrói o ritmo. Aplicada **só nas 3-4 fotos hero/chamadas**, vira detalhe memorável.

**Onde aplicar (lista exclusiva):**

1. **Hero principal** → `.hero-gallery .ph-main img` (foto grande da poltrona no topo)
2. **Seção 2 (Engenharia do toque)** → `.chair-img` (foto centralizada da poltrona)
3. **Seção 9 (Entrega — após o brief de ritmo visual)** → as 3 fotos da nova fileira alternada (Preparação, Transporte, Chegada)

**Não aplicar em:** thumbs do hero, fotos de cards menores, thumbnails de eventos, vídeos, imagens dentro do mosaico de eventos, foto de background da ficha técnica.

**O que fazer:**

1. **Adicionar CSS:**

   ```css
   /* Clip-path reveal — só nas fotos chamadas */
   .reveal-image img {
     clip-path: inset(0 0 100% 0);
     transition: clip-path 800ms cubic-bezier(0.22, 1, 0.36, 1);
     will-change: clip-path;
   }
   .reveal-image.is-visible img {
     clip-path: inset(0 0 0 0);
   }
   ```

2. **Aplicar a classe `.reveal-image`** nos containers das fotos elegidas acima. Exemplo:
   ```html
   <div class="ph ph-main reveal-image">
     <img src="..." alt="...">
   </div>
   ```

3. **JS já cuidado pela Tarefa 1** — o observador também observa `.reveal-image` (já está no querySelector).

4. **Importante:** se o container já tem `overflow: hidden` (a maioria tem), o clip-path funciona bem. Validar que não há overflow visual indesejado durante a animação. Se houver, garantir `overflow: hidden` no `.ph` ou container equivalente.

**Notas do Dev:**
> - Aplicado nos 5 elementos: `.ph-main` do hero (via container), `.chair-img` da Engenharia do toque (via classe direto no `<img>`, ver decisão abaixo) e nos 3 `.process-row-photo` da seção Entrega.
> - **Decisão de implementação:** o `.chair-img` é um `<img>` direto dentro do `.envolvimento-stage` grid, sem container envolvente. Wrap em `<div>` quebraria o template `grid-template-columns: 1fr auto 1fr` que centraliza a poltrona. **Solução:** estendi o seletor CSS para aceitar `.reveal-image` também direto no `<img>`:
>   ```css
>   .reveal-image img, img.reveal-image { clip-path: inset(0 0 100% 0); ... }
>   .reveal-image.is-visible img, img.reveal-image.is-visible { clip-path: inset(0 0 0 0); }
>   ```
>   Funciona porque a transição é no próprio elemento `<img>`.
> - **Containers já têm `overflow: hidden`:** `.ph` (linha 153) tem `overflow: hidden`; `.process-row-photo` também (declarei explicitamente). O `clip-path` corta dentro dos limites do `<img>`, não precisa do overflow no container, mas mantém o contorno limpo.
> - **Hero curtain raise:** o `.ph-main.reveal-image` é a primeira coisa que aparece na page load. O IntersectionObserver dispara o `is-visible` imediatamente (elemento já está intersecting na primeira observação), produzindo o efeito de "cortina subindo" no carregamento — coerente com a intenção luxury do brief.
> - **Mobile:** transição de `clip-path` é GPU-accelerated; testou fluida em viewport estreito.

---

## 🚧 Pendências bloqueantes

A Tarefa 2 depende, em parte, do brief [ritmo-visual-final-pdp.md](ritmo-visual-final-pdp.md) ter sido executado (as 3 fotos da nova fileira alternada da seção 9). Se aquele brief ainda não foi aplicado, **a Tarefa 2 pode ser feita só nos itens 1 e 2** (hero + seção 2). Os 3 itens da seção 9 entram numa rodada futura assim que o layout novo estiver aplicado.

---

## ❌ Não fazer

- Não tocar em [index.html](../index.html) — escopo continua só PDP
- Não usar `slide` lateral (translateX) — sensação SaaS, oposto de luxo
- Não usar bounce, spring, ou easings com overshoot — sensação de jogo
- Não animar em loop após o reveal (pulse, heartbeat, breathing) — destrói o luxo
- Não aplicar `.reveal-image` em **todas** as fotos — usar SÓ na lista da Tarefa 2
- Não usar duração maior que 800ms ou menor que 400ms — fora desse range vira "lento demais" ou "rápido demais"
- Não substituir o easing `cubic-bezier(0.22, 1, 0.36, 1)` por `ease`, `ease-out`, ou similar — esse easing específico é o que dá a sensação editorial
- Não adicionar `delay` global longo (>500ms) na entrada — usuário não pode esperar pra ler

---

## 📝 Log do Dev

**Resumo geral do que foi feito:**
> Implementadas as 2 tarefas em [produto.html](../produto.html). T1: bloco CSS de `.reveal`, `.reveal-stagger` e suporte a `prefers-reduced-motion` adicionado; `.reveal` aplicada em 11 das 12 `<section>` (hero ficou fora, conforme Opção 1 do brief); `.reveal-stagger` aplicada em 9 containers (incluindo dois wrappers genéricos sem classe nos eventos e FAQ que ganharam `class="reveal-stagger"`). T2: `.reveal-image` aplicada nos 5 elementos chamados (hero main, chair-img, 3 process-row-photos), com extensão de CSS para aceitar a classe direto no `<img>` (necessário para a chair-img). IntersectionObserver com `threshold: 0.15` e `rootMargin: '0px 0px -10% 0px'` adicionado ao bloco de scripts existente, com short-circuit pra reduced-motion (materializa tudo na hora).

**Decisões que tomei e que não estavam no brief:**
> 1. **`.chair-img` direto no `<img>`:** o brief diz "aplicar `.reveal-image` nos containers das fotos". A chair-img é `<img>` direto dentro de grid sem container — wrap quebraria o layout. Estendi o seletor CSS para aceitar `img.reveal-image` também, em vez de criar wrapper. Mais cirúrgico, sem alterar layout.
> 2. **`reveal-stagger` em wrappers anônimos:** os 4 event-rows e os 5 `<details>` do FAQ estavam dentro de `<div>` sem classe. Adicionei `class="reveal-stagger"` neles para evitar criar IDs ad-hoc ou usar seletores CSS frágeis (`.events > div:nth-child(2) > div`).
> 3. **JS adicionado como IIFE separado** ao fim do bloco `<script>` existente, ao lado dos outros listeners. Não introduzi nenhuma dependência ou bundler.

**O que ficou pra próxima rodada / dúvidas pro Diretor:**
> - Validar visualmente: a sensação do "stagger" em `.testi-row` (carrossel horizontal) precisa ser conferida. Os children entram com delay 0/80/160/240ms, o que pode parecer estranho se o usuário scrolla horizontalmente mais tarde — mas como `io.unobserve` é chamado, eles só animam uma vez. Vale ver se prefere o stagger ou se em carrossel horizontal devemos remover o `.reveal-stagger` e deixar o reveal apenas na section.
> - Hero "curtain raise" do `.ph-main`: efeito intencional de cortina subindo no load. Se ficar incomodativo (usuário percebe a foto "aparecendo"), basta remover o `.reveal-image` do `.ph-main` ou adicionar `is-visible` direto no HTML.

**Tempo aproximado da execução:**
> ~25 minutos (CSS base, aplicação em 11 sections + 9 containers + 5 imagens, JS, audit final, redação das notas).
