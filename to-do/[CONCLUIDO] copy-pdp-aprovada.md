# Copy aprovada — PDP Confort Supremo

> **Documento vivo.** Vai sendo atualizado a cada seção fechada. Quando estiver completo, o dev aplica tudo de uma vez no [produto.html](../produto.html).
>
> **Regra dura de copy:** **nunca usar travessão (— ou –)** em nenhuma frase do site. Substituir por ponto final, vírgula, dois pontos ou quebra. É cara de IA.

---

## ✅ Status por seção

| # | Seção | Status |
|---|---|---|
| 0 | Header | **Aprovada** (autonomia do diretor) |
| 1 | Buybox / Hero | **Aprovada** |
| 2 | Envolvimento (Engenharia do toque) | **Aprovada** |
| 3 | A Transformação (4 cards) | **Aprovada** |
| 4 | Experiência (98%) | **Aprovada** |
| 5 | Features interativas (tabs) | **Aprovada** |
| 6 | Cards horizontais (Garantia / Entrega / Atendimento) | **Aprovada** |
| 7 | Depoimentos / Vídeos + Stats | **Aprovada** (com 2 ajustes de layout) |
| 8 | Presença (Mosaico de eventos + Logos) | **Aprovada** (autonomia do diretor) |
| 9 | Entrega (Preparação / Transporte / Chegada) | **Aprovada** (autonomia do diretor) |
| 10 | Sente antes de decidir (Eventos) | **Aprovada** (autonomia do diretor, eventos simulados) |
| 11 | Ficha técnica (accordion) | **Aprovada** (autonomia do diretor) |
| 12 | Closing card + FAQ | **Aprovada** (autonomia do diretor) |
| 13 | Footer (expandido) | **Aprovada** (autonomia do diretor) |

---

## Seção 0 — Header

```
[Confort Supremo Store]    Sobre · Onde Testar · Contato    [⌀ WhatsApp]  [ AGENDAR EXPERIÊNCIA ]
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

1. **Brand:** mantido como já está (`Confort Supremo` + `<span class="brand-suffix"> Store</span>` que some no mobile). Sem mudança.
2. **Menu central:** mantido (`Sobre · Onde Testar · Contato`). Sem mudança.
3. **Adicionar ícone de WhatsApp** entre o menu e o CTA "Agendar Experiência":
   - Ícone circular (~36px) com glyph do WhatsApp em outline fino.
   - Linkado pra `[data-cta="whatsapp"]` (usa o hook centralizado que o dev já implementou).
   - `aria-label="Falar pelo WhatsApp"`.
   - Posição: à esquerda do CTA "Agendar Experiência", separado por margin pequeno.
   - **Mobile:** o ícone WhatsApp **se mantém visível** (não some); o CTA "Agendar Experiência" vira ícone-only (📅 calendário) ou se compacta em `Agendar`.
4. **CTA "Agendar Experiência":** mantido. Continua linkando pra `#testar` (âncora dos eventos).

**Razão estratégica:** o WhatsApp é o funil principal de venda (decisão fechada pelo cliente). Ele precisa estar disponível **sempre** no topo da tela, em todas as resoluções, sem competir com a tese consultiva do CTA "Agendar Experiência" (que leva pro fluxo de evento). Dois caminhos visíveis ao mesmo tempo, sem ambiguidade: **agora** (WhatsApp) ou **presencial** (evento).

**Pendência:** ícone WhatsApp pode ser SVG inline (preferido) ou de uma biblioteca leve (Heroicons, Feather, Lucide). Não usar PNG.

---

## Seção 1 — Buybox / Hero

```
LINHA SUPREMA                                    ← eyebrow (era "STONE EDITION")

Confort Supremo                                  ← nome do produto

A pausa que os melhores se permitem.             ← subtítulo

R$ 25.900                                        ← preço (sem centavos)

COR · BROWN                                      ← label de variante (sem travessão)
[● Brown]                                        ← swatch (qtd final pendente Fábio)

[ FALAR COM ESPECIALISTA ]                       ← CTA único (WhatsApp)

╭─────────────────────────────────────╮
│  3 ANOS · TROCA TOTAL               │          ← selo (já implementado pelo dev)
│  Deu problema, trocamos             │          (copy atual mantida; pode refinar
│  a poltrona inteira.                │           depois pra "Trocamos a poltrona
╰─────────────────────────────────────╯           inteira. Sem perícia, sem espera.")

· Entrega especializada em todo o Brasil
· Atendimento por WhatsApp. Pessoa real, sem bot.    ← travessão removido
```

**Pendências bloqueantes:**
- Rodrigo confirmar se "Linha Suprema" é estratégia (haverá mais linhas?) ou apenas copy de site
- Fábio confirmar quantas cores entram no launch (hoje só foto da grande em marrom)

**Diffs em relação ao estado atual do [produto.html](../produto.html):**
1. Eyebrow `STONE EDITION` → `LINHA SUPREMA`
2. Preço `R$ 25.900,00` → `R$ 25.900` (remover centavos)
3. Label cor `COR · STONE DARK` → `COR · BROWN`
4. Microcopy "Atendimento por WhatsApp — pessoa real, sem bot" → "Atendimento por WhatsApp. Pessoa real, sem bot."

---

## Seção 2 — Envolvimento (Engenharia do toque)

