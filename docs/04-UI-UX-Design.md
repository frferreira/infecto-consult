# 4. UI/UX Design

**Produto:** Infecto Consult — apoio à decisão clínica em infectologia à beira do leito
**Versão:** 0.2 (rascunho para aprovação)
**Data:** 04/10/2026
**Status:** 🟡 Aguardando aprovação

---

## Direção visual
**Conceito:** "Clareza clínica com ritmo de app de consumo" — rápido como Instagram, limpo como Spotify, direto como Strava.
1. **Rapidez:** busca sempre à vista; toques grandes; uma decisão por tela.
2. **Confiança:** versão, data e referências visíveis; tom sóbrio.
3. **Conhecido:** padrões de navegação familiares, sem "cara de manual".

**Logo:** lupa metálica com vírus azul no centro e anel turquesa (arquivos em `docs/assets/`: `logo-original.png`, `logo-512.png`, `logo-192.png`). É um logo 3D com fundo branco: para o app, gerar versão com fundo transparente e um **ícone simplificado** (lupa + vírus, 2 cores) para barra superior, favicon e ícone do PWA. O site `infectoconsult.com.br` usa o tom clínico com a assinatura "Conhecimento na prática"; as cores exatas do site não estavam acessíveis no CSS, então os tokens abaixo derivam do logo (azul + turquesa) e **melhoram** o que o site tem: contraste AA, tema escuro e sistema de tokens.

## Paleta de cores
### Base (tokens) — derivada do logo
| Token | Claro | Escuro | Uso |
|---|---|---|---|
| `bg` | #F6F9FC | #0B1219 | Fundo |
| `surface` | #FFFFFF | #141E28 | Cards |
| `text` | #0C1B2A | #E6EEF5 | Texto |
| `text-muted` | #526577 | #9DB1C3 | Secundário |
| `primary` | #1B5FA6 | #5AA9F0 | Botões, links, ação principal (azul do vírus; AA ≥ 4.5 sobre `surface`) |
| `accent` | #1AA3A8 | #3CCFCF | Destaques, progresso, realces (turquesa do anel). **Só para elementos gráficos**: não usar como texto no claro (contraste baixo) |
| `accent-text` | #0E7C82 | #3CCFCF | Texto/ícone turquesa que precisa passar AA |
| `border` | #DCE4EC | #24323F | Divisores |

### Semânticas
| Tipo | Cor | Uso |
|---|---|---|
| Sucesso | #1B8A4B | Conduta confirmada |
| Alerta | #B26A00 | Atenção, ajuste de dose |
| Perigo | #C62828 | Contraindicação, alerta grave |
| Info | #1F5FBF | Nota, referência |

### Cores de domínio
Categorias de protocolo (respiratório, urinário, SNC, pele, abdominal, outros) com cor fixa por categoria, usada em chips e ícones; paleta categórica pensada para daltonismo, nunca como único sinal (sempre com ícone/texto).

## Tipografia
Inter (alternativa: system-ui). Títulos 24/20 semibold; corpo 16 regular; legendas 13. Números tabulares em doses e escores.

## Grade, espaçamento e componentes
Grade de 4 px; margem lateral 16 px; raios 12 px; alvo de toque ≥ 48 px.
Componentes: barra de busca, card de protocolo, chip de categoria, botão de resposta grande, barra de progresso, bloco de conduta (tabela fármaco/dose/via/duração), bloco de alerta, aba inferior, lista de referências, badge de versão, editor de blocos, cartão de plano.

## Modelos de telas
**Início (mobile)**
```
┌──────────────────────┐
│ Infecto Consult   👤 │
│ ┌──────────────────┐ │
│ │ 🔍 Buscar doença │ │
│ └──────────────────┘ │
│ Recentes             │
│ [Pneumonia] [Sepse]  │
│ Categorias           │
│ (Resp)(Urin)(SNC)... │
│ Em alta              │
│ ▸ Meningite  v3      │
├──────────────────────┤
│ Início Cat. ★  Perfil│
└──────────────────────┘
```
**Pergunta do protocolo**
```
┌──────────────────────┐
│ ← Pneumonia   ⋮ 2/6  │
│ ▓▓▓░░░               │
│ Paciente tem ≥ 65    │
│ anos?                │
│ ┌──────────────────┐ │
│ │       SIM        │ │
│ └──────────────────┘ │
│ ┌──────────────────┐ │
│ │       NÃO        │ │
│ └──────────────────┘ │
│ Seções ▾ Referências │
└──────────────────────┘
```
**Conduta**
```
┌──────────────────────┐
│ Conduta sugerida     │
│ ⚠ Internação         │
│ Ceftriaxona 1 g IV   │
│ 12/12h · 7 dias      │
│ Versão 3 · 02/10/26  │
│ 📚 Referências (3)   │
│ [Alterar respostas]  │
└──────────────────────┘
```
**Editor (desktop/tablet):** coluna esquerda com estrutura/seções; centro com blocos; direita com referências, versões e pré-visualização; botão Enviar para revisão.

## Acessibilidade
Contraste AA; informação nunca só por cor; navegação por teclado no editor; rótulos para leitores de tela; fonte ajustável; respeita "reduzir movimento".

## Microcopy
Termos clínicos curtos; texto de ajuda ⓘ em escores e siglas; disclaimer: "Apoio à decisão clínica. Não substitui o julgamento do médico."

## Decisões
| # | Tema | Decisão |
|---|---|---|
| U1 | Tema | Claro e escuro |
| U2 | Primária | Azul do logo (#1B5FA6), turquesa como acento (v0.2) |
| U3 | Tema | Claro e escuro, alternável e seguindo o sistema (v0.2) |
| U4 | Identidade | Logo fornecido; criar versão transparente e ícone simplificado (v0.2) |

## Pontos em aberto
1. Há versão do logo com fundo transparente/vetorial (SVG)? Se não, vetorizamos.
2. Existem cores oficiais do site (hex) a respeitar?
3. Tema padrão: seguir o sistema do aparelho (proposta)?
4. Protótipo no Figma v0.1 criado: ver `Link do Figma.md` (10 quadros: 8 mobile, 1 editor desktop e tokens). Falta validar com os médicos.
