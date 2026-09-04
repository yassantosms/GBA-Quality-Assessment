---
name: flow-quality-assessment
version: "2026-09-04"
canonical_repo: "https://github.com/yassantosms/GBA-Quality-Assessment"
canonical_path: "flow-quality-assessment"
canonical_url: "https://github.com/yassantosms/GBA-Quality-Assessment/tree/main/flow-quality-assessment"
description: "Roda um Quality Assessment de fluxos de produto do Nubank em 3 pilares complementares — Craft (Magic), User Experience Impact e Business Impact (tamanho) — e gera um dashboard HTML em inglês com nota por parâmetro, rationale auditável, evidência do fluxo (vídeo ou prints) ao lado dos main issues, e o mapa de quadrantes Star / Hidden Gem / Table Stakes / Skip. O fluxo entra via link do Figma, screen recording/vídeo da jornada (preferido para apuração), ou prints/telas. Cada parâmetro recebe uma nota que o Claude atribui lendo o fluxo contra a rubrica-âncora embutida (Anexo A). Pilar 1 e 2 usam escala 1–5; Pilar 3 usa 1/3/5 (target). Craft e User Experience Impact cortam no 3 para posicionar o fluxo no mapa; Business Impact vira o tamanho do ponto. Roda parcial: só Craft (sem inputs extras), + User Experience Impact (com JTBDs), + Business Impact (com métricas). Antes de cada rodada, consulta o GitHub canônico se a skill local está atualizada. Suporta o mesmo fluxo em mais de um geo (BR/MX/CO) para comparativo. Escalável entre times: JTBDs e métricas são fornecidos pelo usuário; a rubrica é fixa. Use quando pedirem para avaliar a qualidade de um fluxo, rodar 'quality assessment', 'flow assessment', 'avaliar um fluxo', pontuar craft/UX/business de uma tela/jornada/Figma, ou posicionar fluxos no mapa de quadrantes. Trigger: 'quality assessment', 'avaliar fluxo', 'nota de qualidade do fluxo', 'craft score', 'star/hidden gem/table stakes/skip', link do Figma + JTBDs/metas, upload de telas/vídeo."
---

## O que esta skill faz

Avalia a qualidade de um fluxo de produto do Nubank em **três pilares complementares** e entrega um **dashboard HTML em inglês** (padrão) em duas camadas: uma **folha-resumo** (médias por pilar + evidência do fluxo + main issues + mapa de quadrantes — pronta para stakeholders e multi-geo) e, abaixo, o **detalhe auditável** por parâmetro com rationale. O fluxo se posiciona no **mapa de quadrantes** (Star / Hidden Gem / Table Stakes / Skip).

**Nomes oficiais dos pilares (use sempre estes no dashboard e na comunicação):**
- Pilar 1 → **Craft** (eixo Magic)
- Pilar 2 → **User Experience Impact** — **não** chame de “Customer Value”
- Pilar 3 → **Business Impact** — **não** chame de “Business Metrics”

**O diferencial:** a nota de cada parâmetro é atribuída por mim (Claude), lendo o fluxo e comparando o que observo com a **rubrica-âncora** de cada nível (1 a 5), embutida neste arquivo no **Anexo A**. Não é um checklist mecânico: eu leio as telas, entendo a jornada e justifico cada nota contra a descrição do nível correspondente.

**Escalável entre times:** a rubrica (Anexo A) é fixa e vale para qualquer time. O que varia por produto/BU são os **JTBDs** (alimentam o Pilar 2) e as **métricas de negócio** (alimentam o Pilar 3) — e esses dois vêm do usuário no início da sessão. Por isso a skill não guarda JTBDs nem métricas: ela pergunta.

## Version check (obrigatório a cada execução)

**Antes de coletar inputs ou pontuar**, a skill **deve** conferir se a cópia local está alinhada com o repositório canônico:

- **Repo:** https://github.com/yassantosms/GBA-Quality-Assessment/tree/main/flow-quality-assessment
- **Raw SKILL.md:** https://raw.githubusercontent.com/yassantosms/GBA-Quality-Assessment/main/flow-quality-assessment/SKILL.md
- **Raw VERSION (se existir):** https://raw.githubusercontent.com/yassantosms/GBA-Quality-Assessment/main/flow-quality-assessment/VERSION

### Como checar
1. Leia o campo `version` do frontmatter deste `SKILL.md` local (hoje: `2026-09-04`) e/ou o arquivo local `VERSION`, se houver.
2. Busque a versão remota (`gh api`, `curl`, ou WebFetch) no `SKILL.md` / `VERSION` do GitHub acima.
3. Compare:
   - Se **remoto == local** → siga normalmente (pode mencionar em uma linha que a skill está atualizada).
   - Se **remoto > local** (versão ou conteúdo mais novo) → **atualize a skill local** copiando `SKILL.md`, `README.md`, `VERSION` e `assets/` do repo para `~/.cursor/skills/flow-quality-assessment/` (ou o path ativo da skill), avise a pessoa (“Updated skill from GitHub to version X”), **releia** o `SKILL.md` atualizado e só então continue o assessment.
   - Se não conseguir acessar o GitHub → avise que o version check falhou e pergunte se quer seguir com a cópia local; não bloqueie a rodada.

Nunca invente que está atualizado sem ter consultado o remoto nesta sessão.

## Os três pilares

| Pilar | Nome | Papel no mapa | Escala | Nº de parâmetros |
|---|---|---|---|---|
| 1 | **Craft** | Eixo horizontal → **Magic** | 1–5 | 6 |
| 2 | **User Experience Impact** | Eixo vertical → **User Experience Impact** | 1–5 | 3 |
| 3 | **Business Impact** | **Tamanho do ponto** | 1 / 3 / 5 | 1 por métrica informada |