```
ENGENHARIA DO TOQUE                              ← eyebrow (era "ENVOLVIMENTO")

Onde nenhuma tensão escapa.                      ← H2 (era "Massagem que envolve
                                                    de corpo inteiro.")

O sistema lê seu corpo, encontra os pontos       ← lead (NOVO — seção não tinha lead)
certos e adapta a pressão. Você só fecha
os olhos.

  [Cobertura 100%              [Detecção corporal
   das costas]                  automática]
                       🪑
  [Airbag                      [22 pontos
   multipontos]                 de pressão]
```

**Pendência bloqueante:**
- Confirmar com Rodrigo se "Detecção corporal automática" e "Cobertura 100% das costas" são verdade (a arte do Instagram afirma os dois; assumindo que sim)

**Diffs em relação ao estado atual do [produto.html](../produto.html):**
1. Eyebrow `ENVOLVIMENTO` → `ENGENHARIA DO TOQUE`
2. H2 `Massagem que envolve de corpo inteiro.` → `Onde nenhuma tensão escapa.`
3. Adicionar lead novo entre H2 e callouts: `O sistema lê seu corpo, encontra os pontos certos e adapta a pressão. Você só fecha os olhos.`
4. Callout esq. topo `Massagem envolvente` → `Cobertura 100% das costas`
5. Callout dir. topo `De corpo inteiro` → `Detecção corporal automática`
6. Callouts esq. baixo e dir. baixo: mantém (`Airbag multipontos`, `22 pontos de pressão`)

**Observação visual aprovada:** o tratamento desta seção (texto "supremo" gigante de fundo, foto centralizada, callouts editoriais) deve ser replicado em **uma** outra seção da PDP (candidatos: Garantia ou Transporte) para reforçar identidade visual sem virar repetição. Definir na próxima rodada de layout.

---

## Seção 3 — A Transformação

```
A TRANSFORMAÇÃO                                  ← eyebrow

Entra esgotado. Sai inteiro.                     ← H2 ("Sai inteiro." em bold)

O que muda em 20 minutos na Confort Supremo      ← lead (travessão removido)
surpreende quem ainda não experimentou.
Não é relaxamento. É recuperação real do
corpo e da mente.

01  O corpo
    A tensão que você acumulou durante o dia vai embora músculo
    por músculo. Do pescoço aos pés, sem exceção.

02  A mente
    20 minutos de silêncio real. O tipo que não se acha no sofá,
    no quarto ou com fone. A mente para. O corpo segue.

03  O dia seguinte
    Quem tem a Confort Supremo dorme diferente, acorda diferente.
    A diferença não fica na noite. Entra na manhã.

04  O ritual
    Chegar em casa deixa de ser uma rendição. Vira um ritual.
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**
1. Lead: `É recuperação real — do corpo e da mente.` → `É recuperação real do corpo e da mente.` (travessão removido)
2. Card 03 copy: `O ritual muda mais do que a noite — muda a manhã.` → `A diferença não fica na noite. Entra na manhã.` (corrige duplicação semântica com card 04 + remove travessão)
3. Card 04 copy: `O ritual de chegar em casa muda. Você não desaba no sofá. Você se entrega.` → `Chegar em casa deixa de ser uma rendição. Vira um ritual.` (frase mais curta, contraste rendição/ritual, sem clichê de "se entrega")

Cards 01 e 02 mantidos integralmente.

---

## Seção 4 — Experiência (98%)

```
EXPERIÊNCIA                                      ← eyebrow

Não é relaxamento. É o momento em que o corpo    ← H2 ("para de fingir" em bold)
para de fingir que está bem.

98%                                              ← big stat

dos que experimentam dão nota 10.                ← caption (segunda frase removida)
```

À esquerda da seção: vídeo autoplay/loop com a poltrona em ambiente. À direita: o texto.

**Diffs em relação ao estado atual do [produto.html](../produto.html):**
1. Eyebrow, H2 e big stat: **mantidos integralmente.**
2. Caption: `dos que experimentam dão nota 10. O restante dá 9 — e explica exatamente o que mudaria.` → `dos que experimentam dão nota 10.` (corte da segunda frase: removeu fragilidade do argumento + travessão).

**Pendência cross-seção adicionada:** confirmar com Rodrigo/Fábio se o `98%` vem de pesquisa real, contagem de eventos ou estimativa. Precisa estar documentado em algum lugar pra sustentar a afirmação.

---

## Seção 5 — Features interativas (tabs)

```
(sem eyebrow, sem H2, sem lead — decidido manter limpo)

  01  Gravidade Zero
      Inclinação que tira o peso do corpo da equação.

  02  IA Multifuncional
      Ela aprende o que você precisa antes de você pedir.

  03  8 Rolos nas Costas
      Sistema multidimensional. Cobre 100% das costas com pressão adaptativa.

  04  Áudio HiFi Bluetooth
      Som integrado, para concentração ou silêncio.

  05  Modo Sono
      Pra adormecer sem precisar levantar.

  06  Airbag corpo todo
      22 pontos de pressão. Pescoço, ombros, cintura, quadril, pernas e pés.

         [imagem da poltrona à direita, muda conforme tab selecionada]
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**
1. **Remover** a feature `01 Airbag de braço` (e a imagem associada) — coberta pela feature de "Airbag corpo todo"
2. **Renumerar** as features restantes (01 a 06 na nova ordem; mantida a sequência relativa do original)
3. **Adicionar `<p class="feature-desc">`** com a descrição proposta em cada uma das 5 features que hoje só têm título (a feature `IA Multifuncional` já tem e mantém a descrição existente)

