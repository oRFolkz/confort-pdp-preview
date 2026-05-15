# Brief — Carrosséis com swiper de mouse + setas

> **Documento de trabalho entre dois agentes**
> - **Diretor (Claude):** define o que fazer e por quê.
> - **Dev (Claude Code):** executa, marca o checkbox e preenche o campo de notas com o que fez. Se algo desviar do brief ou ficar bloqueado, escrever no mesmo campo.

**Escopo desta rodada:** somente [produto.html](../produto.html). Implementar um padrão único de carrossel reutilizável (drag com mouse + setas + swipe touch nativo) e aplicar nas seções que se beneficiam de comportamento de carrossel. Independente dos demais briefs.

**Contexto estratégico:** no e-commerce brasileiro, **arrastar com mouse para navegar entre fotos** é um comportamento intuitivo — usuários esperam que funcione. Combinar isso com o **padrão Shopify Dawn de setas visíveis** entrega o melhor dos dois mundos: mouse-drag pra quem descobre + setas visíveis pra quem não. Tudo isso sem usar Swiper.js (~150kb). A implementação custa **~3kb de JavaScript vanilla**.

**Princípio do diretor:**
- Em **desktop**: setas visíveis no hover do container + drag funcional + swipe nativo via pointer events
- Em **mobile**: swipe touch nativo via scroll-snap (setas ocultas — não fazem sentido em touch)
- **Sem bibliotecas externas.** Vanilla puro.

---

## ✅ Checklist de execução

### Tarefa 1 — Criar helper genérico de carrossel (CSS + JS único)

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** em vez de cada seção implementar carrossel à sua maneira, criar **um padrão único** reutilizável. Reduz código, garante consistência visual, facilita manutenção.

**Onde:** [produto.html](../produto.html) — adicionar no bloco `<style>` (junto aos outros utilitários) e no `<script>` final.

**O que fazer:**

1. **HTML — padrão a ser usado em qualquer seção que vire carrossel:**

   ```html
   <div class="carousel" data-carousel>
     <button class="carousel-arrow carousel-prev" aria-label="Anterior">
       <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
         <path d="M15 6l-6 6 6 6"/>
       </svg>
     </button>

     <div class="carousel-track">
       <!-- itens vão aqui (cards, fotos, vídeos) -->
       <div class="carousel-item">…</div>
       <div class="carousel-item">…</div>
       <div class="carousel-item">…</div>
     </div>

     <button class="carousel-arrow carousel-next" aria-label="Próximo">
       <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
         <path d="M9 6l6 6-6 6"/>
       </svg>
     </button>
   </div>
   ```

2. **CSS — adicionar como utilitário genérico:**

   ```css
   /* ==================================================
      CAROUSEL — padrão único reutilizável
      ================================================== */
   .carousel {
     position: relative;
   }

   .carousel-track {
     display: flex;
     gap: var(--space-3);
     overflow-x: auto;
     scroll-snap-type: x mandatory;
     scroll-behavior: smooth;
     scrollbar-width: none;
     -ms-overflow-style: none;
     cursor: grab;
     -webkit-tap-highlight-color: transparent;
   }
   .carousel-track::-webkit-scrollbar { display: none; }

   .carousel-track.is-dragging {
     cursor: grabbing;
     scroll-behavior: auto;       /* desabilita smooth durante drag */
     user-select: none;
   }
   .carousel-track.is-dragging * {
     pointer-events: none;        /* evita cliques acidentais nos itens */
   }

   .carousel-item {
     flex: 0 0 auto;
     scroll-snap-align: start;
   }

   /* Setas — ocultas em mobile, aparecem em hover no desktop */
   .carousel-arrow {
     position: absolute;
     top: 50%;
     transform: translateY(-50%);
     width: 44px;
     height: 44px;
     border-radius: 50%;
     background: rgba(251, 248, 243, 0.92);
     border: 1px solid var(--color-border);
     color: var(--color-text);
     display: none;                /* hidden por padrão */
     align-items: center;
     justify-content: center;
     z-index: 5;
     transition: opacity 240ms cubic-bezier(0.22, 1, 0.36, 1),
                 background 200ms;
     backdrop-filter: blur(8px);
   }
   .carousel-arrow:hover {
     background: var(--color-bg);
   }
   .carousel-arrow:disabled {
     opacity: 0.35;
     cursor: not-allowed;
   }
   .carousel-arrow svg {
     width: 20px;
     height: 20px;
   }
   .carousel-prev { left: var(--space-2); }
   .carousel-next { right: var(--space-2); }

   /* Desktop: setas visíveis on hover do container */
   @media (hover: hover) and (min-width: 768px) {
     .carousel-arrow {
       display: flex;
       opacity: 0;
     }
     .carousel:hover .carousel-arrow {
       opacity: 1;
     }
   }

   /* Acessibilidade — sem animação smooth pra quem prefere reduzido */
   @media (prefers-reduced-motion: reduce) {
     .carousel-track { scroll-behavior: auto; }
   }
   ```

