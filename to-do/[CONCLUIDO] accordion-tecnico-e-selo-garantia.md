# Brief — Accordion técnico + Selo de garantia (PDP)

> **Documento de trabalho entre dois agentes**
> - **Diretor (Claude):** define o que fazer e por quê.
> - **Dev (Claude Code):** executa, marca o checkbox e preenche o campo de notas com o que fez. Se algo desviar do brief ou ficar bloqueado, escrever no mesmo campo.

**Escopo desta rodada:** somente [produto.html](../produto.html). Dois acréscimos finos antes de declarar layout fechado e partir pra copy.

**Contexto estratégico (curto):** análise dos 4 concorrentes (Massage Express, Gran Belo, Doutor Massaggio, Dubai Magazine) mostrou que o **diferencial real de conversão** em PDP de poltrona de massagem high-ticket vem de:
1. **Densidade técnica em accordion** (lista expansível com especificações, funções, manual) — quem só quer sentir a marca rola direto; quem precisa confirmar 42 airbags ou tensão 110/220V abre e confere. Bônus: ajuda SEO e indexação por LLM (ChatGPT/Perplexity).
2. **Selo visual de garantia** próximo à buybox — comunica em peça gráfica o que hoje só vive em texto pequeno. A Confort Supremo tem **3 anos full com troca da poltrona inteira**, diferencial que nenhum concorrente tem. Não está visualmente destacado.

Após essas duas adições, **layout fica fechado** e a próxima rodada vira foco em **copy de todas as seções**.

---

## ✅ Checklist de execução

### Tarefa 1 — Accordion técnico antes do FAQ

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** Massage Express tem dois accordions densos ("Confira mais funções" + "Informações Extras") e isso é uma das razões reais de conversão deles. A gente precisa do mesmo poder técnico **sem poluir** a leitura editorial. Accordion resolve: invisível pra quem não quer; completo pra quem quer.

**Onde:** [produto.html](../produto.html) — adicionar uma nova `<section>` **imediatamente antes** da seção de FAQ (que provavelmente tem `id="faq"` ou similar). Se houver um closing card / CTA antes do FAQ, manter o accordion **antes** desse closing card também — a sequência natural é: features editoriais → accordion técnico → FAQ → closing.

**O que fazer:**

1. **Estrutura HTML:** usar `<details>/<summary>` nativos para acessibilidade e crawler-friendly (SEO/LLM). Estilizar pra parecer com o accordion do FAQ que já existe na página (manter consistência visual).

2. **Três entradas no accordion**, nesta ordem:

   **(a) Especificações técnicas**
   Tabela ou lista chave-valor. Pseudo-conteúdo placeholder (copy real vem na rodada seguinte):
   ```
   - Dimensões (aberta):        160cm × 80cm × 110cm
   - Dimensões (recolhida):     150cm × 80cm × 105cm
   - Peso:                       95kg
   - Capacidade de carga:        até 150kg
   - Altura do usuário:          1,50m a 1,95m
   - Voltagem:                   Bivolt automático (110V / 220V)
   - Potência:                   200W
   - Material do revestimento:   Couro PU premium
   - Material da estrutura:      Aço carbono reforçado
   - Comprimento do cabo:        2m
   - Garantia:                   3 anos full · troca total
   ```

   **(b) Funções e modos de massagem**
   Lista mais densa, em colunas ou agrupamento. Pseudo-conteúdo placeholder:
   ```
   Técnicas de massagem:
   - Shiatsu · Knocking · Tapping · Kneading · Rolling · Guasha

   Modos pré-programados:
   - Relaxamento profundo
   - Recuperação muscular
   - Pré-sono
   - Pós-treino
   - Alívio cervical
   - Massagem completa

   Recursos:
   - Sistema multidimensional de 8 rolos
   - Detecção automática do formato corporal
   - Cobertura de 100% das costas
   - Airbags em pescoço, ombros, braços, cintura, quadril, pernas e pés
   - Aquecimento lombar
   - Função zero gravidade
   - Alto-falantes Bluetooth HiFi
   ```

   **(c) Instalação e cuidados**
   Placeholder:
   ```
   Instalação:
   - Plug and play — pronta para usar ao ligar na tomada
   - Sem instalação técnica
   - Espaço mínimo recomendado: 2m × 1m de área livre

   Entrega:
   - Frete especializado em todo o Brasil
   - Transporte com manuseio dedicado
   - Confirmação de prazo pelo especialista no WhatsApp

   Cuidados:
   - Limpeza com pano levemente úmido
   - Não expor à luz solar direta prolongada
   - Manutenção preventiva recomendada anualmente
   ```