Títulos mantidos integralmente: `Gravidade Zero`, `IA Multifuncional`, `8 Rolos nas Costas`, `Áudio HiFi Bluetooth`, `Modo Sono`, `Airbag corpo todo`.

---

## Seção 6 — Cards horizontais (O que vem junto)

```
O que vem JUNTO com a poltrona.                   ← H2 (mantido; "junto" em bold)

[Garantia 3 anos full.]
Em qualquer ocorrência, a poltrona inteira é substituída.
Não a peça. A poltrona. Sem custo adicional, sem burocracia.

[Entrega especializada.]
Transportadora especializada em carga premium. Entrega agendada
no horário que funciona pra você. Cuidamos dela do início ao fim.

[Atendimento premium.]
WhatsApp direto com especialista. Nenhum bot, nenhuma fila.
Pessoas reais, disponíveis antes, durante e depois da compra.

[Instalação plug and play.]                       ← NOVO 4º card
Chega pronta. Conecta na tomada e está em pé. Sem técnico,
sem espera, sem montagem.
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**
1. H2: **mantido** integralmente.
2. Card 01 (Garantia 3 anos full) — copy refinada:
   - `Problema? A poltrona inteira é substituída. Não a peça. A poltrona. Sem análise técnica, sem custo adicional, sem burocracia.`
   - vira: `Em qualquer ocorrência, a poltrona inteira é substituída. Não a peça. A poltrona. Sem custo adicional, sem burocracia.`
   - (Trocou "Problema?" por "Em qualquer ocorrência," e **removeu** "Sem análise técnica,")
3. Card 02 (Entrega especializada) — copy refinada:
   - `Transportadora especializada em carga premium, entrega agendada no horário que funciona para você. Reerguemos ela do início ao fim.`
   - vira: `Transportadora especializada em carga premium. Entrega agendada no horário que funciona pra você. Cuidamos dela do início ao fim.`
   - (Quebrou em duas frases, corrigiu "Reerguemos ela" para "Cuidamos dela")
4. Card 03 (Atendimento premium) — copy refinada:
   - `WhatsApp direto com especialista. Nenhum bot, nenhuma fila. Pessoas reais que conhecem o produto e estão disponíveis durante e depois da compra.`
   - vira: `WhatsApp direto com especialista. Nenhum bot, nenhuma fila. Pessoas reais, disponíveis antes, durante e depois da compra.`
5. Card 04 (**novo**) — `Instalação plug and play.` adicionado como 4º card.
6. **Remover os 3 cards duplicados** que existiam hoje no HTML (placeholder visual). Grid final fica com 4 cards únicos.

---

## Seção 7 — Depoimentos / Vídeos + Stats

```
DEPOIMENTOS                                      ← eyebrow (mantido)

Quem sabe o que é bom, NÃO VOLTA ATRÁS.          ← H2 (mantido; "não volta atrás." em bold)

[Vídeo Gabriela]        [Vídeo placeholder]    [Vídeo placeholder]

[●] Dra. Gabriela       [●] [Nome]             [●] [Nome]
    Schwartzmann            [Profissão ·          [Profissão ·
    Cirurgiã plástica       Cidade]              Cidade]

————————————————————————————————————————————————

98%                     4+                     9 em 10
dos que experimentam    eventos por semana     clientes recomendam
dão nota 10
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

1. **Eyebrow + H2:** mantidos integralmente.
2. **Card 1 (Dra. Gabriela):** legenda simplificada de `Cirurgiã Plástica · "Vida de médico é corrida..."` para apenas `Cirurgiã plástica`. Sem frase descontextualizada.
3. **Card 2 (Confort Supremo · "O lugar onde seu corpo respira"):** **remover** desta seção (a marca não pode ser sua própria testemunha). Vídeo pode ser reaproveitado em outra seção como peça de marca/manifesto.
4. **Card 3 (Cliente):** manter como placeholder estruturado — `[Nome] / [Profissão · Cidade]`. Sem frase descritiva.
5. **Cards duplicados (4, 5, 6):** remover do HTML (eram placeholder visual). Grade final lança com **3 cards únicos** (Gabriela + 2 placeholders estruturados, completados conforme depoimentos reais forem produzidos).
6. **Stats row** (mesma seção testimonials):
   - `Dos que experimentam dão nota 10` → `dos que experimentam dão nota 10` (minúsculo)
   - `Eventos por semana` → `eventos por semana` (minúsculo)
   - `Clientes recomendam` → `clientes recomendam` (minúsculo)
   - Razão: caption começa minúsculo pra ler como continuação do número (padrão consistente com a caption da seção 4).

### ⚠️ Ajustes de layout adicionais (não-copy)

**A) Card de endosso (foto + nome) abaixo do vídeo.** Adicionar logo abaixo de cada vídeo um pequeno "endorsement card" com:
- Foto circular do rosto da pessoa (avatar 40-48px à esquerda)
- Nome em peso medium ou bold
- Profissão · cidade em peso regular, fonte menor

**Função estratégica:** quando o vídeo mostra alguém reconhecível (médica, palestrante, atleta), a presença do rosto fora do vídeo + o nome em texto **captura a atenção** do visitante que está rolando rápido. A pessoa identifica a celebridade antes de clicar play, o que aumenta a chance de o vídeo ser de fato consumido. Conversa direto com a tese "Poltrona das Estrelas".