A rubrica completa de cada parâmetro (a descrição de cada nível de nota) está no **Anexo A**. Ela é a fonte de verdade — sempre atribua a nota casando o que você observa no fluxo com o texto do nível. Nunca invente parâmetros novos nem renomeie os existentes. **Não use os nomes legados “Customer Value” ou “Business Metrics”** no dashboard nem na fala com a pessoa.

## Os inputs do usuário

Antes de avaliar, apresente ao usuário o que a skill precisa e **o que ela consegue rodar com o que ele tiver** (não é obrigatório ter os três para começar). Nunca invente inputs que faltam — peça ou marque como não avaliado.

### O que cada pilar exige

| Pilar | Input necessário | Roda sem ele? |
|---|---|---|
| **Craft** (Magic) | Só o fluxo (Figma, vídeo e/ou prints) | ✅ Sim — Craft roda sozinho |
| **User Experience Impact** | Fluxo **+ JTBDs** | ❌ Precisa dos JTBDs |
| **Business Impact** (tamanho) | **Métricas** (nome + target + stretch + reported) | ❌ Precisa das métricas |

**No início, diga isso ao usuário** (em PT ou EN conforme a língua da conversa), e **sempre mencione o valor do vídeo**:

> Posso rodar só o Craft agora se você me der o fluxo. Para User Experience Impact preciso dos JTBDs, e para Business Impact das métricas (target, stretch e realizado).
>
> **Com um vídeo/screen recording da jornada a apuração fica ainda melhor** — dá para ver motion, loading, overlaps, timing e o caminho real ponta a ponta (além de Figma ou prints). Me diz o que você já tem.

Rode com o que houver e deixe claro no dashboard o que ficou de fora.

### 1. O fluxo — via Figma, **vídeo**, ou prints
É o objeto avaliado nos Pilares 1 e 2. Três caminhos (podem combinar):

- **Vídeo / screen recording (fortemente recomendado para apuração):** o usuário envia um `.mov` / `.mp4` / similar da jornada. Extraia frames (ex.: AVFoundation no macOS se `ffmpeg` não estiver disponível) e leia a sequência temporal. O vídeo é o melhor input para **Interaction, Motion & Feedback**, **Performance & Resilience** (loading/overlaps), e para flagar inconsistências que prints estáticos escondem. Embutir o vídeo no dashboard (coluna Evidence).
- **Figma (preferido para componentes/tokens):** o usuário cola o(s) link(s) do arquivo/frames. Use o **Figma MCP** (conector da sessão) para inspecionar cada tela. Isso habilita o que print/vídeo sozinhos não dão:
  - **detectar componentes NuDS V3** de fato usados (nomes de componente, variantes);
  - **flagar componentes deprecados** — cruze com o NuDS vigente (ver "Fonte de verdade para NuDS v3"); a lista de deprecados vem da fonte viva, não é congelada aqui;
  - **checar localização** por geo (ver tabela em "Localização");
  - ler tokens, espaçamento e tipografia reais em vez de inferir do pixel.
  Se houver referência de motion/protótipo, use-a para os parâmetros de Interaction, Motion & Feedback.
- **Prints/telas:** o usuário sobe imagens/PDF. Avalie pelo observável. Sem Figma, a detecção de componente/token e o flag de deprecados ficam **limitados ao que é visível** — pontue com base na aparência e marque no rationale quando algo depender de inspeção de componente. Embutir um print representativo (ou carrossel curto) na coluna Evidence do dashboard.

Em todos os casos, leia de verdade cada tela/frame e entenda a jornada ponta a ponta antes de pontuar.

### 2. Os JTBDs do fluxo (para o Pilar 2 — User Experience Impact)
Peça o JTBD principal e os secundários, se houver. Os JTBDs podem mudar de fluxo para fluxo — pergunte a cada assessment, mesmo que já tenha vindo antes. Sem JTBDs, não pontue o Pilar 2; rode Craft (e Business Impact, se houver métricas) e marque **User Experience Impact** como não avaliado.

### 3. As métricas de negócio (para o Pilar 3 — Business Impact)
Para **cada** métrica, peça: **nome** (ex.: % activation, Conversion (eligible/active), MAU/MEAU, Recurrent buyers/Engagement, Market share, PV/AUC/AUM, IFP/NNM — lista não-exaustiva, adaptável por time), **target**, **stretch target** e **número reportado** (realizado). Sem target e reported, marque o Pilar 3 (**Business Impact**) como não avaliado. Use exatamente os números informados; nunca estime metas nem realizados.

### Multi-geo (comparativo, opcional)
Um mesmo fluxo pode existir em mais de uma região (BR/MX/CO) com implementações diferentes. Se o usuário fornecer o fluxo para mais de um geo, avalie cada geo separadamente e mostre o comparativo lado a lado (scores por pilar e posição no mapa). Mantenha simples: uma avaliação por geo, plotadas no mesmo mapa. Não force multi-geo quando o usuário só trouxe um.

## Fonte de verdade para NuDS v3 (não congelar na skill)

Vários parâmetros de Craft (Navigation & Flow Logic, Layout & Surface Craft, Brand & Content Compliance) e a rubrica em geral fazem referência ao **NuDS v3** (componentes, tokens, patterns) e às **Magic App guidelines**. Essas regras mudam com o tempo, então **não estão embutidas nesta skill**. Para avaliar aderência ao NuDS v3:

- Consulte o Nu Design System via o conector disponível na sessão (**NuDS / zeroheight MCP** ou **Glean**, que indexa a documentação interna).
- **Se o MCP do NuDS não estiver disponível na sessão**, **peça à pessoa para instalar/conectar** antes de seguir (ou ofereça rodar parcial só com o observável). Use este link oficial:
  - **NuDS v3 — Nu Design System (MCP):** https://nuds.nu.com.br/46f3733aa/p/40ba9d-nuds-v3--nu-design-system
  - Mensagem sugerida: *"Para cruzar componentes, tokens e deprecados com o NuDS vivo, conecte o MCP do NuDS v3: https://nuds.nu.com.br/46f3733aa/p/40ba9d-nuds-v3--nu-design-system — depois me avisa que eu retomo. Se preferir, sigo agora só pelo que dá para ver no fluxo e marco os parâmetros NuDS como subject to validation."*
- Se a pessoa não puder/não quiser conectar (SSO, sem acesso, etc.), **sinalize** e avalie apenas com base no que é observável no fluxo, marcando os parâmetros dependentes de NuDS como **"subject to NuDS v3 validation"** no rationale. Não invente regras do design system.

## Localização (regra fixa, por geo)

Ao inspecionar o fluxo (sobretudo via Figma), cheque se moeda, idioma e formato de número batem com o geo. Diferente do NuDS, isto é estável e vale como referência embutida:

| Geo | Idioma | Moeda | Símbolo | Separador decimal / milhar | Exemplo |
|---|---|---|---|---|---|
| **BR** | pt-BR | BRL | R$ | vírgula decimal, ponto milhar | R$ 1.234,56 |
| **MX** | es-MX | MXN | $ | ponto decimal, vírgula milhar | $1,234.56 |
| **CO** | es-CO | COP | $ | vírgula decimal, ponto milhar (centavos geralmente omitidos) | $ 1.234 |

Divergências (idioma trocado, moeda errada, formato numérico do geo errado, data em formato inesperado) entram como evidência em **Brand & Content Compliance** e, quando afetam entendimento, em **Customer Clarity**. Cite a tela no rationale.

## Componentes deprecados (via NuDS vivo)

Quando o fluxo vier por Figma, liste os componentes NuDS V3 detectados e **cruze com a documentação vigente do NuDS** (conector NuDS/zeroheight ou Glean) para flagar deprecados ou substituídos. A lista de deprecados **não é congelada nesta skill** — muda com o design system. Se a fonte NuDS não estiver acessível, **peça para instalar/conectar o MCP** (link na seção "Fonte de verdade para NuDS v3"); se a pessoa seguir sem ele, informe que o flag de deprecados não pôde ser validado e siga avaliando o observável. Componentes deprecados detectados pesam em **Brand & Content Compliance** (e podem afetar **Navigation & Flow Logic** se o pattern estiver fora do padrão atual).

## Passo a passo

### 0. Version check (sempre primeiro)
Consulte o GitHub canônico (seção **Version check**) e atualize a skill local se o remoto estiver mais novo. Só depois avance.

### 1. Coletar os inputs disponíveis
Confirme o que o usuário tem: o fluxo (Figma, **vídeo/screen recording**, e/ou prints), JTBDs (para User Experience Impact) e métricas (para Business Impact). **No pitch inicial, diga explicitamente que com vídeo da jornada a apuração é ainda melhor.** Explique o que dá para rodar com o que há (ver "Os inputs do usuário"). Rode parcial se for o caso — Craft roda sozinho.

### 2. Ler o fluxo
- **Se veio vídeo:** extraia frames ao longo da timeline; leia loading, transitions, overlaps e o caminho real. Guarde o arquivo de mídia junto do HTML de output para embutir na coluna Evidence.
- **Se veio Figma:** use o Figma MCP para abrir cada frame. Extraia componentes e variantes NuDS V3, tokens, tipografia e espaçamento; liste os componentes detectados; flague deprecados (cruzando com NuDS vivo); cheque localização por geo. Use referência de motion/protótipo se houver.
- **Se vieram prints:** leia cada tela (imagens/PDF). Avalie pelo observável e sinalize as limitações de inspeção de componente/token. Selecione 1+ prints para a coluna Evidence.

Em todos os casos, entenda a jornada de ponta a ponta: entrada, passos, como volta/sai, estados de erro/vazio/loading, e como o fluxo entrega os JTBDs informados. Em multi-geo, repita a leitura por geo.

### 3. Pontuar o Pilar 1 — Craft (6 parâmetros, escala 1–5)
Para **cada** um dos 6 parâmetros (Navigation & Flow Logic, Performance & Resilience, Interaction/Motion & Feedback, Layout & Surface Craft, Brand & Content Compliance, Smart & Personal):
- Leia as 5 descrições de nível no **Anexo A** e escolha o nível cuja descrição melhor corresponde ao que você observa no fluxo.
- Atribua a **nota (1–5)** e escreva um **rationale curto** citando a evidência concreta na(s) tela(s) que justifica o nível.
- Para os parâmetros que dependem de NuDS v3, aplique a regra da seção "Fonte de verdade para NuDS v3".

**Craft score = média simples das 6 notas.**

### 4. Pontuar o Pilar 2 — User Experience Impact (3 parâmetros, escala 1–5)
Para **cada** um dos 3 parâmetros (JTBD Efficiency, Customer Clarity, Trust):
- Use os **JTBDs informados pelo usuário** como referência — especialmente em JTBD Efficiency, avalie se o JTBD principal (e os secundários) se completa com passos mínimos, baixa carga cognitiva e sem becos sem saída.
- Escolha o nível no **Anexo A**, atribua a **nota (1–5)** e escreva o **rationale** citando o JTBD e a evidência no fluxo.