3. **JavaScript — adicionar como bloco IIFE no `<script>` final:**

   ```javascript
   (function () {
     const carousels = document.querySelectorAll('[data-carousel]');
     if (!carousels.length) return;

     carousels.forEach(carousel => {
       const track = carousel.querySelector('.carousel-track');
       const prev = carousel.querySelector('.carousel-prev');
       const next = carousel.querySelector('.carousel-next');
       if (!track) return;

       // Helper: largura de um item (incluindo gap)
       const stepSize = () => {
         const first = track.children[0];
         if (!first) return 0;
         const styles = getComputedStyle(track);
         const gap = parseFloat(styles.columnGap || styles.gap || 0);
         return first.getBoundingClientRect().width + gap;
       };

       // Setas — scroll programático
       prev?.addEventListener('click', () => {
         track.scrollBy({ left: -stepSize(), behavior: 'smooth' });
       });
       next?.addEventListener('click', () => {
         track.scrollBy({ left: stepSize(), behavior: 'smooth' });
       });

       // Atualizar estado das setas (disabled nos extremos)
       const updateArrows = () => {
         if (!prev || !next) return;
         const max = track.scrollWidth - track.clientWidth;
         prev.disabled = track.scrollLeft <= 1;
         next.disabled = track.scrollLeft >= max - 1;
       };
       track.addEventListener('scroll', updateArrows, { passive: true });
       window.addEventListener('resize', updateArrows);
       updateArrows();

       // Drag com pointer events (mouse + touch + caneta)
       let isDown = false;
       let startX = 0;
       let startScroll = 0;
       let moved = false;

       track.addEventListener('pointerdown', e => {
         // Ignora drag em botões/links dentro do carrossel
         if (e.target.closest('button, a')) return;
         isDown = true;
         moved = false;
         startX = e.clientX;
         startScroll = track.scrollLeft;
         track.setPointerCapture(e.pointerId);
       });

       track.addEventListener('pointermove', e => {
         if (!isDown) return;
         const delta = e.clientX - startX;
         if (Math.abs(delta) > 4) {
           moved = true;
           track.classList.add('is-dragging');
         }
         track.scrollLeft = startScroll - delta;
       });

       const endDrag = e => {
         if (!isDown) return;
         isDown = false;
         track.classList.remove('is-dragging');
         try { track.releasePointerCapture(e.pointerId); } catch {}
       };
       track.addEventListener('pointerup', endDrag);
       track.addEventListener('pointercancel', endDrag);
       track.addEventListener('pointerleave', endDrag);

       // Previne click no item se foi drag (não um clique simples)
       track.addEventListener('click', e => {
         if (moved) {
           e.stopPropagation();
           e.preventDefault();
           moved = false;
         }
       }, true);
     });
   })();
   ```

4. **Validações importantes:**
   - **Acessibilidade:** setas têm `aria-label`. O foco do teclado funciona normalmente (botões nativos). Scroll-snap garante que ao usar Tab dentro do track, o item focado entra no viewport.
   - **Não conflita com `.reveal` do brief de animações** — `data-carousel` é seletor independente.
   - **Touch nativo continua funcionando** — pointer events cobrem mouse + touch + caneta unificadamente.

**Notas do Dev:**
> - **CSS:** padrão colado integralmente como veio no brief, com 2 adições para alinhar com a paleta da página: `backdrop-filter: blur(8px)` ganhou o prefixo `-webkit-backdrop-filter` (Safari). Adicionei `cursor: pointer` nas setas.
> - **Overrides desktop:** criei dois blocos de media query logo após o helper. (1) `@media (min-width: 1025px)` cobre `.transformation`, `.bundle` e `.testimonials`: viram grid (4-col, 4-col, 3-col), com `overflow: visible`, `margin-right: 0`, `padding-right: 0`, `cursor: auto` para anular o bleed e o cursor grab herdados das classes existentes (`.three-cols`, `.bundle-grid`, `.testi-row`). (2) `@media (min-width: 769px)` faz o mesmo para `.presence` (volta a grid 4-col em tablet+desktop). As `.carousel-arrow` ficam `display: none` em todos os breakpoints sem carrossel ativo.
> - **JS:** IIFE colocado logo após o IIFE de reveal, dentro do bloco `<script>` final. Zero dependências externas. `passive: true` no listener de scroll — performance ok.
> - **Conflitos de pointer events:** o `e.target.closest('button, a')` no `pointerdown` cobre os links de evento na seção de eventos (não foram aplicados como carrossel, mas é proteção genérica). O play overlay dos depoimentos (`.testi-play`) é um `<button>` — então o drag não dispara em cima dele, o play continua clicável. ✓
> - **Reveal-stagger coexistência:** o `.carousel-track` continua sendo o pai imediato dos cards, então o `.reveal-stagger > *` continua funcionando. Os botões de seta (`.carousel-arrow`) são irmãos do track dentro do `.carousel`, não filhos do track — não interferem no stagger.