3. **Visual:**
   - Cabeçalho `<summary>` em peso medium (não bold), tamanho `--fs-md` ou `--fs-lg`, com indicador de abrir/fechar (chevron ou `+ / −`).
   - Conteúdo aberto em peso regular, `--fs-base`, linha alta (`--lh-body`).
   - Divisores finos entre entradas (`1px solid var(--color-border)`).
   - Sem sombra, sem cor de fundo destacada. Editorial, não cartão.
   - Tom igual ao do FAQ — se o FAQ tem `+/−`, usar o mesmo aqui.

4. **Header da seção** (acima dos 3 accordions):
   ```html
   <p class="eyebrow">Ficha técnica</p>
   <h2 class="h-display">Tudo o que importa, sem distração.</h2>
   ```
   (Copy provisória — vai pra refino na rodada de copy.)

5. **Acessibilidade:**
   - `<details>` com `<summary>` é nativo e suficiente.
   - Adicionar `aria-expanded` automaticamente cuidado pelo browser via `<details>`.

**Notas do Dev:**
> - Usei `<details>/<summary>` nativos. Zero JS, indexável por crawler/LLM, `aria-expanded` cuidado pelo próprio browser.
> - Posicionamento: nova `<section class="section tech-specs" id="ficha-tecnica">` inserida **entre** a seção `events` (Onde Testar) e a seção `closing` (Fechamento + FAQ + closing-card). Sequência final: hero → envolvimento → transformação → experiência → features → ... → eventos → **ficha técnica** → fechamento + FAQ. Cabe a referência por âncora futura via `#ficha-tecnica`.
> - Visual: para bater 100% com o FAQ, repliquei o padrão de `padding: var(--space-3) 0`, font display em `--fs-md`, indicador `+` em `--fs-lg` no `::after`, divisores 1px `--color-border` entre itens e topo. Diferença para o FAQ: quando aberto, troco `+` por `−` (FAQ não tem essa lógica porque é placeholder estático sem expansão).
> - Conteúdo interno: tabela `<dl class="tech-table">` para Especificações (2 col → 1 col no mobile), grupos com `tech-group-title` (eyebrow) + `<ul>` 2-col para Funções/Modos, e `ul.single-col` para listas que têm itens longos (Recursos, Instalação, Entrega, Cuidados). `—` em `--color-accent` no `::before` dos `<li>` para manter o estilo da página.
> - Header da seção: usei `<p class="eyebrow">Ficha técnica</p>` + `<h2 class="h-display">Tudo o que importa,<br><strong>sem distração.</strong></h2>` conforme brief, embrulhado num `.tech-header` para limitar largura. `max-width: 880px` no `.tech-list` evita medida de leitura muito larga em desktop.
> - Não precisou ajustar espaçamento da seção vizinha — `.section { padding: var(--space-7) 0 }` já entrega o respiro entre eventos e o accordion, e entre o accordion e o fechamento.

---

### Tarefa 2 — Selo visual de garantia próximo à buybox

**Status:** [ ] Pendente · [x] Concluído · [ ] Bloqueado

**Por quê:** a garantia "3 anos full com troca total" é o **único** diferencial competitivo que nenhum concorrente tem. Hoje só aparece como bullet de texto. Massage Express transformou os 2 anos deles em **peça gráfica visível no hero** — isso converte. A gente tem argumento melhor e está comunicando pior.