Pendência: produzir fotos de rosto (PR/oficiais) das pessoas que aparecem nos vídeos. Sem foto real, manter avatar placeholder até a sessão fotográfica.

**B) Bug das captions invisíveis.** O Fábio reportou que as captions atuais (`<div class="testi-caption">`) não estão aparecendo visualmente — provavelmente sobrepostas pelo vídeo ou com `display: none` / `z-index` errado. Dev precisa investigar e corrigir o stacking antes de implementar o "endorsement card" acima.

---

## Seção 8 — Presença (Mosaico de eventos + Logos)

```
PRESENÇA                                          ← eyebrow (mantido)

A Confort Supremo frequenta                       ← H2 (mantido; "mesmos lugares" em bold)
os MESMOS LUGARES que você.

[Mosaico de fotos com overlays atualizados:]
[Trinca Real Estate]      [Tiago Brunet ·         [Pedro Quintanilha ·   [Jogo do Ronaldinho ·
                           Casa de Destino]        Camarim]                Lisboa]

Tesla · Ferrari · Mercedes-Benz · BMW · Porsche
(régua infinita, sem Toyota)
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

1. **Eyebrow + H2:** mantidos integralmente.
2. **Overlays do mosaico:** trocar os atuais `Evento RJ / Evento SP / Evento BH / Evento Brasília` pelos 4 nomes de eventos reais já documentados no Instagram da marca:
   - **Trinca Real Estate**
   - **Tiago Brunet · Casa de Destino**
   - **Pedro Quintanilha · Camarim**
   - **Jogo do Ronaldinho · Lisboa**
3. **Cards duplicados do mosaico (4, 5, 6, 7, 8):** **remover.** Grade final lança com 4 cards únicos (escalável pra 6-8 quando vierem fotos profissionais dos eventos da Verônica Cupini · Legacy Club, Porsche Experience SP etc.).
4. **Logos:** **remover Toyota** da régua. Lista final: `Tesla · Ferrari · Mercedes-Benz · BMW · Porsche`. Razão: Toyota destoa da família visual premium e quebra a tese "frequenta os mesmos lugares". Duplicação pra loop infinito mantida no código.

**Pendência crítica de produção:** as 4 fotos atuais do mosaico provavelmente não correspondem a esses 4 eventos específicos. Precisa mapear quais fotos vêm de quais eventos, OU produzir/conseguir fotos em alta resolução dos eventos reais antes do launch. Se nenhum dos dois for viável, **plano B:** remover overlays completamente até a sessão fotográfica profissional rolar.

---

## Seção 9 — Entrega (Preparação / Transporte / Chegada)

```
ENTREGA                                          ← eyebrow (mantido)

Do nosso espaço ao seu.                          ← H2 (mantido; "exige." em bold)
Com o cuidado que um produto desse nível EXIGE.

Cada etapa pensada para que a chegada seja tão  ← intro (refinada)
cuidadosa quanto a poltrona que está vindo.

01  Preparação
    Inspeção técnica antes do despacho. Embalagem reforçada.
    Rastreamento ativo do início ao fim.

02  Transporte
    Transportadora especializada em carga premium. Seguro de
    transporte incluso. Sem manuseio compartilhado.

03  Chegada
    Entrega agendada no horário que funciona pra você.
    O prazo é confirmado pelo especialista no WhatsApp
    antes da reserva.
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

1. **Eyebrow + H2:** mantidos.
2. **Intro:** `Cada etapa pensada para que a experiência de compra seja tão boa quanto a experiência de uso.` → `Cada etapa pensada para que a chegada seja tão cuidadosa quanto a poltrona que está vindo.` (mais específico, menos genérico publicitário)
3. **Card 01 (Preparação):** removida a frase `Documentação de envio.` (operacional demais, não premium). Resto mantido.
4. **Card 02 (Transporte):** `Sem compartilhamento com cargas inadequadas.` → `Sem manuseio compartilhado.` (mais elegante, menos defensivo)
5. **Card 03 (Chegada):** enxugado de `O prazo estimado para o seu CEP é confirmado pelo especialista no WhatsApp antes da reserva.` para `O prazo é confirmado pelo especialista no WhatsApp antes da reserva.` (cortes de "estimado para o seu CEP" porque "prazo" já implica isso). Trocou também `para você` por `pra você` na frase anterior (oralidade premium).

---

## Seção 10 — Sente antes de decidir (Eventos)

```
ONDE TESTAR                                      ← eyebrow (NOVO — seção não tinha)

Sente ANTES DE DECIDIR.                          ← H2 (mantido; "antes de decidir." em bold)

Nos próximos eventos, a poltrona vai até você.
Escolha a data mais perto.

Porsche Experience São Paulo      São Paulo · 28/05/2026       [Reservar]
Trinca Real Estate · Edição Rio   Rio de Janeiro · 12/06/2026  [Reservar]
Tiago Brunet · Casa de Destino    São Paulo · 25/06/2026       [Reservar]
Legacy Club · Beauty Edition      Curitiba · 10/07/2026        [Reservar]
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

1. **Adicionar eyebrow:** `ONDE TESTAR` acima do H2 (consistência editorial com as outras seções; hoje a seção começa direto no H2).
2. **H2 + intro:** mantidos integralmente.
3. **4 cards de evento — substituir pelos eventos simulados** abaixo (todos os 4 cards atuais são duplicação do mesmo "Porsche Experience São Paulo · 18/03/2026"):
   - **Porsche Experience São Paulo** — São Paulo · 28/05/2026
   - **Trinca Real Estate · Edição Rio** — Rio de Janeiro · 12/06/2026
   - **Tiago Brunet · Casa de Destino** — São Paulo · 25/06/2026
   - **Legacy Club · Beauty Edition** — Curitiba · 10/07/2026
4. **CTA do botão:** `Reservar Meu Lugar` → `Reservar lugar` (mais curto, ainda direto; "meu" é redundante porque o botão está vinculado à linha de cada evento)

**Pendência:** quando o cliente passar a agenda real, é trocar nomes/datas/cidades — estrutura está pronta. Os eventos simulados foram escolhidos pra refletir o universo "Poltrona das Estrelas" já documentado no Instagram (palestras de coaching, real estate, beauty, automotivo premium). Para apresentação ao cliente, ficam realistas e diversos.

---

## Seção 11 — Ficha técnica (accordion)

```
FICHA TÉCNICA                                    ← eyebrow (mantido)