---

### Tarefa 2 — Aplicar o helper `.carousel` nas seções escolhidas

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** o helper só vale se for usado. Lista abaixo define onde aplicar e em qual breakpoint.

**Mapa de aplicação:**

| Seção | Quando vira carrossel | Justificativa |
|---|---|---|
| **Hero — thumbs da galeria** | Sempre | É carrossel por natureza. Hoje já é scroll, vira drag + setas. |
| **Hero — foto principal** | Não aplicar `.carousel` | A troca de foto é via clique no thumb, não por arraste. Manter como está. |
| **Cards de transformação (seção 3)** | Mobile + tablet (≤1024px) | Desktop cabem 4 cards em grid. Mobile precisa de scroll horizontal pra não empilhar. |
| **Cards "O que vem junto" (seção 6)** | Mobile + tablet (≤1024px) | Mesma lógica. |
| **Depoimentos (seção 7)** | Mobile + tablet (≤1024px) | 3 vídeos cabem no desktop. Em telas menores vira swipe. |
| **Mosaico de eventos (seção 8)** | Mobile (≤768px) | Grid 4-col funciona em desktop e tablet. Só vira carrossel em mobile. |
| **Stats row (seção 7 fim)** | Não aplicar | 3 stats cabem em qualquer tela com layout responsivo. |
| **Lista de eventos (seção 10)** | Não aplicar | É lista vertical, não horizontal. |
| **Régua de logos** | Não aplicar | Já tem animação CSS de loop infinito; mantém. |

**O que fazer:**

1. **Hero thumbs** ([produto.html](../produto.html) — `.hero-thumbs`):
   - Envolver os thumbs em um container `.carousel` com `data-carousel`
   - Renomear `.hero-thumbs` pra `.carousel-track` ou aplicar **ambas** as classes (mais seguro pra não quebrar outros estilos)
   - Adicionar os dois botões `.carousel-arrow` (prev/next)
   - Cada thumb ganha `.carousel-item`

2. **Cards de transformação, Cards "O que vem junto", Depoimentos, Mosaico de eventos:**
   - Mesma operação: envolver o container existente em `.carousel`, adicionar `.carousel-track` ao container interno, classes `.carousel-item` nos filhos, e os dois botões de seta.
   - **Importante:** o carrossel só "ativa visualmente" no breakpoint correto. Em desktop, manter o grid original com display reorganizado pra não virar uma "linha única scrollável":

     ```css
     /* Desktop: grid normal (sem carrossel ativo) */
     @media (min-width: 1025px) {
       .transformation .carousel-track {
         display: grid;
         grid-template-columns: repeat(4, 1fr);
         overflow: visible;
       }
       .transformation .carousel-arrow { display: none; }
     }
     ```

   - Repetir o padrão acima nos breakpoints corretos pra cada seção (mosaico de eventos é 768px, os outros são 1024px).

3. **Não tocar em:** régua de logos (já tem loop infinito CSS), stats row, lista de eventos, foto principal do hero.

**Notas do Dev:**
> - **Aplicado em 5 seções:**
>   1. **Hero thumbs** — wrap em `.carousel`, classes `hero-thumbs carousel-track` no track, `ph ph-thumb carousel-item` em cada thumb. Sempre carrossel (sem override desktop).
>   2. **Transformation (`.three-cols`)** — wrap + track combinado com `reveal-stagger`. 4 cards com `tcard carousel-item`. Vira grid 4-col acima de 1024px.
>   3. **Bundle (`.bundle-grid`)** — wrap + track combinado com `reveal-stagger`. 4 cards com `bcard carousel-item`. Grid 4-col acima de 1024px.
>   4. **Testimonials (`.testi-row`)** — wrap + track combinado com `reveal-stagger`. 3 `testi-item carousel-item`. Grid 3-col acima de 1024px.
>   5. **Presence (`.presence-banner`)** — wrap + track. 4 `.ph.ph-3-4.carousel-item`. Grid 4-col acima de 768px (tablet + desktop). O `style="margin-top: var(--space-5);"` que estava no `.presence-banner` foi movido para o `.carousel` wrapper.
> - **Não aplicado em:** régua de logos (CSS loop infinito mantido), stats row, lista de eventos (linhas verticais com thumbs), foto principal do hero, FAQ accordion, ficha técnica accordion.
> - **Mantive ambas as classes** no track (existente + `carousel-track`) conforme orientação do brief. Os estilos existentes (bleed via `margin-right` negativo, `padding-right`, flex-basis de 3.5 itens) continuam ativos em mobile/tablet; os overrides desktop neutralizam o que precisa.
> - **Reveal-stagger compatível:** todos os tracks com cards mantiveram a classe `reveal-stagger`. Como os botões prev/next ficam fora do track, a contagem de filhos do stagger continua só com os cards (delays 0/80/160/240ms aplicados corretamente).

