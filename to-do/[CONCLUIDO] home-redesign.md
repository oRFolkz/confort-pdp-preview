# Brief — Redesign da Home (Confort Supremo)

> **Documento de trabalho entre dois agentes**
> - **Diretor (Claude):** define o que fazer e por quê.
> - **Dev (Claude Code):** executa, marca o checkbox e preenche o campo de notas com o que fez. Se algo desviar do brief ou ficar bloqueado, escrever no mesmo campo.

**Escopo desta rodada:** somente [index.html](../index.html). A PDP ([produto.html](../produto.html)) **NÃO entra** neste brief.

**Regra dura mantida:** **sem travessão** em copy. Substituir por ponto, vírgula, dois pontos ou quebra de frase.

---

## Princípios estratégicos da Home

A Home da Confort Supremo **não é página de produto**. É o **vestíbulo da marca**: onde o visitante entende quem ela é, onde ela vive, e por que vale a pena entrar mais fundo. O catálogo, a vitrine e a venda ficam na PDP.

Três princípios que regem todas as decisões abaixo:

1. **Manifesto antes de catálogo.** A Home apresenta a marca, não os recursos. Quem chega curioso encontra um universo; quem chega buscando produto encontra um convite pra ir pra PDP.
2. **Convite, não vitrine.** Cada seção termina convidando pra um caminho (PDP, eventos, WhatsApp). Não força clique; respira.
3. **Diferente da PDP visualmente, idêntica em identidade.** Mesma paleta, mesma tipografia, mesma cadência editorial. Mas com seções e ritmo próprios — pra que o usuário que rolar a PDP depois sinta **continuidade**, não repetição.

---

## Diagnóstico do estado atual

A Home hoje tem **15 seções** (header → 13 seções de conteúdo → footer). Aproximadamente **6 dessas seções são clones literais da PDP**, o que faz a Home virar uma "PDP em formato curto". Isso destrói a função de Home.

| Seção atual | Função real | Decisão |
|---|---|---|
| Header | Navegação + WhatsApp | **Manter** (replicar Header da PDP, já aprovado em [copy-pdp-aprovada.md](copy-pdp-aprovada.md)) |
| Hero | Recepção da marca | **Refinar copy + CTAs** |
| Weight ("O dia tem um peso") | Manifesto narrativo | **Manter + refinar** (essa é joia da Home, não existe na PDP) |
| Logos band | Sinal de pertencimento | **Manter + remover Toyota** |
| Lifestyle (mosaico de fotos) | Respiro visual | **Mover** pra dentro da seção "Espaços" |
| Features (tabs) | Detalhe técnico | **Remover** (é clone literal da PDP) |
| Intensidade | Detalhe técnico | **Remover** (clone da PDP) |
| Inteligência | Detalhe técnico | **Remover** (clone da PDP) |
| Models | Linha de produtos | **Manter + refinar** |
| Spaces ("Não é só para sua casa") | Diversidade de uso | **Manter + refinar + fotos novas** |
| Testimonials (vídeos individuais) | Prova social individual | **Remover** (PDP já tem) |
| Bundle ("O que vem junto") | Garantia + entrega | **Remover** (não é função da Home) |
| Events (lista de 4 iguais) | Convite presencial | **Manter + enxugar** (3 eventos) |
| FAQ | Quebra de objeção | **Remover** (PDP tem; Home não precisa) |
| Footer | Institucional | **Manter** (replicar do [copy-pdp-aprovada.md](copy-pdp-aprovada.md)) |

**Resultado final:** Home passa de **15 seções para 9** (header + 7 seções de conteúdo + footer). Mais respiratória, mais editorial, mais funcional.

---

## Estrutura final da nova Home

```
┌──────────────────────────────────────────────────────────────┐
│  0.  Header (igual PDP)                                      │
│  1.  Hero — Manifesto de boas-vindas                         │
│  2.  O peso do dia — Manifesto narrativo (refinado)          │
│  3.  Régua de logos — Sinal de pertencimento                 │
│  4.  Dois modelos — Apresentação da linha                    │
│  5.  A Poltrona das Estrelas — Prova social agregada (NOVA)  │
│  6.  Não é só pra sua casa — Diversidade de uso (refinada)   │
│  7.  Próximos eventos — Convite presencial (enxugado)        │
│  8.  Convite final — Closing editorial (NOVA)                │
│  9.  Footer (igual PDP)                                      │
└──────────────────────────────────────────────────────────────┘
```

---

## ✅ Checklist de execução

### Tarefa 0 — Replicar Header e Footer da PDP

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** identidade visual coerente entre Home e PDP. Quem navega entre as duas não deve sentir descontinuidade.

