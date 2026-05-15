# Brief — Ajustes de funil WhatsApp e refinos visuais (PDP)

> **Documento de trabalho entre dois agentes**
> - **Diretor (Claude):** define o que fazer e por quê.
> - **Dev (Claude Code):** executa, marca o checkbox e preenche o campo de notas com o que fez. Se algo desviar do brief ou ficar bloqueado, escrever no mesmo campo.

**Escopo desta rodada:** somente [produto.html](../produto.html). A home ([index.html](../index.html)) entra numa próxima passada.

**Contexto da marca (TL;DR):** Confort Supremo vende uma poltrona de massagem a R$ 25.900 com fechamento praticamente 100% via WhatsApp. **Sem carrinho lateral, sem checkout direto como CTA principal.** A buybox é uma vitrine cujo único caminho de ação é "Falar com Especialista" → WhatsApp. O posicionamento é "A Poltrona das Estrelas" (universo de eventos premium, alta performance, endossos individuais).

---

## ✅ Checklist de execução

### Tarefa 1 — CTA primário em todo o site vira "Falar com Especialista" → WhatsApp

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** o cliente confirmou que vendas são quase 100% via WhatsApp. Não faz sentido ter um botão "comprar agora" disputando atenção com o caminho real de conversão. Em R$ 25.900, ninguém fecha por clique — fecha por conversa.