**User Experience Impact score = média simples das 3 notas.**

### 5. Pontuar o Pilar 3 — Business Impact (escala 1/3/5, por métrica)
Para **cada** métrica informada, compare o **número reportado** com o **target** e o **stretch**:
- **1 – Target missed**: reported < target
- **3 – Meets target**: reported = target (na prática: reported ≥ target e < stretch — atingiu a meta mas não o stretch)
- **5 – Stretch**: reported ≥ stretch

Use exatamente os números que o usuário informou. **Não invente números, targets nem realizados** — se faltar algum, peça ou marque a métrica como não avaliada.

**Business Impact score = média simples das notas das métricas.** Esse score vira o **tamanho do ponto** no mapa.

### 6. Posicionar no mapa de quadrantes
Cruze **Craft (eixo X, Magic)** × **User Experience Impact (eixo Y)**, com **corte fixo em 3** nos dois eixos:

| Quadrante | Condição | Leitura |
|---|---|---|
| **Star** (↑Magic · ↑UX Impact) | Craft ≥ 3 **e** User Experience Impact ≥ 3 | Alto valor estratégico + alta qualidade de craft. Os fluxos ideais. |
| **Hidden Gem** (↓Magic · ↑UX Impact) | Craft < 3 **e** User Experience Impact ≥ 3 | Alto valor, craft baixo hoje. Fortes candidatos a melhoria/investimento. |
| **Table Stakes** (↑Magic · ↓UX Impact) | Craft ≥ 3 **e** User Experience Impact < 3 | Craft forte, valor relativo menor. Pedem manutenção, não grande investimento novo. |
| **Skip** (↓Magic · ↓UX Impact) | Craft < 3 **e** User Experience Impact < 3 | Baixo valor e baixo craft. Repensar, simplificar ou despriorizar. |

O **tamanho do ponto** reflete o Business Impact score. Com corte fixo em 3, a skill funciona para **um fluxo isolado**; quando houver vários fluxos, plote todos no mesmo mapa.

### 7. Sintetizar main issues (antes do HTML)
Antes de montar o dashboard, extraia **3–6 main issues** do assessment — problemas transversais do fluxo, **não** uma lista por pilar/parâmetro. Cada issue em uma linha acionável (o que está quebrado + por que importa). Priorize o que mais move Craft, User Experience Impact ou Business Impact. Esses issues alimentam a **folha-resumo** (ver Dashboard).

### 8. Gerar o dashboard HTML
Monte um dashboard HTML auto-contido (ver seção "Dashboard"). Salve em `outputs/` (ou caminho equivalente da sessão) e apresente ao usuário.
- **Idioma padrão: inglês (EN).** Toda a UI do dashboard (labels, issues, rationales, âncoras resumidas, captions) sai em EN, a menos que o usuário peça explicitamente PT (ou outro idioma).
- **Labels de pilar no dashboard:** use exatamente **Craft**, **User Experience Impact**, **Business Impact**. Nunca “Customer Value” nem “Business Metrics”.
- **Evidence no summary:** copie o vídeo (preferir `.mp4` para playback amplo; `.mov` como fallback) e/ou prints para a mesma pasta do HTML e embuta com paths relativos.
- **Rodada parcial:** mostre apenas os pilares avaliados e sinalize claramente os não avaliados (ex.: "User Experience Impact — not assessed: JTBDs not provided"). Se só Craft rodou, mostre o Craft score na folha-resumo; o mapa de quadrantes precisa de Craft **e** User Experience Impact, então só desenhe o mapa quando ambos existirem.
- **Multi-geo:** plote um ponto por geo no mesmo mapa e, na folha-resumo, uma **tabela comparativa só com scores por pilar** (Craft / User Experience Impact / Business Impact) entre BR/MX/CO — sem quebrar parâmetros nessa visão.

## Regras de pontuação (idênticas para qualquer time)

- **A rubrica do Anexo A é a régua.** Sempre escolha o nível cuja descrição corresponde ao observado; não pontue "por impressão" sem casar com o texto do nível.
- **Média simples** em todos os agregados (dentro de cada pilar e por métrica). Nunca aplique pesos, a menos que o usuário peça explicitamente.
- **Corte dos quadrantes é fixo em 3** nos dois eixos (≥3 = alto ↑; <3 = baixo ↓).
- **Craft e User Experience Impact são eixos separados** — nunca colapse os três pilares numa nota única. O output preserva Craft, User Experience Impact e Business Impact como três dimensões.
- **Protagonismo da média do pilar.** Na comunicação e no dashboard, a **média do pilar** é o número principal. Quebras por parâmetro/métrica existem para auditoria e aprofundamento — não para a leitura de stakeholders. Ao comparar fluxos ou o mesmo fluxo entre países, compare **sempre** as médias de pilar primeiro.
- **Business Impact usa só 1/3/5** (não notas intermediárias), derivadas da comparação reported × target × stretch.
- **Rationale obrigatório por parâmetro** — é o que torna o assessment auditável. Cada nota vem com a evidência que a sustenta. Rationale detalhado fica na camada de detalhe, não na folha-resumo.
- **Nunca invente dados.** JTBDs, métricas, targets e realizados vêm do usuário. Regras de NuDS v3 vêm da fonte viva (zeroheight/Glean). Se algo faltar, peça ou sinalize.
- **Números reais, sempre.** Ao reportar o Pilar 3, use exatamente os valores fornecidos; não arredonde nem estime metas.

## Dashboard (estrutura)

Dashboard HTML único, auto-contido, responsivo. **UI em inglês por padrão.** **Duas camadas de leitura** — a folha-resumo vem primeiro e deve bastar para senior stakeholders e comparativos multi-país; o detalhe por parâmetro fica abaixo (ou recolhido).