**Onde:** [produto.html](../produto.html) — dentro da buybox do hero, **entre o preço e o botão "Falar com Especialista"**. Ou, alternativa, **abaixo do botão** dependendo de como visualmente respira melhor. Decidir conforme densidade visual atual.

**O que fazer:**

1. **Conteúdo do selo:**
   ```
   3 ANOS · TROCA TOTAL
   Deu problema, trocamos a poltrona inteira.
   ```
   - Linha 1: kicker grande, peso bold ou semi-bold, letter-spacing leve.
   - Linha 2: subtexto em peso regular, `--fs-sm`, em `--color-text-muted`.

2. **Estilo editorial — NÃO badge promocional:**
   - **Sem** background colorido vivo, sem ícone de check verde, sem "%", sem badge fluo.
   - **Pode ter:** borda fina (`1px solid var(--color-border)`) ou linha superior + inferior fina (estilo divisor editorial), ou um separador vertical à esquerda.
   - Paleta: usar a mesma da página (creme/marrom). Acento sutil no `--color-accent` apenas em detalhe (linha, dot, separador).
   - Tipografia: mesma família, peso bold no kicker, regular no subtexto.

3. **Duas opções visuais que aceito** (dev escolhe pela leitura visual):

   **Opção A — Card horizontal fino abaixo do CTA:**
   Caixa retangular fina (~60px altura), borda 1px cor `--color-border`, padding generoso, texto centralizado ou alinhado à esquerda com ícone discreto à esquerda (opcional: monograma "CS" ou um glyph fino).

   **Opção B — Linha editorial sem caixa:**
   Apenas duas linhas de texto separadas por um divisor horizontal fino acima e abaixo. Sem borda lateral. Mais minimalista.

   **Preferência:** começar pela **Opção B** (mais editorial, conversa melhor com o resto da página). Se ficar visualmente apagado demais, migrar pra Opção A.

4. **Não confundir com a lista de bullets já existente** na buybox ("Garantia 3 anos full — troca da poltrona completa / Entrega especializada / Atendimento WhatsApp"). Decisão sobre isso:
   - Se o selo entrar, **remover** o bullet "Garantia 3 anos full" da lista (vira redundante).
   - Os outros bullets (entrega + atendimento) ficam.
   - Avaliar se a lista de bullets continua fazendo sentido ou se o selo + linha de tranquilidade abaixo do CTA já bastam. Decidir pela leitura visual.

5. **Mobile:** o selo precisa funcionar bem em viewport estreito (375-400px). Texto pode quebrar em 2 linhas no kicker, ou pode-se reduzir font-size proporcionalmente.

**Notas do Dev:**
> - **Opção B (editorial sem caixa).** Duas linhas separadas por divisor fino acima e abaixo (`border-top` + `border-bottom` 1px `--color-border`). Sem background colorido, sem ícone, sem badge. Conversa com o resto da página.
> - **Posição:** dentro da buybox, **abaixo do CTA "Falar com Especialista"** e **acima** das `.assurances`. No closing-card, mesma lógica (selo entre CTA e assurances). Razão: ficar logo no fim do caminho de ação — você lê o preço, vê o CTA, e a próxima coisa é a tranquilidade da garantia. Subindo o selo para entre preço e CTA quebrava o ritmo (preço → CTA é o par-chave).
> - **Bullet "Garantia 3 anos full" removido** nas duas listas (buybox hero + closing-card). Os outros bullets (entrega + atendimento WhatsApp na buybox; entrega + montagem inclusa no closing-card) ficaram porque comunicam coisas que o selo não diz.
> - **Conteúdo:** kicker "3 anos · Troca total" com o `·` em `--color-accent` num `<span class="seal-dot">` (separador editorial sutil). Sub: "Deu problema, trocamos a poltrona inteira." em `--fs-sm`, `--color-text-muted`. `role="note"` + `aria-label` para o conjunto.
> - **Mobile (390px):** o kicker cabe numa única linha; o sub também. Testado em 390×844 — sem quebra ruim. Não foi preciso reduzir font-size proporcional.
> - **Decisão de não migrar para Opção A:** a leitura visual da Opção B ficou densa o suficiente sem virar "cartão". A garantia respira na buybox sem competir com o CTA.