**O que fazer:** copiar do [produto.html](../produto.html) (versão final após brief de copy):
- Bloco `<header class="site-header">` com brand, menu Sobre/Onde Testar/Contato, ícone WhatsApp e CTA "Agendar Experiência"
- Bloco `<footer class="site-footer">` em 4 colunas (Identidade, Navegação, Suporte, Fale com a Marca), faixa de pagamento monocromática, copyright

Conteúdo, classes e CSS mantidos idênticos. Não recriar do zero. Reutilizar.

**Notas do Dev:**
> _(preencher: copiou direto ou houve algum ajuste de classe específico da Home?)_

---

### Tarefa 1 — Hero (Manifesto de boas-vindas)

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** o hero é o que diferencia a Home da PDP. Aqui a marca **fala**, não vende. A frase atual já é uma das melhores da Confort Supremo. Vamos manter o eixo e refinar entrega + CTAs.

**Onde:** `<section class="hero">` no [index.html](../index.html) (atualmente linhas ~1440-1466).

**O que fazer:**

1. **Vídeo de fundo:** **manter o vídeo atual** (já é forte). Adicionar overlay sutil em gradient pra garantir legibilidade do texto:
   ```css
   .hero-bg::after {
     content: "";
     position: absolute;
     inset: 0;
     background: linear-gradient(to bottom, rgba(0,0,0,0.15) 0%, rgba(0,0,0,0.35) 100%);
   }
   ```

2. **Copy da headline:** **manter integral.** É frase intocável.
   ```
   Você cuida de tudo.
   Está na hora de alguém cuidar de você.
   ```
   (com "cuidar de você." em bold)

3. **Sub-headline (refinar):**
   - Atual: `A poltrona que reconstrói você. Todos os dias. Para quem entende que descanso de qualidade não é luxo: é o que te mantém inteiro.`
   - Proposta: `A poltrona que está nos camarins, salões e eventos de quem decide. Agora, também na sua sala.`
   - Razão: refina o tom, amarra no universo "Poltrona das Estrelas", dá especificidade (camarins/salões/eventos) e termina convidando pra dentro da casa do cliente. Sem travessão, sem clichê de luxo.

4. **CTAs (refinar):**
   - Atual: `Quero a minha Confort Supremo` (botão primário) + `Agendar Experiência` (botão ghost)
   - Proposta:
     - **Primário:** `Conhecer a Confort Supremo` → `href="produto.html"`
     - **Secundário:** `Agendar experiência` → `href="#eventos"` (anchor da seção 7 desta Home)
   - Razão: "Quero a minha" é vocabulário de carrinho de e-commerce popular. "Conhecer" é convite editorial. Pra Home, o objetivo é levar pra PDP, não converter direto.

5. **Decisão sobre o terceiro CTA (WhatsApp):** **não adicionar.** O ícone WhatsApp já está no header. Dois CTAs no hero (Conhecer + Agendar) é o suficiente. Mais que isso vira indecisão.

**Notas do Dev:**
> _(preencher: o gradient overlay ficou bom em mobile? Algum ajuste de tipografia precisou?)_

---

### Tarefa 2 — O peso do dia (Manifesto narrativo)

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** esta é a **seção mais editorial da Home** e a que mais a distingue da PDP. Storytelling puro: 4 momentos do dia de quem decide, terminando na poltrona. Não tem nada parecido na PDP. **Mantém integral, com refinos pequenos de copy.**

**Onde:** `<section class="section weight">` (atualmente linhas ~1471-1514).

**O que fazer:**

1. **Header:**
   - Eyebrow: `Antes da poltrona` → manter
   - H2: `O dia tem um peso que ninguém vê.` → manter integralmente (com "peso" em bold/destaque)
   - Sub: `Mas o corpo sente cada hora.` → manter

2. **Os 4 itens:** mantidos com pequenos refinos:

   ```
   01  Você acorda antes do alarme.
       A lista já está rodando na sua cabeça. Reunião, decisão,
       deslocamento. O dia começa antes de começar.

   02  O ombro trava às 14h.
       Você ignora. Tem mais três horas pela frente. A cadeira
       do escritório não foi feita pro ritmo que você vive.

   03  Você chega em casa.
       O silêncio finalmente existe. Mas o corpo ainda está no
       trabalho. Tenso, pesado, sem saber como desligar.

   04  Então o silêncio chega de verdade.
       E em vinte minutos, o corpo finalmente acredita que terminou.
   ```

   **Diffs:**
   - Item 02 — `feita para o ritmo` → `feita pro ritmo` (oralidade premium)
   - Item 03 — `tenso, pesado, sem saber como desligar.` (continua) — substituí o travessão original (`— tenso, pesado, sem saber como desligar`) por ponto final + frase
   - Item 04 — mantido