---

## 🚧 Pendências bloqueantes

- A **Tarefa 2 aplicada nos cards da seção 9 (Entrega) NÃO é necessária** — depois do brief de ritmo visual, aquela seção vira **fileiras horizontais alternadas**, não carrossel. Não confundir.
- Se o brief [ritmo-visual-final-pdp.md](ritmo-visual-final-pdp.md) ainda não foi aplicado, **aguardar ou coordenar com o Fábio** antes de tocar nos containers das seções 7, 8 e 9 — eles podem mudar de estrutura.

---

## ❌ Não fazer

- Não usar Swiper.js, Slick, Embla, ou qualquer outra biblioteca de carrossel
- Não criar paginação com bullets/dots — só drag + setas (padrão Shopify Dawn)
- Não animar o "snap" com easings exóticos — `scroll-behavior: smooth` nativo é suficiente
- Não esconder as setas em desktop a ponto de o usuário não descobrir — `opacity: 0 + on hover` está ok porque o hover do container revela; **não usar `display: none` em desktop**
- Não aplicar `.carousel` em listas que **não fazem sentido horizontal** (lista de eventos verticais, FAQ, stats row)
- Não criar carrossel automático (autoplay) — destrói o luxo
- Não tocar em [index.html](../index.html) — escopo continua só PDP

---

## 📝 Log do Dev

**Resumo geral do que foi feito:**
> Helper único de carrossel (CSS + JS vanilla, ~3kb) adicionado ao [produto.html](../produto.html). CSS aplicado como utilitário genérico logo após o bloco REVEAL, com dois blocos de media query para desativar o carrossel acima de 1024px (transformation, bundle, testimonials) e 768px (presence). JS adicionado como IIFE logo após o IIFE de reveal, cobrindo drag por pointer events (mouse + touch + caneta), setas com `scrollBy`, atualização de `disabled` nos extremos e prevenção de clique-acidental pós-drag. Aplicado em 5 lugares: hero thumbs (sempre), cards de transformação, cards "O que vem junto", depoimentos e mosaico de eventos.

**Decisões que tomei e que não estavam no brief:**
> 1. **Mantive ambas as classes** no track de cada seção em vez de substituir a classe existente por `carousel-track`. Razão explícita do brief: "aplicar ambas as classes (mais seguro pra não quebrar outros estilos)". O bleed lateral, scroll-snap e flex-basis de 3.5 cards já estão na classe original; o `.carousel-track` só adiciona cursor grab e o suporte a drag.
> 2. **Override de `cursor: auto`** no desktop. Sem isso, o `.carousel-track` deixava o cursor `grab` mesmo quando virava grid (sem drag possível). Trivial mas importante para a percepção.
> 3. **Override de `margin-right: 0; padding-right: 0`** no desktop. As classes existentes (`.three-cols` etc.) têm bleed à direita via margin negativo. Quando vira grid 4-col, esse bleed deixa o último card desalinhado com o grid de container. Zerei os dois para o grid ficar limpo.
> 4. **Mover `style="margin-top"`** do `.presence-banner` para o `.carousel` wrapper. Como o wrapper é o novo elemento de layout externo, o espaçamento entre o H2 e a galeria precisa ficar nele, não no track interno.
> 5. **Botões com `aria-label` contextual** ("Card anterior", "Próximo depoimento", etc.) em vez de só "Anterior"/"Próximo" — mais informativo para leitores de tela.

**O que ficou pra próxima rodada / dúvidas pro Diretor:**
> - Validar visualmente em 3 breakpoints: mobile (375), tablet (900), desktop (1280). O comportamento desktop (sem carrossel) deve mostrar o grid completo nas 4 seções; em tablet, presence vira grid (≥769), mas as outras 3 ainda são carrossel (porque o cutoff é 1025).
> - Hero thumbs em desktop: a régua continua scrollável horizontalmente porque tem 10 thumbs. Setas aparecem no hover — verificar se posição/aspecto está correto sobrepondo as thumbs.
> - Em telas muito largas (>1400px), as setas podem ficar "longe demais" das bordas dos cards porque o `.carousel` ocupa toda a largura do `.container`. Caso queira aproximar, ajustar `left: var(--space-2)` / `right: var(--space-2)`.

**Tempo aproximado da execução:**
> ~35 minutos (CSS, JS, aplicação em 5 seções, overrides por breakpoint, redação das notas).