Tudo o que importa,                              ← H2 (mantido; "sem distração." em bold)
SEM DISTRAÇÃO.

▸ Especificações técnicas
▸ Funções e modos de massagem
▸ Instalação e cuidados
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

1. **Eyebrow + H2:** mantidos integralmente.
2. **Conteúdo dos 3 accordions:** mantido como o dev implementou (já está bom como copy técnica). Único ajuste:
   - Em "Instalação e cuidados" → "Instalação" → primeiro bullet, hoje é `Plug and play — pronta para usar ao ligar na tomada`. Tem travessão. Trocar por `Plug and play. Pronta para usar ao ligar na tomada.`

**Pendência:** todos os números (dimensões, peso, voltagem, potência etc.) são placeholders sensatos. Substituir pelos dados reais da poltrona quando o Rodrigo passar a ficha técnica oficial.

---

## Seção 12 — Closing card + FAQ

```
O CONVITE                                        ← eyebrow (NOVO — era "O FECHAMENTO")

O dia que você                                   ← H2 (mantido; "parou de adiar." em bold)
PAROU DE ADIAR.

A Confort Supremo está esperando.                ← lead (mantido)
A pergunta é quando você vai parar de imaginar
e começar a sentir.

FAQ (com respostas novas):

▸ Como funciona a entrega?
  A poltrona sai do nosso espaço em embalagem reforçada e viaja em
  transportadora especializada em carga premium. Você agenda a entrega
  no horário que funciona pra você. Atendemos todo o Brasil. O prazo é
  confirmado pelo especialista no WhatsApp antes de fechar a reserva.

▸ A garantia cobre o quê exatamente?
  Cobre tudo. Em qualquer ocorrência, dentro de 3 anos, trocamos a
  poltrona inteira. Não a peça, não a câmara de ar, não o motor.
  A poltrona. Sem custo adicional, sem burocracia, sem fila.

▸ Posso parcelar?
  Sim. As condições de pagamento são tratadas diretamente com o
  especialista pelo WhatsApp, incluindo PIX, transferência e parcelamento
  em cartão.

▸ Como funciona o teste presencial?
  A Confort Supremo está presente em eventos premium (Porsche Experience,
  Trinca Real Estate, Casa de Destino do Tiago Brunet, entre outros) onde
  você pode sentar e experimentar antes de decidir. A agenda está na seção
  "Onde Testar". Não trabalhamos com showroom fixo.

▸ Por que não encontro em marketplaces?
  Porque a Confort Supremo não está em marketplaces. Vendemos diretamente,
  com importação própria, atendimento humano e garantia full de 3 anos.
  Quem chega à marca, chega à marca. Não a um catálogo.

[Closing card aside:]
Confort Supremo
A pausa que os melhores se permitem.

R$ 25.900                                        ← sem centavos
[ FALAR COM ESPECIALISTA ]
[Selo 3 anos · Troca total]
· Entrega especializada
· Plug and play                                  ← antes era "Montagem inclusa"
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

1. **Eyebrow:** `O Fechamento` → `O Convite`. Razão: "fechamento" é vocabulário interno de venda (soa como "fim de funil"); "convite" é vocabulário do cliente (acolhedor, premium, não-pressionado).
2. **H2 + lead:** mantidos integralmente.
3. **5 perguntas do FAQ:** títulos mantidos. **Adicionar respostas** conforme bloco acima (atualmente as perguntas são só botões sem resposta — placeholder estrutural; vira FAQ funcional com schema.org `<details>/<summary>` ou padrão similar).
4. **Closing card aside:**
   - Preço `R$ 25.900,00` → `R$ 25.900` (sem centavos, consistente com a buybox)
   - Assurance label `Montagem inclusa` → `Plug and play` (corrige inconsistência: a poltrona NÃO precisa de montagem — é plug and play, conforme accordion técnico)
   - Resto mantido (subtitle, CTA, selo, entrega especializada)

**Observação técnica para o dev:** as respostas do FAQ devem entrar dentro de `<details>` ou expandir via JS com `aria-expanded`. Isso é crítico pra SEO e indexação por LLM (era um dos requisitos do Fernando na reunião de 24/03/2026). Conteúdo das respostas precisa estar no HTML estático, não carregado via fetch.

---

## Seção 13 — Footer (expandido)

```
┌──────────────────────────────┬───────────────────┬───────────────────┬──────────────────────────┐
│  CONFORT SUPREMO STORE       │  NAVEGAÇÃO        │  SUPORTE          │  FALE COM A MARCA        │
│  O conforto que você         │                   │                   │                          │
│  conquistou.                 │  Sobre            │  Atendimento      │  [⌀ WhatsApp]            │
│                              │  Onde Testar      │  FAQ              │  [⌀ Instagram]           │
│  Importadora oficial da      │  Garantia         │  Manual           │  [⌀ YouTube]             │
│  poltrona que está em        │  Política de      │  Trocas e         │                          │
│  camarins, salões e          │  Privacidade      │  devoluções       │  Atendimento humano      │
│  eventos de quem já não      │                   │                   │  Seg a sex · 9h às 19h   │
│  tem mais o que provar.      │                   │                   │  Sáb · 9h às 14h         │
│                              │                   │                   │                          │
│  Direto da marca. Garantia   │                   │                   │                          │
│  full de 3 anos com troca    │                   │                   │                          │
│  total.                      │                   │                   │                          │
└──────────────────────────────┴───────────────────┴───────────────────┴──────────────────────────┘