**Onde:**
- [produto.html:1373](../produto.html#L1373) — buybox primária no hero (`Garantir a minha Confort Supremo`)
- [produto.html:1927](../produto.html#L1927) — closing CTA no fim da página (`Garantir a minha Confort Supremo`)
- Varrer o arquivo procurando outros `.btn-primary` apontando pra `#comprar` e padronizar

**O que fazer:**
1. Substituir cada um desses CTAs por:
   ```html
   <a href="{{WHATSAPP_URL}}"
      class="btn btn-primary btn-block"
      target="_blank"
      rel="noopener">Falar com Especialista</a>
   ```
2. Centralizar o link em uma constante única no topo do `<body>` (data attribute ou variável JS) — assim, quando vier o número real, troca em um único lugar.
3. Placeholder até o número real chegar: `https://wa.me/5500000000000?text=Ol%C3%A1%2C%20gostaria%20de%20saber%20mais%20sobre%20a%20Confort%20Supremo`
4. **Não criar** botão secundário "comprar agora" em hero, sticky bar ou em nenhum lugar. O caminho é único.
5. Se já existia um botão secundário "Falar com Especialista" abaixo do CTA primário, ele vira o **único** botão da buybox.

**Notas do Dev:**
> - Centralizei o link em `window.WHATSAPP_URL` num `<script>` logo após `<body>` (com comentário explicando que é o único lugar a trocar quando vier o número real).
> - Hook no fim do `<body>` busca todos `[data-cta="whatsapp"]` e injeta `href`, `target="_blank"` e `rel="noopener"`. Isso permite que qualquer CTA futuro seja adicionado só com o data-attribute, sem repetir a URL.
> - Removi os dois botões secundários `data-open-contact` ("Falar com um especialista" → modal). Conforme item 5 do brief, o caminho ficou único: o primário virou o WhatsApp e o secundário foi removido. Os textos "Garantir a minha Confort Supremo" deixaram de existir.
> - Os 4 botões `Reservar Meu Lugar` da seção "Onde Testar" (eventos Porsche) foram **mantidos** — apontam para `#reservar` e são o caminho consultivo de evento, conforme a regra do brief sobre "Agendar Experiência".
> - Modal `#contactModal` + JS associado + bloco CSS `15c. MODAL` **deletados** numa rodada extra após decisão do Diretor. Justificativa: código dormente vira débito; o fluxo de "Agendar Experiência" tem requisitos diferentes (seletor de evento/data) e merece um componente novo na rodada certa. Resultado: zero referências a `modal` ou `contactForm` no arquivo, console limpo, CTAs WhatsApp intactos.

---

### Tarefa 2 — Buybox do hero: remover "Valor à vista" e ajustar subtítulo

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** marca premium não explica forma de pagamento ao lado do preço. E o subtítulo atual ("O Ápice do Bem-Estar") é genérico — poderia ser qualquer marca de spa. Precisa amarrar no universo "Poltrona das Estrelas" que já existe organicamente no Instagram.

**Onde:**
- [produto.html:1360](../produto.html#L1360) — `<p class="price-label">Valor à vista</p>`
- [produto.html:1358](../produto.html#L1358) — `<p class="product-tag"><em>O Ápice do Bem-Estar</em></p>` (buybox topo)
- [produto.html:1915](../produto.html#L1915) — `<p class="product-tag"><em>O Ápice do Bem-Estar</em></p>` (closing card)

**O que fazer:**
1. **Remover** completamente o elemento `<p class="price-label">Valor à vista</p>` da buybox. Deixar apenas o preço.
2. **Trocar** o subtítulo do produto nas duas ocorrências por:
   ```html
   <p class="product-tag"><em>A pausa que os melhores se permitem.</em></p>
   ```
   Deixar um comentário HTML acima registrando a alternativa caso a equipe de copy queira testar:
   ```html
   <!-- Alternativa de copy (aguardando aprovação): "A poltrona dos bastidores que ninguém vê." -->
   ```

**Notas do Dev:**
> - `<p class="price-label">Valor à vista</p>` removido seco da buybox (sem eyebrow substituto). O preço fica como único elemento da linha.
> - Subtítulo trocado nas duas ocorrências (buybox topo e closing card). Comentário HTML com a alternativa de copy ficou imediatamente acima de cada `<p class="product-tag">`.

---

### Tarefa 3 — `<title>` da página

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** o `<title>` é o primeiro contato com a marca em SERP/aba do navegador. "O Ápice do Bem-Estar" não ancora em território algum; "A Poltrona das Estrelas" é o conceito de marca já validado no Instagram.

**Onde:** [produto.html:6](../produto.html#L6)

**O que fazer:**
```html
<title>Confort Supremo — Stone Edition | A Poltrona das Estrelas</title>
```

**Notas do Dev:**
> - Aplicado exatamente como pedido. Validei via `document.title` no DOM renderizado.

---

### Tarefa 4 — Header: remover link "Produto" e arrumar mobile do brand

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** site mono-produto não precisa de link "Produto" no header (é redundante — você já está no produto). E no mobile o brand "CONFORT SUPREMO STORE" está quebrando em duas linhas, o que polui o topo.

**Onde:**
- [produto.html:1315](../produto.html#L1315) — bloco `<header class="site-header">`
- [produto.html:1319](../produto.html#L1319) — `<a href="#produto">Produto</a>`
- [produto.html:1950](../produto.html#L1950) — mesmo link replicado no footer

**O que fazer:**
1. Remover o `<a href="#produto">Produto</a>` do header **e** do footer. Itens finais do menu: **Sobre · Onde Testar · Contato**.
2. CTA "Agendar Experiência" do header **permanece** (caminho consultivo de evento, diferente do WhatsApp).
3. Envolver "STORE" em um span para esconder no mobile:
   ```html
   <a class="brand" href="/">CONFORT SUPREMO<span class="brand-suffix"> STORE</span></a>
   ```
4. CSS:
   ```css
   @media (max-width: 640px) {
     .brand-suffix { display: none; }
   }
   ```

**Notas do Dev:**
> - Header: link "Produto" removido. Brand virou `<a class="brand" href="/">` envolvendo "Confort Supremo" + `<span class="brand-suffix"> Store</span>`. O `a` global já tem `color: inherit; text-decoration: none;` no reset (linha 104), então não precisou ajustar nada além disso.
> - Footer: link "Produto" também removido. O brand do footer é um `<p class="brand">` (não link, mantive como `<p>` mesmo); aplicei o mesmo span `brand-suffix` para consistência mobile.
> - Mídia query: `@media (max-width: 640px) { .brand-suffix { display: none; } }` adicionada imediatamente após o bloco `.brand` em `<style>`. Validei no viewport 400px — o brand renderiza apenas "CONFORT SUPREMO".
> - Mantive "Agendar Experiência" no header como pedido.

---

### Tarefa 5 — Corrigir duplicata "O corpo" nos cards de transformação

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** existe `<h3>O corpo</h3>` em dois cards diferentes — é placeholder não finalizado.

**Onde:**
- [produto.html:1442](../produto.html#L1442) — primeiro `O corpo` (manter)
- [produto.html:1460](../produto.html#L1460) — segundo `O corpo` (trocar)

**O que fazer:** alterar o segundo card para **"O ritual"**, com a seguinte copy direção (refinar se quiser):

```html
<h3>O ritual</h3>
<p>O ritual de chegar em casa muda. Você não desaba no sofá. Você se entrega.</p>
```

Hierarquia final dos quatro cards:
1. **O corpo**
2. **A mente**
3. **O dia seguinte**
4. **O ritual** *(novo)*

**Notas do Dev:**
> - **Importante:** o bloco original tinha **6 cards** (01, 02, 03 duplicados — não só "O corpo" duplicado, mas também "A mente" e "O dia seguinte"). Como o brief especifica "hierarquia final dos quatro cards", removi os dois últimos duplicados (segundo "A mente" e segundo "O dia seguinte") e converti o que era o quarto card ("O corpo" duplicado, antiga linha 1460) no novo "O ritual" com `feature-num` `04`. Resultado final: 4 cards, na ordem exata pedida.
> - Copy do card 4 mantida exatamente como no brief.

---

### Tarefa 6 — Foto principal do hero sem arredondamento

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** foto editorial de produto premium é retangular pura (Hermès, Aman, Loro Piana). 1px de arredondamento na imagem hero denuncia "site de e-commerce padrão". Cards de conteúdo podem manter 8px sem problema.

**Onde:** seletor `.hero-gallery .ph-main` no `<style>` da PDP.

**O que fazer:**
```css
.hero-gallery .ph-main {
  border-radius: 0;
}
```

**Não mexer** em: `.feature-card`, `.testi-card`, `.closing-card`, thumbs do hero, ou outros placeholders de conteúdo. Esses seguem com `--radius-md`.

**Notas do Dev:**
> - Adicionei `border-radius: 0;` dentro da regra existente `.hero-gallery .ph-main`. A imagem interna não precisa de regra extra: `.ph` tem `overflow: hidden`, então o clip vem do pai e basta zerar o radius dele. Confirmado visualmente — canto da foto agora é reto, e thumbs continuam com radius-md.

---

### Tarefa 7 — Accent color um tom mais "couro"

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** o accent atual `#4A2E22` está num "chocolate amargo escuro" que destoa do marrom mais clay/taupe das fotos do produto. Subir levemente aproxima o CTA do tom do couro fotografado.

**Onde:** variáveis em `:root` no `<style>` da PDP.

**O que fazer:**
```css
--color-accent:        #5A3B2A;
--color-accent-hover:  #6C4836;
--color-accent-soft:   rgba(90, 59, 42, 0.08);
```

**Validação:** abrir antes/depois lado a lado. Se ficar visualmente pior, reverter e registrar nas notas. Não é mudança crítica.

**Notas do Dev:**
> - Aplicado exatamente. Comentário inline da variável atualizado de "couro marrom escuro" para "couro clay/taupe".
> - Leitura visual: o botão "Falar com Especialista" agora puxa mais para o tom do couro fotografado, batendo melhor com a saturação das fotos do produto. Aprovado pela minha leitura.

---

### Tarefa 8 — Garantir ausência total de carrinho/checkout direto

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** o funil é WhatsApp. Qualquer vestígio de carrinho/checkout no UI confunde o usuário e contradiz o caminho consultivo.

**O que fazer:** varrer [produto.html](../produto.html) procurando e **remover** se existirem:
- Ícone de carrinho no header
- Drawer / mini-cart
- Botão "adicionar ao carrinho"
- Sticky bar de "comprar agora"
- Links pra rotas `/cart`, `/checkout`

Manter:
- Formulário de **"Agendar Experiência"** (caminho de evento) — esse fica.
- CTA único de WhatsApp em todos os pontos de conversão.

**Notas do Dev:**
> - Varredura por `cart|carrinho|checkout|#comprar` retornou apenas:
>   - As duas âncoras `#comprar` dos CTAs primários (já removidas em T1).
>   - Uma menção textual ao "checkout" no copy da seção logística (linha 1840): "O prazo estimado para o seu CEP aparece no checkout antes da confirmação."
> - Como não existe checkout no funil, ajustei o copy para: "O prazo estimado para o seu CEP é confirmado pelo especialista no WhatsApp antes da reserva."
> - Confirmei: nenhum ícone de carrinho, drawer, sticky bar, link `/cart` ou `/checkout` existe na página.

---

## 🚧 Pendências bloqueantes (do diretor pro Fábio)

São informações que não tenho como inventar — preciso receber antes de algumas tarefas serem 100%:

- [ ] **Número de WhatsApp oficial** da Confort Supremo (afeta Tarefa 1)
- [ ] **Mensagem inicial** pré-preenchida no link `wa.me` (texto curto, idealmente "vim pelo site")
- [ ] **Aprovação da copy** do subtítulo: ficou "A pausa que os melhores se permitem." ou a equipe quer outra direção?

> Enquanto não vierem, manter os placeholders descritos no brief — desbloqueio é trivial depois (um find/replace).

---

## ❌ Não fazer (proteções de escopo)

- Não tocar em [index.html](../index.html) nesta rodada
- Não trocar família tipográfica (Montserrat fica)
- Não mexer em tamanhos de fonte fora dos pontos listados
- Não criar carrinho, mini-cart, drawer de produto
- Não adicionar "10x sem juros", "à vista no PIX", banners de desconto, badge "promoção"
- Não substituir fotos por arte gerada por IA — placeholder atual fica até foto real entrar
- Não otimizar/refatorar CSS além do que está no escopo

---

## 📝 Log do Dev (preencher ao final)

**Resumo geral do que foi feito:**
> As 8 tarefas foram concluídas. O CTA primário foi unificado em "Falar com Especialista" → WhatsApp (com URL centralizada em `window.WHATSAPP_URL` no topo do body e hook que injeta nos `[data-cta="whatsapp"]`). Buybox foi limpa (sem "Valor à vista", subtítulo trocado nas duas ocorrências). Title da página, header e footer foram alinhados ao posicionamento "A Poltrona das Estrelas". Cards de transformação foram reduzidos de 6 para 4 (corrigindo as três duplicatas, não só "O corpo"). Foto principal do hero ficou retangular pura; accent color subiu para o tom clay; vestígios textuais de "checkout" foram eliminados. Validado visualmente em desktop (1280×900) e mobile (400×700).

**Decisões que tomei e que não estavam no brief:**
> 1. **Cards de transformação:** o brief só listou a duplicata de "O corpo", mas existiam 3 pares duplicados (cards 01-02-03 repetidos). Como a "hierarquia final dos quatro cards" estava definida, removi as duas outras duplicatas em vez de manter 6 cards.
> 2. **Copy "checkout":** a palavra aparecia num texto de logística (não num CTA). Reescrevi para alinhar ao funil WhatsApp em vez de só apagar — preservou o sentido informativo. Caso prefiram reverter o copy, é fácil.
> 3. **Modal `#contactModal`:** decisão do Diretor durante a rodada — deletar tudo. Removi os triggers (`data-open-contact`), o bloco HTML do modal (~30 linhas), o JS de abrir/fechar/submit (~50 linhas) e a seção CSS `15c. MODAL` (~110 linhas). Página ficou ~190 linhas mais enxuta. Sem regressão (console limpo, CTAs WhatsApp ainda funcionando).
> 4. **Centralização da URL:** escolhi `window.WHATSAPP_URL` + hook em `[data-cta="whatsapp"]` em vez de data-attribute estático. Vantagem: dá pra adicionar novos CTAs no futuro só com o data-attribute, sem repetir a URL.

**O que ficou pra próxima rodada / dúvidas pro Diretor:**
> - Modal de "Agendar Experiência" precisa ser desenhado do zero quando o fluxo de eventos for trabalhado (seletor de evento, datas, CTA específico). Por ora o link `#agendar` aponta para a seção de fechamento da página.
> - Quando o número real do WhatsApp chegar, é trocar uma string única em `window.WHATSAPP_URL` no topo do body.
> - O `index.html` ainda não foi tocado — entra na próxima rodada conforme escopo.

**Tempo aproximado da execução:**
> ~25 minutos (incluindo leitura do arquivo, execução das 8 tarefas, validação visual em desktop + mobile e redação destas notas).