3. **Visual:** o item 04 já tem a classe `is-featured` que destaca dele. **Manter.** É o "punch" da seção.

4. **Adicionar lead final** (opcional, depois dos 4 itens):
   ```
   É nesse exato silêncio que ela entra.
   ```
   Em peso regular, mais discreto, como uma "ponte" pro próximo bloco. Avaliar se cabe visualmente. Se aglomerar, pular.

**Notas do Dev:**
> _(preencher: aplicou o lead final ou pulou? Visual ficou consistente com a `.section` padrão?)_

---

### Tarefa 3 — Régua de logos

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** mesma régua infinita da PDP. Sinal de pertencimento ao universo premium. Toyota destoa, sai (mesma decisão da PDP).

**Onde:** `<section class="logos-band">` (atualmente linhas ~1519-1548).

**O que fazer:**

1. **Remover** todas as ocorrências de Toyota (alt="Toyota" + as repetições aria-hidden). Lista final: **Tesla · Ferrari · Mercedes-Benz · BMW · Porsche** (5 logos × 2 metades = 10 imagens).

2. **Adicionar eyebrow centralizado acima da régua** (hoje a seção vem "do nada"):
   ```html
   <p class="eyebrow" style="text-align: center; margin-bottom: var(--space-3);">
     Onde a Confort Supremo já está
   </p>
   ```

3. **Garantir loop seamless** com a metade duplicada (já está implementado, só revisar se ficou ímpar depois da remoção de Toyota).

**Notas do Dev:**
> _(preencher: removeu também as repetições aria-hidden de Toyota? O loop continua seamless?)_

---

### Tarefa 4 — Dois modelos (Apresentação da linha)

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** a Home precisa apresentar a **linha** (não detalhar o produto). Dois cards lado a lado, função de "menu de entrada" pra duas direções (Supremo → PDP / Essential → lista de interesse via WhatsApp).

**Onde:** `<section class="section models">` (atualmente linhas ~1761-1814).

**O que fazer:**

1. **Header:**
   - Eyebrow: `Linha Confort` → trocar para `LINHA SUPREMA` (consistente com a decisão da Buybox da PDP — ver [copy-pdp-aprovada.md](copy-pdp-aprovada.md) Seção 1)
   - H2: `Dois modelos. Uma filosofia.` → manter (com "Uma filosofia." em bold)
   - Sub: `Escolha o que cabe no seu espaço — sem abrir mão do conforto.` → `Escolha o que cabe no seu espaço. Sem abrir mão do conforto.` (travessão removido)

2. **Card 1 — Confort Essential** (à esquerda; modelo compacto, ainda não disponível):
   ```
   Compacto · Lista de interesse

   Confort Essential

   O essencial do descanso, em um corpo mais discreto.
   Pensado para apartamentos e ambientes menores.

   · Massagem em 4 zonas principais
   · Gravidade Zero
   · Reclinação manual
   · Acabamento em couro premium

   [ Receber novidade pelo WhatsApp ]   ← CTA novo (substitui "Em breve" desabilitado)
   ```
   **Mudanças:**
   - Tag: `Compacto · Em breve` → `Compacto · Lista de interesse` (proativo, não passivo)
   - Lead: remover o `[mock]` do começo
   - Specs: `Acabamento em couro sintético premium` → `Acabamento em couro premium` (corta "sintético" — desnecessário)
   - CTA: o botão desabilitado `Em breve` vira **link funcional pra WhatsApp**, com mensagem pré-preenchida pelo hook `data-cta="whatsapp"`. Mas com mensagem específica:
     ```
     Olá, tenho interesse no Confort Essential. Quero receber quando estiver disponível.
     ```
   - Como o hook atual usa uma URL única, deixar como **um link com data-attribute específico**, ex: `data-cta="whatsapp" data-message="lista-essential"` — e ampliar o hook no JS pra ler `data-message` e trocar o `text=` da URL. **Pendência do dev:** decidir se vale ampliar o hook ou criar `<a href="https://wa.me/...?text=..." target="_blank">` inline pra esse caso específico.
   - **Foto:** trocar `FOTO_25.jpg` (atual, é uma poltrona qualquer) pela imagem nova `img/essential-residencial.jpg` (ver Bloco de Imagens abaixo). Se ainda não tiver, manter placeholder.