### Camada 1 — Folha-resumo (stakeholder / multi-geo)
Entrega valor rápido. Contém agregados, evidência e issues gerais:

1. **Header**: flow name, country/BU (if provided), assessment date, and the resulting **quadrant** badge.
2. **Pillar scores (lead)**: Craft (Magic), User Experience Impact, Business Impact — each with the **pillar average** in large type, scale, and one-line reading (do not list parameters here). In multi-geo, show a **comparative table of pillar averages × country** on this sheet.
3. **Summary row (padrão de layout)** — três colunas lado a lado:
   - **Evidence (esquerda):** vídeo do fluxo embutido (`<video controls>` com `.mp4` + fallback `.mov`) **ou**, se não houver vídeo, print(s) representativo(s) da jornada. Caption curta da sequência observada. Arquivos de mídia na mesma pasta do HTML (paths relativos).
   - **Main issues (centro):** lista curta (3–6) dos principais problemas do fluxo **no geral**, não agrupados por pilar. Linguagem acionável, pronta para apresentação (em EN).
   - **Quadrant map (direita):** scatter com eixo X = Craft (Magic), eixo Y = User Experience Impact, linhas de corte em 3, quadrantes rotulados (Star / Hidden Gem / Table Stakes / Skip), ponto dimensionado pelo Business Impact. Vários fluxos/geos = vários pontos no mesmo mapa.
4. Responsivo: em viewports estreitas, empilhar Evidence → Issues → Map.

### Camada 2 — Detalhe auditável (secundária)
Aprofundamento opcional; visualmente subordinada à folha-resumo (seção inferior, tipografia menor, ou `<details>` recolhido por padrão):

5. **Quebra por parâmetro dentro de cada pilar**: nota (1–5), rótulo do nível (Not Ready / Partially Ready / Baseline / Strong / Superb) e **rationale** (EN). Seções de detalhe: **Audit detail · Craft**, **Audit detail · User Experience Impact**, **Audit detail · Business Impact** (nunca “Business Metrics”). Pilar 3: métrica, target, stretch, reported e nota 1/3/5.
6. **Âncora da rubrica**: ao lado de cada nota, a descrição do nível do Anexo A usada como âncora (pode permanecer no inglês da rubrica oficial).

**Hierarquia visual obrigatória:** médias de pilar ≫ (evidence + issues + map) ≫ quebra por parâmetro. Nunca inverta — a primeira tela/viewport da folha-resumo não deve competir com tabelas de parâmetros.