PAGAMENTO ACEITO
[PIX] [Visa] [Mastercard] [Amex] [Elo] [Boleto]

────────────────────────────────────────────────────────────────────────────────
© 2026 Confort Supremo Store. CNPJ XX.XXX.XXX/0001-XX. Todos os direitos reservados.
Feito para durar. Como o descanso que você merece.
```

**Diffs em relação ao estado atual do [produto.html](../produto.html):**

### Estrutura geral

1. **Layout:** ampliar de 3 colunas pra **4 colunas** no desktop. Empilha em coluna única no mobile (`@media max-width: 768px`).
2. **Coluna 1 — Identidade da marca** (expansão):
   - Brand + tagline `O conforto que você conquistou.` → **mantidos.**
   - **Adicionar texto institucional** (novo) abaixo da tagline:
     > **Importadora oficial da poltrona que está em camarins, salões e eventos de quem já não tem mais o que provar.**
     >
     > **Direto da marca. Garantia full de 3 anos com troca total.**
   - Tamanho do texto: `--fs-sm`, peso regular, em `--color-text-muted`.
3. **Coluna 2 — Navegação institucional** (expansão):
   - Mantém os 2 atuais: `Sobre`, `Onde Testar`.
   - **Adicionar (mockados, `href="#"`):** `Garantia`, `Política de Privacidade`.
   - Remove `Contato` daqui (substituído pelos ícones da coluna 4 e por `Atendimento` na coluna 3).
   - Título da coluna: `Footer Menu` → `Navegação`.
4. **Coluna 3 — Suporte** (nova):
   - Itens (mockados, `href="#"`):
     - `Atendimento`
     - `FAQ` (âncora pra `#agendar` ou seção do FAQ)
     - `Manual`
     - `Trocas e devoluções`
   - Razão de remover `WhatsApp direto` desta coluna: redundante com os ícones da coluna 4 (que já têm WhatsApp em destaque visual). Em luxo, mesma ação repetida em duas colunas vira poluição.
5. **Coluna 4 — Fale com a marca** (nova, substitui a antiga coluna "Redes"):
   - **Ícones grandes** (~32px) com `aria-label` em vez de texto: **WhatsApp · Instagram · YouTube**.
   - WhatsApp linka via `[data-cta="whatsapp"]` (mesmo hook centralizado).
   - Instagram: `https://www.instagram.com/confortsupremo/` (link real, esse é canal vivo).
   - YouTube: `#` (placeholder mockado por enquanto).
   - **Adicionar abaixo dos ícones, em texto pequeno:**
     > **Atendimento humano**
     > **Seg a sex · 9h às 19h**
     > **Sáb · 9h às 14h**
   - Tamanho: `--fs-xs`, peso regular.
   - (Esses horários são mock pra apresentação; pedir confirmação ao cliente.)

### Faixa de pagamento (nova)

6. **Adicionar uma faixa horizontal** abaixo das 4 colunas e acima do copyright, com:
   - Label discreto à esquerda: `Pagamento aceito` (em `--fs-xs`, uppercase, letter-spacing `0.18em`, cor `--color-text-dim`).
   - À direita, 6 ícones de bandeiras de pagamento, todos mockados (SVG inline preferido): **PIX · Visa · Mastercard · Amex · Elo · Boleto**.
   - Estilo: ícones em tom único (linha fina ou silhueta monocromática em `--color-text-muted`), não as bandeiras coloridas oficiais. Razão: bandeiras coloridas oficiais destoam da paleta editorial — viram "loja popular". Em luxo, sempre monocromático.

### Copyright + linha final

7. **Linha do copyright:**
   - Atual: `© 2026 Confort Supremo Store. Todos os direitos reservados.`
   - Proposta: `© 2026 Confort Supremo Store. CNPJ XX.XXX.XXX/0001-XX. Todos os direitos reservados.`
   - O CNPJ entra como placeholder até o Fábio passar o número real. Para apresentação, fica como `CNPJ XX.XXX.XXX/0001-XX`.
8. **Tagline final:**
   - Atual: `Feito para durar — assim como o descanso que você merece.`
   - Proposta: `Feito para durar. Como o descanso que você merece.` (travessão removido)

### Pendências cross-seção (adicionar à lista global)