---

## 🚧 Pendências bloqueantes

Nenhuma. O conteúdo das duas tarefas funciona com placeholders (que entrarão em copy na próxima rodada). Layout pode ser fechado nesta passada.

---

## ❌ Não fazer

- Não tocar em [index.html](../index.html) — escopo continua só PDP
- Não criar badges promocionais (% off, "limitado", "última unidade")
- Não usar ícones cartoon (check verde, estrela amarela)
- Não duplicar conteúdo das features cards já existentes no accordion técnico — ele é **complemento**, não repetição
- Não adicionar carrossel "Outros modelos" no fim (mono-produto)
- Não tocar nas seções já fechadas (hero, cards de transformação, sessão de eventos, etc.)

---

## 📝 Log do Dev (preencher ao final)

**Resumo geral do que foi feito:**
> Adicionada uma nova `<section class="tech-specs" id="ficha-tecnica">` entre Eventos e Fechamento, com três `<details>` (Especificações técnicas em tabela `<dl>`, Funções e modos em grupos com listas 2-col, Instalação e cuidados em listas single-col). Visual amarrado ao padrão do FAQ existente (`+`/`−`, divisores finos, sem caixa). Selo de garantia (Opção B editorial) inserido em duas posições — buybox do hero e closing-card — abaixo do CTA, com `border-top` + `border-bottom` finos. O bullet redundante "Garantia 3 anos" foi removido das duas listas de assurances. Validado em desktop (1280) e mobile (390), sem erros de console.

**Decisões que tomei e que não estavam no brief:**
> 1. **Selo abaixo do CTA, não entre preço e CTA.** O brief deixou em aberto ("dentro da buybox, entre preço e botão. Ou abaixo do botão dependendo de como visualmente respira melhor"). Optei pelo "abaixo": mantém o par preço→CTA intacto e a garantia ancora como reasoning pós-clique mental.
> 2. **Indicador `−` quando aberto.** O FAQ não tem (placeholder estático), mas como o accordion técnico **abre de fato**, faltava o feedback visual. Adicionei via `[open] > summary::after { content: "−" }`.
> 3. **`max-width: 880px` no `.tech-list`.** Em telas grandes, linhas de texto técnico ficariam longas demais. Limitei para preservar leitura, sem alterar a largura do `.tech-header` (que segue editorial).
> 4. **Listas mistas (2-col + single-col).** Brief sugere agrupamento. Para Técnicas e Modos (itens curtos) usei `<ul>` 2-col. Para Recursos e seções de Instalação/Entrega/Cuidados (itens longos), usei `ul.single-col` — 2-col quebraria feio.
> 5. **`role="note"` + `aria-label`** no selo, para leitores de tela contextualizarem o bloco sem precisar ler o texto duas vezes.

**O que ficou pra próxima rodada / dúvidas pro Diretor:**
> - **Copy real do accordion** (todo o conteúdo das três entradas é placeholder técnico realista, mas precisa ser conferido pelo time de produto — dimensões, peso, voltagem, lista de modos pré-programados, etc.).
> - **Copy real do header da ficha técnica** ("Tudo o que importa, sem distração.") — está provisória.
> - **Copy real do selo** ("Deu problema, trocamos a poltrona inteira.") — funciona, mas o time de copy pode querer testar variações na próxima rodada.
> - Como o brief declarou que após essa rodada o **layout está fechado**, a próxima é foco em **copy de todas as seções**.

**Tempo aproximado da execução:**
> ~30 minutos (leitura do brief, exploração do padrão FAQ existente, montagem do CSS dos dois blocos, HTML do accordion + dois selos, validação em desktop + mobile e redação destas notas).