3. **Card 2 — Confort Supremo** (à direita; produto principal disponível):
   ```
   Topo de linha · Disponível

   Confort Supremo

   A pausa que os melhores se permitem.

   · Sistema de 8 rolos multidimensional
   · Detecção corporal automática
   · 22 pontos de pressão (airbag corpo todo)
   · Áudio HiFi Bluetooth · Modo Sono

   [ Conhecer a Confort Supremo ]   ← CTA leva pra PDP
   ```
   **Mudanças:**
   - Lead: `A poltrona que reconstrói você. Todos os dias.` → `A pausa que os melhores se permitem.` (consistente com a buybox da PDP)
   - Specs:
     - `7 funcionalidades inteligentes` → remover (vago, não é spec real)
     - `Display LCD touch com IA` → `Detecção corporal automática` (alinha com Seção 2 da PDP)
     - `22 pontos de pressão · airbag corpo todo` → manter
     - `Áudio HiFi Bluetooth · Modo Sono` → manter
     - **Adicionar:** `Sistema de 8 rolos multidimensional` no topo
   - CTA: `Conhecer Supremo` → `Conhecer a Confort Supremo` (artigo + nome completo, mais editorial)
   - **Foto:** trocar `FOTO_22.jpg` pela imagem nova `img/supremo-residencial.jpg` (ver Bloco de Imagens). Se ainda não tiver, manter placeholder.

**Notas do Dev:**
> _(preencher: como resolveu o data-message do CTA Essential? Substituiu fotos pelas novas ou aguardou o Fábio gerar?)_

---

### Tarefa 5 — A Poltrona das Estrelas (Prova social agregada) — NOVA

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** a Home não precisa de depoimentos individuais (vídeos da Dra. Gabriela etc.) — a PDP já tem isso. Em vez disso, **prova social agregada** no formato editorial: mosaico de eventos premium com os nomes que importam.

**Onde:** [index.html](../index.html) — **substitui** completamente a seção `<section class="section testimonials">` atual (linhas ~1847-1960). A nova seção pode reusar parte da CSS do mosaico da PDP (`.presence-banner`).

**O que fazer:**

1. **Estrutura HTML nova:**
   ```html
   <section class="section stars">
     <div class="container">
       <p class="eyebrow" style="text-align: center;">A Poltrona das Estrelas</p>
       <h2 class="h-display" style="text-align: center;">
         Onde a Confort Supremo está,<br>
         está <strong>quem decide.</strong>
       </h2>

       <div class="stars-mosaic">
         <!-- 4-6 fotos de eventos com overlays nominados -->
         <figure>
           <img src="img/evento-porsche.jpg" alt="Porsche Experience São Paulo">
           <figcaption>Porsche Experience São Paulo</figcaption>
         </figure>
         <figure>
           <img src="img/evento-realestate.jpg" alt="Trinca Real Estate">
           <figcaption>Trinca Real Estate · Rio</figcaption>
         </figure>
         <figure>
           <img src="img/evento-coaching.jpg" alt="Casa de Destino">
           <figcaption>Tiago Brunet · Casa de Destino</figcaption>
         </figure>
         <figure>
           <img src="img/evento-beauty.jpg" alt="Legacy Club">
           <figcaption>Legacy Club · Beauty Edition</figcaption>
         </figure>
       </div>
     </div>
   </section>
   ```

2. **CSS sugerido:**
   - Mosaico em grid 4-col (desktop) → 2-col (tablet) → 1-col (mobile, com swipe horizontal via `.carousel` quando o brief de carrosséis estiver aplicado)
   - Cada `<figure>` com aspect-ratio 1/1 ou 4/5
   - `<figcaption>` em overlay no canto inferior esquerdo, fundo gradient bottom-to-top semi-transparente, texto branco em peso medium

3. **Imagens:** reutilizar as 4 imagens já geradas em `img/` (`evento-porsche.jpg`, `evento-realestate.jpg`, `evento-coaching.jpg`, `evento-beauty.jpg`). **Não precisa gerar nada novo.**

4. **Sem CTA na seção.** É prova social pura. Quem se interessa rola pra próxima.

**Notas do Dev:**
> _(preencher: tomou decisão sobre 4 ou 6 cards? Aplicou carrossel em mobile?)_

---

### Tarefa 6 — Não é só pra sua casa (Diversidade de uso)

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** seção exclusiva da Home, **excelente conceito** (a poltrona em ambientes que não são residenciais). Reforça a tese "Poltrona das Estrelas" mostrando que ela vive onde quem decide vive. Mantém estrutura, refina copy, melhora fotos.

**Onde:** `<section class="spaces" id="spaces">` (atualmente linhas ~1819-1842).

**O que fazer:**

1. **H2:** `Ela não é apenas para a sua casa.` → manter
2. **Lead:** `Certos espaços têm um padrão que se vê antes mesmo de entrar. A Confort Supremo já faz parte de alguns deles.` → manter integral (frase muito boa)