- **Cliente:** CNPJ oficial para footer
- **Cliente:** horários reais de atendimento
- **Cliente:** URL do canal YouTube (se houver)
- **Equipe legal:** páginas institucionais (Política de Privacidade, Trocas e devoluções, Garantia) — quando criar, basta trocar `href="#"` pelo link real. Estrutura visual do footer não muda.

---

## ✅ Todas as seções da PDP estão aprovadas

Não há mais seções pendentes. Próxima rodada: brief consolidado de execução para o dev aplicar todas as mudanças de copy de uma vez.

---
- **Seção 6 — Cards horizontais (Garantia / Entrega / Atendimento)**
- **Seção 7 — Depoimentos / Vídeos**
- **Seção 8 — Stats (98% / 4+ / 9 em 10)**
- **Seção 9 — Mosaico de eventos ("frequenta os mesmos lugares que você")**
- **Seção 10 — Logos**
- **Seção 11 — Preparação / Transporte / Chegada**
- **Seção 12 — Sente antes de decidir (Porsche Experience)**
- **Seção 13 — Closing card**
- **Seção 14 — FAQ (com SEO + LLM indexing)**
- **Seção 15 — Footer**

---

## 🚧 Pendências cross-seção (acumulando para resolver de uma vez)

- **Rodrigo:** "Linha Suprema" é estratégia de coleção (haverá mais linhas/edições) ou apenas copy do site?
- **Rodrigo:** confirmar verdade técnica de "Detecção corporal automática" e "Cobertura 100% das costas"
- **Fábio:** quantas cores entram no launch (1 ou mais)?
- **Fábio:** existe estoque imediato para comunicar "Pronta entrega" próximo ao preço?
- **Equipe de copy:** copy do selo de garantia pode ser refinada de "Deu problema, trocamos a poltrona inteira." para "Trocamos a poltrona inteira. Sem perícia, sem espera." (sugestão do diretor, baixa prioridade)
- **Rodrigo/Fábio:** confirmar fonte do `98%` exibido na seção Experiência (pesquisa real, contagem de eventos, estimativa). Se não houver fonte documentada, considerar substituir por outra métrica verificável.
- **Rodrigo/Fábio:** confirmar fontes dos demais stats da seção 7: `4+ eventos por semana` e `9 em 10 clientes recomendam`. Mesma regra do `98%` — precisa documentação.
- **Produção:** fotos de rosto (PR/oficiais) das pessoas que aparecem nos vídeos de depoimento (Dra. Gabriela e demais), para alimentar o "endorsement card" da seção 7.
- **Cliente:** CNPJ oficial para footer (hoje placeholder `XX.XXX.XXX/0001-XX`)
- **Cliente:** horários reais de atendimento ao cliente (mock atual: Seg-Sex 9h-19h, Sáb 9h-14h)
- **Cliente:** URL do canal YouTube (se houver)
- **Equipe legal:** páginas institucionais (Política de Privacidade, Trocas e devoluções, Garantia, Manual). Estrutura visual do footer está pronta — basta trocar `href="#"` pelos links reais quando as páginas existirem.

---

## 📝 Notas do Dev (rodada de execução)

**Resumo geral:**
> Implementadas as 14 seções (S0 a S13) em uma única rodada. Todas as cópias e diffs do brief foram aplicados em [produto.html](../produto.html), incluindo refatorações estruturais (remoção de cards duplicados em Cards horizontais, Depoimentos, Presença e Eventos; conversão do FAQ para `<details>` funcional; expansão do footer de 3 para 4 colunas com faixa de pagamento). Adicionado também o ícone WhatsApp no header (SVG inline em outline) com `[data-cta="whatsapp"]` para aproveitar o hook centralizado.

**Decisões / observações por seção:**

- **S0 — Header:** ícone WhatsApp em SVG inline (não CDN) com `aria-label="Falar pelo WhatsApp"`. Wrappei o ícone + CTA dentro de um `.header-actions` (flex gap pequeno). O CTA "Agendar Experiência" passou a apontar para `#testar` (âncora dos eventos, conforme intenção do brief). No mobile (≤640px), o texto longo do botão é trocado por "Agendar" via `<span class="btn-full">` / `<span class="btn-mobile">`, e o padding do botão reduz. O ícone permanece visível em todas as resoluções.
- **S1 — Buybox:** todos os 4 diffs aplicados (eyebrow, preço sem centavos, cor Brown, microcopy WhatsApp com ponto). Removi o comentário HTML da alternativa de copy "A poltrona dos bastidores" para não poluir.
- **S2 — Envolvimento:** eyebrow, H2 e lead conforme brief. Para os callouts, mantive a estilística existente (linha 1 + linha 2 com `<strong>` ou `<em>`). "Cobertura 100% das costas" ficou com `<strong>100%</strong>`, e "Detecção corporal automática" com `<em>automática</em>`. Reduzi o `margin-bottom` do H2 de `var(--space-4)` para `var(--space-3)` para acomodar o lead novo sem inflar a seção.
- **S3 — Transformação:** todos os 3 diffs aplicados.
- **S4 — Experiência:** caption cortada para uma única linha (removida a segunda frase + o `<br>`).
- **S5 — Features:** remoção do card "Airbag de braço" (era data-feature="01"). Renumerei os data-feature attrs e as imagens correspondentes para manter alinhamento sequencial 01-06. Adicionei `<p class="feature-desc">` em todos os 6 cards. O primeiro card (Gravidade Zero) ficou com `is-active` e a primeira `<img>` correspondente também.
- **S6 — Cards horizontais:** grid limpo (4 cards únicos, sem duplicação). Card 4 "Instalação plug and play" usa FOTO_20 como placeholder (pode trocar quando a imagem oficial chegar).
- **S7 — Depoimentos:**
  - Removidos os 3 cards duplicados + o card "Confort Supremo" (auto-testemunho).
  - Wrappei cada video card em `.testi-item` que contém `.testi-card` + `.endorsement` (avatar circular placeholder + nome + profissão · cidade).
  - **Fix do bug de caption invisível:** subi `z-index: 4` no `.testi-caption` (estava abaixo do `.testi-play` que tem z-index 3) e adicionei `pointer-events: none` para não bloquear o play. Caption simplificada conforme brief (Gabriela: "Cirurgiã plástica" sem frase descontextualizada; placeholders: `[Nome]` + `[Profissão · Cidade]`).
  - Card 3 ficou como placeholder estrutural sem vídeo (só avatar + nome placeholder), já que só sobraram 2 vídeos únicos após remover o auto-testemunho. Quando depoimentos reais forem produzidos, é só preencher.
  - **Stats:** removi `text-transform: uppercase` e o `letter-spacing` do `.stat-label` para que as captions em minúscula leiam como continuação do número (consistente com `.stat-caption` da seção 4). Aumentei o `font-size` de `--fs-xs` para `--fs-sm`.
