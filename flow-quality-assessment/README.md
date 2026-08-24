# flow-quality-assessment

Skill do Claude para rodar um **Quality Assessment de fluxos de produto do Nubank** em 3 pilares complementares e gerar um dashboard HTML auditável com o mapa de quadrantes (Star / Hidden Gem / Table Stakes / Skip).

## Os 3 pilares

| Pilar | Papel no mapa | Escala | Parâmetros |
|---|---|---|---|
| **Craft** | Eixo X → Magic | 1–5 | 6 (Navigation & Flow Logic, Performance & Resilience, Interaction/Motion & Feedback, Layout & Surface Craft, Brand & Content Compliance, Smart & Personal) |
| **User Experience Impact** | Eixo Y → Customer Value | 1–5 | 3 (JTBD Efficiency, Customer Clarity, Trust) |
| **Business Impact** | Tamanho do ponto | 1/3/5 | 1 por métrica informada |

Craft e Value cortam no **3** para posicionar o fluxo. Business Impact vira o tamanho do ponto. Agregação sempre por **média simples**.

## Inputs do usuário

A rubrica é fixa; o que varia por produto/time o usuário fornece no início. A skill roda **parcial** — não precisa dos três para começar:

| Pilar | Input | Roda sem? |
|---|---|---|
| Craft (Magic) | Só o fluxo | ✅ roda sozinho |
| User Experience Impact (Value) | Fluxo + **JTBDs** | precisa dos JTBDs |
| Business Impact (tamanho) | **Métricas** (nome + target + stretch + reported) | precisa das métricas |

**O fluxo entra de dois jeitos:**
- **Figma (preferido):** link(s) inspecionados via Figma MCP → detecta componentes NuDS V3, flaga deprecados, checa localização, lê tokens/tipografia reais.
- **Prints/telas:** imagens/PDF em uploads → avaliação pelo observável (detecção de componente/token limitada).

Suporta o **mesmo fluxo em múltiplos geos** (BR/MX/CO) para comparativo lado a lado.

## NuDS v3 como fonte viva

As regras do NuDS v3 **não estão congeladas na skill** (mudam com o tempo). A skill consulta o design system via conector na sessão (zeroheight/MCP ou Glean). Se indisponível (ex.: SSO), marca os parâmetros dependentes como "sujeito a validação contra NuDS v3".

## Como escalar para outro time

Nenhuma edição de arquivo é necessária para adotar. Cada time apenas fornece **seus próprios JTBDs e métricas** no início da conversa — a rubrica (Anexo A do `SKILL.md`) é a mesma para todos. Isso mantém os assessments comparáveis entre times.

## Estrutura

```
flow-quality-assessment/
├── SKILL.md            # instruções + rubrica-âncora completa (Anexo A) — fonte de verdade
├── README.md           # este arquivo
└── assets/
    └── rubric.json     # versão machine-readable da rubrica (labels, cores, quadrantes, regras)
```

## Origem da rubrica

Rubrica oficial "Craft / User Experience Impact / Business Impact — Parameters Score" (deck interno GBA, pág. 8–17). As descrições de nível no `SKILL.md` são transcrições literais dessa fonte.