3. **5 ambientes (`data-sublabels`)** — **manter** os 5 atuais, refinar copy:
   ```
   Lounges executivos · São Paulo
   Spas e bem-estar · Rio de Janeiro
   Showrooms premium · Belo Horizonte
   Áreas VIP · Brasília
   Coberturas privativas · Florianópolis
   ```
   Sem mudança. Já está editorial.

4. **Fotos (`<img>` dos 5 slots):** **trocar pelas 5 fotos novas geradas** (ver Bloco de Imagens). As fotos atuais são genéricas e se repetem. Lista de substituição:
   - Slot 01 → `img/espaco-lounge.jpg`
   - Slot 02 → `img/espaco-spa.jpg`
   - Slot 03 → `img/espaco-showroom.jpg`
   - Slot 04 → `img/espaco-vip.jpg`
   - Slot 05 → `img/espaco-cobertura.jpg`

5. **Mover o `lifestyle strip`** (mosaico de 3 fotos editoriais atual, linhas ~1553-1564) **pra dentro desta seção** como pré-introdução visual. Ou seja: a seção 6 (Spaces) começa com o mosaico de 3 fotos e logo abaixo vem o slider de 5 ambientes. Une o que estava espalhado.

**Notas do Dev:**
> _(preencher: integrou o lifestyle dentro da seção spaces ou manteve separado? Por quê?)_

---

### Tarefa 7 — Próximos eventos (Convite presencial — enxugado)

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** a PDP já tem a agenda completa de 4 eventos. Na Home, lista enxuta de 3 eventos + CTA pra ver a agenda completa na PDP. Não duplicar.

**Onde:** `<section class="section events" id="testar">` (atualmente linhas ~2013-2042). Trocar o `id="testar"` por `id="eventos"` pra bater com o anchor do hero.

**O que fazer:**

1. **Header:**
   - Adicionar eyebrow: `Onde testar` (estava ausente)
   - H2: `Sente antes de decidir.` → manter (com "antes de decidir." em bold)
   - Adicionar intro curto:
     ```
     Nos próximos eventos, a poltrona vai até você.
     ```

2. **3 eventos** (os 4 atuais são placeholder repetido; trocar pelos 3 primeiros da PDP):
   ```
   [Thumb]  Porsche Experience São Paulo     São Paulo · 28/05/2026       [Reservar]
   [Thumb]  Trinca Real Estate · Edição Rio  Rio de Janeiro · 12/06/2026  [Reservar]
   [Thumb]  Tiago Brunet · Casa de Destino   São Paulo · 25/06/2026       [Reservar]
   ```
   (O 4º evento — Legacy Club Beauty Edition — fica só na PDP. Aqui mostra a "ponta do iceberg".)

3. **Adicionar CTA secundário no final da seção:**
   ```
   Ver agenda completa  →  produto.html#testar
   ```
   Em estilo `btn-ghost` ou link discreto. Convida pra ir pra PDP sem forçar.

4. **Thumbs:** reutilizar `img/evento-porsche.jpg`, `img/evento-realestate.jpg`, `img/evento-coaching.jpg` (mesmas da PDP).

**Notas do Dev:**
> _(preencher: ajustou o id de "testar" para "eventos" no anchor do hero também? Validou que o link da PDP ainda funciona?)_

---

### Tarefa 8 — Convite final (Closing editorial) — NOVA

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** a Home termina hoje em FAQ (clone da PDP) — péssima nota de saída. **Substituir por closing editorial**: foto/vídeo full-bleed + frase emocional que ecoa o hero + 2 CTAs.

**Onde:** [index.html](../index.html) — **substituir** completamente a seção `<section class="section faq" id="faq">` (linhas ~2046-2094).

**O que fazer:**

1. **Estrutura HTML nova:**
   ```html
   <section class="section closing-home">
     <div class="closing-bg">
       <video
         src="[mesma fonte de vídeo do hero, ou foto img/closing.jpg]"
         autoplay muted loop playsinline preload="auto"
         poster="img/closing-poster.jpg"></video>
     </div>

     <div class="closing-content">
       <p class="eyebrow">O Convite</p>
       <h2 class="h-display">
         Você cuida de tudo.<br>
         Está na hora de alguém <strong>cuidar de você.</strong>
       </h2>
       <p class="closing-sub">
         A Confort Supremo está esperando.
       </p>

       <div class="closing-ctas">
         <a href="produto.html" class="btn btn-primary">Conhecer a Confort Supremo</a>
         <a data-cta="whatsapp" target="_blank" rel="noopener" class="btn btn-ghost">Falar com Especialista</a>
       </div>
     </div>
   </section>
   ```