Siga o design system visual do Nubank quando possível (cores, tipografia). Consulte a skill `frontend-design` para padrões de UI de alta qualidade. Cores dos níveis, para consistência com os prints da rubrica: 1 = vermelho, 2 = laranja/âmbar, 3 = amarelo, 4 = verde-médio, 5 = verde-escuro; roxo (#820AD1) como cor de marca.

---

# Anexo A — Rubrica-âncora (fonte de verdade)

As descrições abaixo são transcrições literais da rubrica oficial ("Parameters Score"). Use o texto do nível para ancorar cada nota. Não parafraseie ao decidir; compare o observado com estas descrições.

## Pilar 1 — Craft (escala 1–5)

Níveis: **1 – Not Ready · 2 – Partially Ready · 3 – Baseline · 4 – Strong · 5 – Superb**

### Navigation & Flow Logic
*Avalia se o fluxo de navegação é intuitivo e eficiente — a sequência de telas, a lógica de transição e o caminho estrutural garantem que o usuário avance nas tarefas, se recupere de erros e saia de processos sem becos sem saída ou fricção desnecessária.*

- **1 – Not Ready:** The navigation pattern does not match a NuDS V3 type, or the flow mixes patterns across similar moments. The flow has no way to go back or exit. The back or close button leads to the wrong screen. One user intent triggers stacked or redirect screens. The step order does not match how a customer thinks about the task. The flow takes more steps than the outcome needs. A step is a dead end, with no clear way forward. Navigation labels don't name the destination ("Continue," "OK" where the action is specific).
- **2 – Partially Ready:** Most screens use a NuDS V3 pattern, but a few default to the wrong type or mix patterns for similar moments. The user can usually find a way back or out, but on at least one screen it takes an extra tap, a workaround, or isn't obvious. Back or close occasionally lands on the wrong screen. The step order mostly matches how a customer thinks about the task, but the flow carries a few avoidable steps or an awkward detour. No screen is a full dead end, but at least one offers no obvious next action without backtracking. Some navigation labels name the destination; others default to generic terms like "Continue" or "OK."
- **3 – Baseline:** Each screen uses the correct NuDS V3 pattern. Back and close lead to the right place, but earlier context, such as scroll position or previously entered information, may not carry over. The user can back out of or exit the flow at each step. The flow follows a logical order and reaches the outcome, though it may take one or two extra steps, or hit one awkward stop. Labels state the main action. The user can follow, but a step or two relies on inference. Progress in longer flows isn't always made explicit.
- **4 – Strong:** Nearly every screen uses the correct NuDS V3 pattern, chosen with intent; only an edge case or two falls back to a workaround. The user almost always knows how to go back or exit, and back or close lead to the right place, though context such as scroll position may occasionally not carry over. The flow is close to the shortest path, with at most one step that could be trimmed. There are no dead ends, though one path forward may require a beat of extra thought. Most labels name their destination or outcome; progress in longer flows is legible most of the time.
- **5 – Superb:** Every screen uses the correct NuDS V3 pattern, chosen on purpose. The user always knows how to go back or exit, and each button leads to the right place. Moving between steps keeps context; nothing resets without reason. The flow is the shortest path to the outcome. Every path forward, including cancel, back, and error, leads somewhere clear. There are no dead ends. Every label names its destination or outcome. In multi-step flows, progress is legible. Reading alone guides the shortest path.

### Performance & Resilience
*Avalia a resiliência operacional e a fluidez — velocidade de carregamento, estabilidade visual e robustez sob estresse. Garante que a experiência seja rápida, previsível e funcional, com tratamento gracioso de erros, proteção de ações de alto risco e integridade de estado durante interrupções.*

- **1 – Not Ready:** The page shows more than one loading indicator. Skeletons do not match the final layout, so content jumps when it loads. Frames freeze or stutter. Edge cases and error states are missing. Leaving and returning to the app resets the flow. The errors only say something failed, without naming what happened or offering a next step. Empty/no-data states have no guiding copy. Risky or irreversible actions have no confirmation. Copy assumes a single data shape: it truncates or overflows with a long name/value.
- **2 – Partially Ready:** The page mostly shows a single loading indicator, but a secondary one appears on part of the screen. Skeletons resemble the final layout only loosely, so some content still shifts once it loads, and an occasional frame stutters on a slow connection. A few edge cases, such as long text, no data, or permission denied, have a defined state, but poor connectivity and most error states are still undefined. Leaving to another app and returning sometimes lands the user back on the right step, but progress and entered data are lost more often than not. Errors state that something went wrong but rarely say what happened or what to do next; risky actions sometimes lack confirmation; copy occasionally truncates or overflows with a long name.
- **3 – Baseline:** The page shows one main loading indicator. Shimmer appears only on data that is still loading and is dynamic. Fixed content appears instantly. Skeletons roughly match the final layout, but some adjustments might still occur. Core error states are designed for the main flow, but some edge cases, such as long text, no data, permissions, or poor connectivity, are still undefined. Returning from another app usually lands back on the right step, but entered data or scroll position may be lost. Errors in the main flow explain and suggest an action, but edge cases (long text, no data, permissions, poor connectivity) still use generic messages. Common data-variation cases are handled (basic plural, expected truncation), but extreme, negative, or zero values still produce odd copy.
- **4 – Strong:** The page shows one main loading indicator, and shimmer appears only on data still loading. Skeletons closely match the final layout, so content rarely shifts once it appears; frames stay stable even on a slow connection. Edge cases and error states are defined for the main flow and most secondary ones, though a rare case, such as an extreme connectivity drop, remains untested. Leaving to another app and returning restores the right screen and most entered data, with only an occasional loss of scroll position. Most errors name what happened and suggest a next step; risky or irreversible actions ask for confirmation; copy holds up across common data variations, with only rare edge values producing awkward phrasing.
- **5 – Superb:** The layout and copy load and stay stable; only data still in transit shows shimmer. Dynamic data that rarely changes is pre-fetched, so it loads instantly after the first time. There is no layout shift and no frozen frame, even on a slow connection. Leaving and returning to the app always restores the exact screen, context and data. Every error and edge state names what happened and gives the next step in clear language. Risky or irreversible actions ask for confirmation. Sensitive data is masked. Copy stays correct across every expected data variation: plural/singular, zero, negative, long name, empty list — variable agreement resolved, nothing truncates unintentionally.

### Interaction, Motion & Feedback
*Avalia a eficácia do modelo de interação — alinhamento à tarefa, intuitividade do input e a responsividade de motion e feedback. Garante que o comportamento do sistema pareça natural e proposital, com animações, cues hápticos e sons calibrados às ações do usuário.*

- **1 – Not Ready:** The interaction approach does not fit the task, or people struggle to use it correctly. Motion is missing, decorative, or does not match its purpose. Motion is added with no reason. Feedback copy missing or off-tone: lightness in a serious moment, or coldness where acknowledgment was due. States with no text confirming what happened.
- **2 – Partially Ready:** The interaction approach mostly fits the task, but some people need a second attempt or explanation to use it correctly. A few transitions are defined, but others are missing, feel decorative, or don't match the moment they're meant to support. Some state changes show feedback, but others leave the user unsure whether the action registered. Tone is inconsistent: a light touch appears in a serious moment, or an important action passes without acknowledgment.
- **3 – Baseline:** The interaction approach fits the task, and most people can use it without confusion. Core transitions and micro-interactions are defined and consistent. Animation curves match NuDS tokens. State feedback exists and confirms the action. Tone usually matches the moment, but restraint isn't consistent.
- **4 – Strong:** The interaction approach fits the task well, and almost everyone can use it correctly on the first try. Nearly every transition and micro-interaction is defined, purposeful, and matches NuDS motion tokens; an occasional flourish lacks a clear reason. State feedback confirms most actions clearly. Tone matches the gravity of the moment in almost every case, with restraint holding up outside of a rare exception.
- **5 – Superb:** The interaction approach is the best fit for the task, and people use it correctly without extra effort. Every transition has a purpose: it guides attention, confirms an action, or marks a real milestone. Every feedback confirms what changed. Tone always matches the gravity of the moment: it celebrates a real milestone, stays sober for what's serious or irreversible. No manufactured pressure.

### Layout & Surface Craft
*Mede a clareza visual e a intencionalidade dos layouts — hierarquia visual, focal points, espaçamento, ritmo, consistência, tipografia e redução de ruído. Garante que cada tela mantenha um foco narrativo claro, onde cada elemento cumpre um propósito distinto.*

- **1 – Not Ready:** The screen looks noisy or unbalanced. The hierarchy is unclear. Several elements compete for attention. The same kind of element uses different components on the same screen, such as two different button styles for the same kind of action. The screen uses more typography styles than it needs, or uses different styles for the same kind of text. Copy repeats what the visual already conveys. Text runs longer than needed and competes for attention. No reading hierarchy: title, support, and action carry the same weight. In confirmation and status screens — the ones a customer opens only to check where something stands — copy is wordy or clever where the user only wants to read a fact at a glance.
- **2 – Partially Ready:** The hierarchy is legible in parts, but a few screens still have more than one element competing for attention. Most instances of the same kind of element share a component, but one or two exceptions remain, such as a second button style for the same action. Typography uses more styles than the screen needs, with a couple of interchangeable ones left over. Copy sometimes restates what's already visible, and confirmation or status screens carry a few more words than a quick scan needs.
- **3 – Baseline:** Typography styles are mostly consistent, though a few extra or mismatched styles remain. The hierarchy is mostly clear. Pockets of redundancy or longer-than-needed copy remain. Confirmation and status copy is mostly lean, but some items carry more words than a quick scan needs.
- **4 – Strong:** The hierarchy is clear on nearly every screen, with one focal point per moment; a rare screen still has a secondary element pulling attention. The same kind of element consistently uses the same component. Typography is close to the minimum needed, with at most one style that could be consolidated. Spacing is mostly refined, and copy is lean; confirmation and status screens read at a glance, aside from an occasional line that could be tightened.
- **5 – Superb:** The hierarchy is clear at a glance. One thing leads at each moment, action is unambiguous. The same kind of element uses the same component throughout the screen. The screen uses the fewest typography styles needed, and the same style is always used for the same function. Spacing is refined. Nothing appears without a reason, every word has a function.

### Brand & Content Compliance
*Avalia a aderência do fluxo aos padrões de design e marca — uso de componentes e tokens, consistência com o design system, Magic App guidelines e estratégia visual/de conteúdo. Garante uma experiência coesa e alinhada à documentação e identidade de marca da Nu.*

- **1 – Not Ready:** The design ignores or heavily changes NuDS v3 components with no documented reason, or does not follow Magic App guidelines where they apply. Copy breaks content guidelines: terminology off the canonical set, prohibited terms (e.g. sensory verbs), inconsistency across locales. The same concept changes name across the flow (one term on one screen, another on the next). Interactive elements have no accessibility label, or one that doesn't describe the action; copy depends on color or position ("tap the green button"); informative imagery has no alt text. Imagery is unlicensed, off-brand, or generic stock. Promotional content ignores brand or marketing rules.
- **2 – Partially Ready:** Most components come from NuDS v3, but a few are modified or replaced without a documented reason, and Magic App guidelines are followed inconsistently where they apply. Some terminology sits outside the canonical set, and at least one concept changes name partway through the flow. A few interactive elements carry accessibility labels, but several are missing or don't describe the action, and some copy still leans on color or position ("tap the green button"). Imagery is mostly on-brand, though a piece or two is generic stock or its licensing hasn't been confirmed.
- **3 – Baseline:** Most components, tokens, and patterns come from NuDS v3, and follow Magic App guidelines where they apply. Any custom solution is documented. Copy follows content guidelines. Canonical terminology mostly correct, with occasional slips or inconsistencies across locales. Main elements have accessibility labels and text doesn't rely on color alone, though generic labels or an unconsidered screen-reader reading order remain. Imagery is on-brand, though not always the ideal asset.
- **4 – Strong:** Nearly all components, tokens, and patterns come from NuDS v3 and follow Magic App guidelines; any exception is documented. Canonical terminology is correct in almost every instance, with at most an isolated slip in one locale, and each concept keeps a single name across nearly the whole journey. Most interactive elements have accessibility labels that describe the action, and reading order is sensible, though a secondary element or two still uses a generic label. Imagery is on-brand and licensed, even if not always the strongest available asset.
- **5 – Superb:** The flow combines NuDS v3 components and Magic App guidelines instead of inventing new pieces. Copy, imagery, and promotional content follow content, brand, and marketing guidelines. Canonical terminology is correct and consistent across all locales, and each concept uses a single term from the start of the journey to the end. Every interactive element has an accessibility label that describes the action; copy works without relying on color, position, or a single sense; informative imagery has a text alternative; reading order makes sense for a screen reader. All imagery is officially licensed.

### Smart & Personal
*Mede a personalização e inteligência do app — como ele usa insights do cliente (pré-preencher dados, oferecer recomendações relevantes, adaptar conteúdo ao histórico e surface de ações lógicas) para criar uma experiência proativa, adaptativa e individual.*

- **1 – Not Ready:** The experience is the same for every user, regardless of history or context. The app asks for information it already has. There is no suggested next step. Personalization, where it exists, isn't expressed in language: generic recommendation, no copy that recognizes context.
- **2 – Partially Ready:** The experience is largely the same for every user, though one or two fields pre-fill from information already on file. The app still asks for some data it already has elsewhere. There's no suggested next step after a task finishes, and where a recommendation does appear, it reads as generic rather than aware of the user's context.
- **3 – Baseline:** Some personalization exists, such as pre-filling a known field or remembering a past choice. Recommendations or defaults exist but are not proactively surfaced.
- **4 – Strong:** Personalization shows up in most of the relevant moments: known fields pre-fill, past choices are remembered, and at least one recommendation is proactively surfaced rather than waiting to be found. A next step is suggested after most tasks finish, though not universally. Where customization fits, the user can shape some of the experience, even if the option isn't yet complete.
- **5 – Superb:** The app recognizes what the user knows and needs, pre-fills and recommends based on context, and proactively suggests a next step. Where it fits, the user can customize their own experience.

## Pilar 2 — User Experience Impact (escala 1–5)

Níveis: **1 – Not Ready · 2 – Partially Ready · 3 – Baseline · 4 – Strong · 5 – Superb**
Este pilar usa os **JTBDs informados pelo usuário** como referência.

### JTBD Efficiency
*Quão simples é completar o JTBD principal e os secundários? O cliente consegue completá-lo com passos mínimos, baixa carga cognitiva e sem becos sem saída?*

- **1 – Not Ready:** The primary JTBD cannot be completed end-to-end or face several frictions to do it so.
- **2 – Partially Ready:** The primary JTBD is technically completable. There are redundant steps or unnecessary decisions, making the task less efficient.
- **3 – Baseline:** The primary JTBD is completable in a minimal sequence. Regulatory/technical complexity is somehow perceived. The flow doesn't ask for information it already has and common shortcuts or defaults exist for repeat actions.
- **4 – Strong:** Additionally to the points covered by the Baseline, the regulatory/technical complexity is barely perceived and the flow provides features that goes beyond delight the JTBD completion by making the experience faster.
- **5 – Superb:** Additionally to the points covered by Strong, every step feels necessary and fluid. Complex jobs (multi-step, multi-account, multi-geo) are modular so the experience doesn't feel as burdensome.

### Customer Clarity
*O cliente sempre sabe onde está, o que aconteceu e o que fazer em seguida?*

- **1 – Not Ready:** The customer cannot tell the flow/product status or whether something worked. Low affordance; actions complete without feedback or with misleading feedback. No clear recovery path.
- **2 – Partially Ready:** Feedback exists for primary actions but arrives late, is generic, or disappears too quickly. Some states (loading, error, empty) are missing or described in technical language. Recovery paths exist but aren't obvious.
- **3 – Baseline:** Clear, timely feedback for all primary actions. States (loading, success, error, empty) are visible and in plain language. The customer always has an obvious next step. Errors explain what happened and how to fix it.
- **4 – Strong:** Additionally to Baseline, the feedback is calibrated — tone and weight match the importance of the action. The customer feels guided rather than just informed. Errors feel helpful, not alarming.
- **5 – Superb:** Additionally to Strong, the flow proactively prevents mistakes (smart defaults, clear warnings, confirmation on destructive actions). Feedback feels immediate and human — it acknowledges what the customer was trying to do, confirms success, and anticipates what they'll want to know next.

### Trust
*O fluxo parece seguro, honesto e vale a pena voltar a usar? Aumenta o relacionamento com o Nubank?*

- **1 – Not Ready:** The flow contains misleading, wrong, incomplete, or absent information about fees, yields, limits, or risks. The customer cannot verify what happened to their money. Security signals are absent or broken.
- **2 – Partially Ready:** Key financial information is present but buried, in jargon, or disclosed too late (e.g. fee shown only at confirmation). Trust signals exist but feel generic or templated.
- **3 – Baseline:** All fees, yields, limits, and financial impacts are disclosed upfront, in plain language, before the customer commits. Security signals are clear and consistent.
- **4 – Strong:** Additionally to Baseline, the flow actively builds confidence and when automation options are present, they are clear and customer can easily revoke the control. Disclosures feel like helpful information, not legal standard. The customer feels the product is working in their interest.
- **5 – Superb:** Additionally to Strong, the flow makes the customer feel genuinely secure and informed at every step by proposing the better path to complete the same JTBD or the next best action.

## Pilar 3 — Business Impact (escala 1 / 3 / 5)

Parâmetro: **Métricas sob a categoria "Demand"** (não-exaustivas, adaptadas ao conjunto de métricas de cada time — ex.: % activation, # active users, Conversion (eligible/active), MAU/MEAU, Recurrent buyers/Engagement, Market share, PV/AUC/AUM, IFP/NNM). Definidas segundo as guidelines do time. Pergunta central: *o fluxo está impactando positivamente as métricas de negócio? Está alinhado aos objetivos das squads/BU?*

Para cada métrica, compare o número reportado com o target definido:

- **1 – Target missed:** The business metric set for this flow was not reached (the reported number < set target).
- **3 – Meets target:** The business metric set for this flow was reached (the reported number = set target).
- **5 – Stretch:** The business metric set for this flow was surpassed, reaching the stretch (the reported number > set target and = stretch target).

## Anexo B — Como ler os scores e o mapa

Para Craft e User Experience Impact, avalia-se cada fluxo com uma nota por critério e chega-se a uma média (Craft = média dos 6 parâmetros; User Experience Impact = média dos 3). Cruzando os dois scores, posiciona-se o fluxo num chart:

- **Eixo horizontal: Craft** (Magic)
- **Eixo vertical: User Experience Impact**
- **Business Impact: refletido no tamanho do ponto**

Quadrantes (corte em 3 nos dois eixos):

- **01 · Star (↑Magic · ↑UX Impact):** Experiences with high strategic value and high craft quality. These are the ideal flows: important to the business and to users, while also delivering a polished, coherent, and refined experience.
- **02 · Hidden Gem (↓Magic · ↑UX Impact):** Experiences with high value but low craft quality today. These flows matter strategically or are heavily used, but the experience is still underperforming — making them strong candidates for improvement and investment.
- **03 · Table Stakes (↑Magic · ↓UX Impact):** Experiences with strong craft quality but lower relative value on the map. They are well executed, but less critical than other strategic flows, so they usually call for maintenance rather than major new investment.
- **04 · Skip (↓Magic · ↓UX Impact):** Experiences with low value and low craft quality. These typically do not justify significant incremental investment in their current form and may need to be rethought, simplified, or deprioritized.