- **S8 — Presença:** overlays atualizados, cards duplicados removidos (sobraram os 4 únicos). Toyota removida do logos-track (lista limpa: Tesla · Ferrari · Mercedes-Benz · BMW · Porsche, com duplicação preservada para o loop infinito).
- **S9 — Entrega:** intro reescrita, card 01 sem "Documentação de envio", card 02 com "Sem manuseio compartilhado", card 03 enxugado.
- **S10 — Eventos:** adicionado eyebrow "Onde testar" acima do H2. Substituí os 4 cards duplicados pelos 4 eventos simulados. Botão CTA: "Reservar lugar".
- **S11 — Ficha técnica:** travessão substituído por ponto no bullet "Plug and play".
- **S12 — Closing + FAQ:**
  - Eyebrow trocado para "O Convite".
  - **FAQ convertido para `<details>/<summary>` funcionais.** Atualizei o CSS de `.faq-question` (button) para `.faq-item > summary` (com o mesmo `+` / `−` do accordion técnico). Adicionei `.faq-answer` para o corpo (max-width 640px, `color: --color-text-muted`). Todas as 5 respostas estão no HTML estático (não fetch), pronto pra crawler/LLM.
  - Closing card: preço sem centavos, "Montagem inclusa" → "Plug and play". Removi o comentário HTML da alternativa de copy.
- **S13 — Footer:**
  - Grid expandido de 3 para 4 colunas (`1.4fr 1fr 1fr 1fr`).
  - Coluna 1: brand + tagline + 2 parágrafos institucionais (`.footer-about` com `<strong>` que herda cor mais clara).
  - Coluna 2 "Navegação": Sobre, Onde Testar, Garantia (#), Política de Privacidade (#).
  - Coluna 3 "Suporte": Atendimento, FAQ (âncora #agendar), Manual, Trocas e devoluções.
  - Coluna 4 "Fale com a marca": 3 ícones SVG inline (WhatsApp via `[data-cta="whatsapp"]`, Instagram com URL real, YouTube placeholder) + bloco `.footer-hours` com "Atendimento humano" + horários.
  - **Faixa de pagamento** (`.payments-strip`): label "Pagamento aceito" à esquerda + 6 chips monocromáticos (PIX, Visa, Mastercard, Amex, Elo, Boleto). Cada chip é um `<span>` com borda 1px e texto em uppercase — fica em paleta editorial (não bandeira colorida), conforme brief.
  - Copyright: CNPJ placeholder `XX.XXX.XXX/0001-XX`.
  - Tagline final: "Feito para durar. Como o descanso que você merece." (travessão removido).
  - Mobile (≤768px): grid colapsa para 1 coluna.

**Audit final de travessões:**
> Varredura de `—` e `–` no arquivo. Todas as ocorrências restantes são:
> 1. **Comentários CSS e HTML** (linhas 37, 40-48, 56, 284, 479, 783, 914, 1414, 1479, 1486, 1658, 1883, 1928, 1973, 2007). Não são copy visível; deixei intactos para não tocar em documentação técnica.
> 2. **Marcadores tipográficos `::before`** (linha 417 `.assurances span::before { content: "—" }` e linha 1064 `.tech-content li::before { content: "— " }`). São glifos decorativos (substituem bullets), não frases. Decidi manter como marcador visual. Se o Diretor preferir trocar por `·` ou `•`, é uma alteração trivial de duas linhas de CSS. Não há nenhum travessão em copy textual visível ao usuário.
> 3. **`<title>` da página** e `alt` de imagens: corrigidos (todos os "Confort Supremo —" viraram "Confort Supremo ·", `aria-label` do vídeo da Experiência reescrito sem travessão).

**Pendências bloqueantes não resolvidas (do brief):**
> Mantidas todas as pendências listadas em "🚧 Pendências cross-seção" acima. Nenhuma foi resolvida nesta rodada (a maior parte depende do cliente, equipe de copy ou produção).

**Tempo aproximado da execução:**
> ~90 minutos (leitura completa do brief, mapeamento dos pontos de toque em produto.html, execução em 14 seções, audit final de travessões, redação destas notas).