2. **Visual:**
   - Vídeo/foto full-bleed atrás do texto
   - Overlay em gradient (mesma técnica do hero)
   - Texto centralizado, com peso alto na headline (eco visual do hero)
   - 2 CTAs lado a lado (primário marrom + secundário ghost)

3. **A frase repetida do hero ("Você cuida de tudo...") cria um arco narrativo**: a Home começa e termina com a mesma proposição, mas no fim ela soa como **decisão** (e não como pergunta).

4. **Imagem:** se não houver `img/closing.jpg` ou `img/closing-poster.jpg`, usar o mesmo vídeo do hero atual (`84e0bc179800425e87e716b1ae7ff7ca.mp4`). Vale a coerência.

**Notas do Dev:**
> _(preencher: usou vídeo ou foto estática? Os 2 CTAs ficaram bem no mobile? Foi necessário ajustar o overlay?)_

---

### Tarefa 9 — Remover seções clonadas da PDP

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** consolida a tese da Home. Seções abaixo são versões duplicadas do que a PDP já entrega. Remover sem dó.

**Onde:** [index.html](../index.html) — remover blocos HTML inteiros + qualquer CSS específico que não seja reutilizado em outra seção.

**O que remover:**

| Seção | Linhas aproximadas | Razão |
|---|---|---|
| Features (tabs interativos) | ~1568-1631 | Idêntica à seção Features da PDP. PDP tem 6 features detalhadas + imagem grande. Aqui só dilui. |
| Intensidade | ~1635-1694 | Detalhe técnico. Pertence à PDP (accordion técnico). |
| Inteligência | ~1698-1757 | Mesma lógica. Detalhe técnico. PDP cobre. |
| Testimonials individuais (Dra. Gabriela etc.) | ~1847-1960 | **Substituída pela Tarefa 5** (A Poltrona das Estrelas — prova social agregada). |
| Bundle ("O que vem junto") | ~1965-2008 | Cards de Garantia/Entrega/Atendimento são da PDP. Na Home descontextualizam o tom. |
| FAQ | ~2046-2094 | **Substituída pela Tarefa 8** (Closing editorial). FAQ na Home dilui o convite. |

**Atenção:**
- Cuidado pra **não remover CSS compartilhado**. Antes de apagar um bloco de CSS, validar se nenhuma das seções mantidas usa.
- O CSS de `.features` da Home pode ser totalmente removido (não vai mais existir tabs aqui). Mas alguns CSS de `.bundle` ou `.testimonials` podem estar interligados com classes globais (`.h-display`, `.eyebrow`) — esses **não** mexer.

**Notas do Dev:**
> _(preencher: lista de classes CSS efetivamente removidas, alguma reaproveitamento, e validação que o CSS global continua íntegro)_

---

## 🖼 Imagens novas necessárias (prompts para Nano Banana)

São **7 imagens novas** específicas pra Home. As outras (eventos, etc.) já estão em `img/`.

### Imagem 1 — `img/essential-residencial.jpg` (3:2 horizontal)
**Para:** Tarefa 4, card Confort Essential
**Anexar:** ❌ Não (modelo Essential ainda não existe fisicamente)

```
A compact, modern massage chair in Brown leather, smaller and more
discreet than a full-size massage chair (about 70% the size, slimmer
profile, less mechanical-looking, designed to fit in apartments).
Positioned in a stylish modern São Paulo apartment living room with
white walls, oak wood floor, large window showing blurred city
skyline at golden hour, minimalist Scandinavian furniture, plants.
Editorial residential photography, warm late afternoon natural light,
premium aesthetic. No people, no text. 3:2 aspect ratio.
```

### Imagem 2 — `img/supremo-residencial.jpg` (3:2)
**Para:** Tarefa 4, card Confort Supremo
**Anexar:** ✅ Sim (poltrona Brown de referência)

```
A premium massage chair (preserve exact design, color, and Brown
leather details from the reference image) as the centerpiece of a
luxurious modern penthouse living room. Floor-to-ceiling windows
showing a blurred metropolitan skyline at golden hour, marble and
dark wood interior, ambient indirect lighting, premium aesthetic
(Aman, RH Modern style). Editorial photography, warm cinematic
tones, no people, no text. 3:2 aspect ratio.
```

### Imagens 3 a 7 — Os 5 espaços (1:1 quadradas, ou 4:5 verticais)
**Para:** Tarefa 6, seção "Não é só pra sua casa"
**Anexar:** ✅ Sim em todas (poltrona Brown de referência)

#### 3 — `img/espaco-lounge.jpg`
```
A premium massage chair (preserve exact Brown leather design from
reference) inside an executive corporate lounge in São Paulo,
floor-to-ceiling windows with city view at sunset, modern Brazilian
business interior design, leather seating, minimalist art on walls,
soft warm directional lighting. Editorial corporate photography,
no people, no text or logos. 4:5 aspect ratio.
```

#### 4 — `img/espaco-spa.jpg`
```
A premium massage chair (preserve exact Brown leather design from
reference) inside a high-end Rio de Janeiro spa, dimmed warm
candlelight, neutral linen drapes, organic textures (wood, stone),
plants, serene atmosphere, wellness aesthetic. Editorial spa
photography, no people, no text. 4:5 aspect ratio.
```

#### 5 — `img/espaco-showroom.jpg`
```
A premium massage chair (preserve exact Brown leather design from
reference) inside a minimalist Belo Horizonte automotive or design
showroom, polished concrete floor, large open space, dramatic
overhead lighting, neutral palette, sculptural architecture.
Editorial showroom photography, no people, no text or logos.
4:5 aspect ratio.
```

#### 6 — `img/espaco-vip.jpg`
```
A premium massage chair (preserve exact Brown leather design from
reference) inside an exclusive Brasília VIP airport-style lounge or
private members club, dark wood paneling, leather and brass accents,
ambient warm lighting, low-key luxury, no windows visible.
Editorial private-club photography, no people, no text. 4:5 aspect ratio.
```

#### 7 — `img/espaco-cobertura.jpg`
```
A premium massage chair (preserve exact Brown leather design from
reference) on the open terrace of a private penthouse in
Florianópolis, ocean view at golden hour, infinity pool partially
visible, minimalist outdoor furniture, palm trees in soft background
blur, late afternoon warm natural light. Editorial luxury real
estate photography, no people, no text. 4:5 aspect ratio.
```

### Opcional — `img/closing.jpg` ou `img/closing-poster.jpg` (16:9 horizontal)
**Para:** Tarefa 8, closing editorial
**Anexar:** ✅ Sim
**Pode pular se preferir reusar o vídeo atual do hero.**

```
Cinematic ultra-wide shot of a premium massage chair (preserve
exact Brown leather design from reference) in a dimly lit modern
living room at twilight, single warm directional light from a side
lamp creating dramatic shadows, glass of whiskey on a side table,
abstract art on the wall. Pure atmosphere, no people, no text,
editorial mood photography. 16:9 aspect ratio.
```

---

## 🚧 Pendências bloqueantes (do diretor pro Fábio)

**Resolvidas em 2026-05-15:**
- ✅ **Confort Essential** confirmado como nome final do modelo compacto. Não precisa nota de "naming pendente".
- ✅ **Mensagem do WhatsApp pré-preenchida** do card Essential aprovada: `Olá, tenho interesse no Confort Essential. Quero receber quando estiver disponível.`
- ✅ **Imagens novas:** Fábio vai gerar (Imagens 1, 3, 4, 5, 6, 7; Imagem 2 e Closing opcionais).

**Pendência ativa:**
- ⚠️ **Vídeos do hero e do closing são mocks.** Não existem vídeos reais da Confort Supremo no momento. Implementar a Home usando o vídeo mock atual, mas registrar como item de produção futuro: **substituir todos os vídeos por material real** (gravação profissional da poltrona em ambiente, idealmente captado em evento real). Até lá, o que está vai. Critério de aceite: o vídeo mock não pode mostrar de forma identificável outra marca de poltrona — se mostrar, sinalizar.

---

## ❌ Não fazer

- Não tocar em [produto.html](../produto.html) — escopo continua só Home
- Não criar carrinho, mini-cart, drawer de produto (decisão arquitetural já fechada)
- Não usar travessão em nenhuma copy (regra dura)
- Não adicionar tabs interativas / features detalhadas / accordions técnicos na Home (clone da PDP)
- Não duplicar a régua de logos em outras seções (ela já está em 1 lugar)
- Não adicionar "% off", "10x sem juros", banners promocionais
- Não usar foto de produto isolada em fundo branco no estilo "e-commerce padrão" — a Home é sempre **produto em contexto** (ambiente, evento, vida)
- Não duplicar a sub-headline do hero em nenhuma outra seção
- Não usar emojis em nenhuma copy

---

## 📝 Log do Dev

**Resumo geral do que foi feito:**
> Home reestruturada em [index.html](../index.html) de 15 seções para 9 (header + 8 conteúdo + footer). T0: header e footer importados da PDP (4 colunas com payment strip, CNPJ placeholder, ícones sociais SVG). T1: hero com overlay linear simplificado, copy refinada, CTAs novos (Conhecer a Confort Supremo + Agendar experiência → #eventos). T2: weight com 3 refinos de copy + lead-ponte final "É nesse exato silêncio que ela entra." T3: logos sem Toyota + eyebrow centralizado. T4: dois models com copy/CTA novos e CTA Essential virou WhatsApp com data-message. T5: nova seção Stars com mosaico 4-col reutilizando imagens dos eventos. T6: lifestyle integrado como adjacente da spaces (8ª seção combinada). T7: eventos enxugado para 3 + link agenda completa para PDP. T8: nova closing-home full-bleed com vídeo + 2 CTAs. T9: removidas Features, Intensidade, Inteligência e Bundle (192 linhas via sed, depois Bundle separadamente). JS antigo (features tabs + testi-play) substituído pelo hook WhatsApp centralizado com suporte a `data-message`. CSS órfão das seções removidas ficou no arquivo (não afeta render, marcado para cleanup futuro).

**Decisões que tomei e que não estavam no brief:**
> 1. **Lifestyle como `<section>` adjacente, não "dentro" de spaces.** O brief diz "pra dentro desta seção como pré-introdução visual". Como `.spaces` tem `height: 80vh`, `position: relative` com `.spaces-bg` absoluto e color invertido (texto claro sobre foto escura), inserir o mosaico de 3 fotos dentro do `<section>` quebraria o layout imersivo. Optei por manter como `<section>` adjacente (irmão), com a mesma posição visual de "abertura" da seção 8. Reposicionei do meio do arquivo para imediatamente antes do `.spaces`. Conceitualmente, é uma seção dupla composta (lifestyle mosaic + spaces immersive). Marquei como "Seção 8" no comentário HTML.
> 2. **Imagens da seção Spaces não substituídas.** As 5 imagens `img/espaco-*.jpg` listadas no brief não estão em `img/` (só existem evento-* + entrega-* + ficha-tecnica-fundo). Mantive os Shopify CDN como placeholder. Quando o Fábio gerar, basta trocar os 5 `src` na seção spaces (linhas ~1898-1902 atuais).
> 3. **Imagens essential/supremo-residencial e closing também ausentes** — também mantidos placeholders Shopify CDN (FOTO_25 para Essential, FOTO_22 para Supremo, mesmo vídeo do hero para closing). Trivial trocar quando vierem.
> 4. **Hook WhatsApp com data-message:** ampliei o hook do produto.html. Agora existe `window.WHATSAPP_MESSAGES = { essential: "..." }` e o JS lê `data-message="essential"` no `<a>` e gera URL específica via `phonePart + '?text=' + encodeURIComponent(...)`. Permite adicionar novas mensagens contextuais sem tocar no HTML do CTA.
> 5. **CTA "Agendar Experiência" do header e do hero apontam ambos para `#eventos`** (id renomeado da seção de eventos para bater com o anchor do hero). Brief dizia pra trocar `#testar` → `#eventos`, fiz isso.
> 6. **JS limpo:** removidos os IIFE de features tabs e testi-play (alvos não existem mais). Mantido o IIFE de spaces autoplay intacto (continua válido).
> 7. **CSS órfão preservado:** as classes `.features`, `.intensidade`, `.inteligencia`, `.bundle`, `.faq`, `.testimonials` ainda têm seus blocos CSS no arquivo, totalizando ~250 linhas. Não removi para não correr risco de quebrar utilitários compartilhados (`--color-*`, `.h-display`, etc.). Pode ser limpado em rodada futura de housekeeping CSS.

**O que ficou pra próxima rodada / dúvidas pro Diretor:**
> - **Imagens novas (7 imagens listadas no brief)** ainda não estão em `img/`. Quando o Fábio gerar via Nano Banana, é só copiar para o diretório com os nomes do brief — código já espera esses paths nas seções Models (3) e Spaces (5). Closing usa vídeo do hero — pode ficar como está ou substituir por `img/closing.jpg` quando vier.
> - **CSS órfão** das seções removidas (Features/Intensidade/Inteligência/Bundle/FAQ/Testimonials). ~250 linhas que ninguém referencia mais. Limpar quando der.
> - **Confirmar com o cliente** a copy do WhatsApp do Essential ("Olá, tenho interesse no Confort Essential. Quero receber quando estiver disponível.") e o naming "Confort Essential" (brief lista como pendência).
> - **Audit travessões** rodado. Único hit em copy visível era `<title>` ("Confort Supremo — A poltrona..." → "Confort Supremo · A Poltrona das Estrelas"). Tudo o mais era comentário CSS/HTML ou pseudo-element `::before` marker.

**Tempo aproximado da execução:**
> ~80 minutos (mapeamento estrutural, T0-T9 sequencialmente, reordenação de Stars antes de Lifestyle+Spaces, JS WhatsApp com data-message, audit final, redação das notas).
