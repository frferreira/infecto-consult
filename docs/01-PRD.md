# 1. PRD — Product Requirements Document

**Produto:** Infecto Consult — apoio à decisão clínica em infectologia à beira do leito
**Versão:** 0.3 (rascunho para aprovação)
**Data:** 04/10/2026
**Status:** 🟡 Aguardando aprovação

---

## 1.1 Visão geral

O **Infecto Consult** é um aplicativo (SaaS por assinatura) que apoia a tomada de decisão de médicos plantonistas em pronto-socorro, UTI e hospitais. O médico informa a doença ou o cenário clínico (ex.: pneumonia, sepse, pielonefrite, meningite) e recebe um **protocolo prático**, com **algoritmo interativo** e **esquema terapêutico**, de forma rápida, na beira do leito.

Dois públicos usam o produto:
- **Médicos usuários (consulta):** pesquisam e percorrem protocolos, respondendo a perguntas simples até chegar à conduta.
- **Médicos contribuidores (autoria):** escrevem e mantêm os protocolos em um ambiente de escrita fácil, com histórico de versões e referências bibliográficas.

Os protocolos **não têm padrão fixo** de escrita, tamanho, sequência ou procedimentos. Alguns exigem perguntas ao médico consultante, outros são apenas descritivos. O modelo de conteúdo precisa ser flexível.

### Contexto atual (levantado em 04/10/2026)
| Item | Valor |
|---|---|
| Base de conteúdo inicial | Base no **Notion** com protocolos já escritos (link em `Entradas/Link.txt`). Será usada nos testes iniciais. |
| Base Notion — "Contrato editorial / Fila de publicação" (analisada em 04/10/2026 a partir da página exportada em HTML) | **17 páginas**: 6 Publicado, 2 Rascunho, 9 "Testando no PWA". Categorias: Síndrome clínica, Raciocínio clínico, Patógeno, Medicamento. Propriedades: Título, Status, Categoria, Publicar no site, Página premium, Nível de página, MiniApps usados, Abas adicionais, Ambiente (PS, Enfermaria, UTI, Ambulatório), Classe, Descrição curta, Fonte/URL da imagem, População (Adulto, Gestante, Imunossuprimido, PVHA, Idoso), Prioridade editorial, Próxima revisão, Sistema, Tags, Tipo de síndrome, URL PWA, Última atualização. |
| Protocolos em HTML (`Entradas/`) | 6 decisores autônomos (PAC, sepse, meningite, hepatite B, artrite séptica, pós-craniotomia): abas (Decisor, Líquor, Tratamento, Profilaxia…), fluxo de perguntas com botões, tabelas, alertas "regra crítica", rodapé de aviso. Servem de **modelo de conteúdo e de interação**. |
| Página de medicamento (Fluconazol) | Outro tipo de conteúdo: consulta rápida, prescrição rápida, ajuste renal, interações, monitorização, espectro, abas adicionais (Hemodiálise, Resistência, PK/PD, Gestante, Pediatria). |
| Versão anterior | PWA gerado pelo ChatGPT (`infecto-consult-pwa.vercel.app`). **Referência só de conteúdo**, não de interface (tem "cara de manual"). |
| Referências de UX | Instagram, Spotify, Strava: navegação já conhecida e rápida. |
| Planos | **1 plano** inicial: R$ 15,00/mês, teste de 5 dias; planos futuros (inclusive especiais para contribuidores). |
| Site atual | `infectoconsult.com.br`: "Conhecimento na prática"; módulos de exemplo (pneumonia, pielonefrite aguda, infecção por *C. difficile*); aviso de uso informativo; © Dr. Marcello Leal. |

> ⚠️ A base do Notion e o PWA anterior ainda **não foram analisados** (não há conector Notion nesta sessão). Volumes, campos e estrutura dos protocolos viram ponto em aberto (ver abaixo) e devem ser validados antes de fechar o modelo de dados.

## 1.2 Metas e objetivos
| # | Objetivo | Resultado esperado |
|---|---|---|
| O1 | Consulta rápida à beira do leito | Médico chega à conduta em poucos toques e segundos |
| O2 | Protocolos interativos | Algoritmos com perguntas de ida e volta, simples e por protocolo |
| O3 | Autoria facilitada | Médico contribuidor escreve protocolos sem apoio técnico |
| O4 | Confiabilidade clínica | Histórico de versões, alterações e referências em todo protocolo |
| O5 | Monetização SaaS | Login Microsoft/Google e assinatura por cartão de crédito |
| O6 | Base para evolução | Estrutura pronta para chat com IA e bot de WhatsApp |

**Fora do escopo (versão 1):** chat com IA/LLM; bot de WhatsApp; múltiplos planos; app nativo nas lojas; prontuário ou dados de pacientes.

## 1.3 Requisitos

### Requisitos funcionais

#### Acesso e conta
| ID | Requisito | Prioridade |
|---|---|---|
| RF-01 | Login com conta Google ou Microsoft (OAuth), sem senha própria | Must |
| RF-02 | Cadastro automático no primeiro login, com confirmação de dados (nome, CRM/UF, especialidade) | Must |
| RF-03 | Perfis: **Leitor**, **Contribuidor**, **Revisor** e **Admin** | Must |
| RF-04 | Assinatura do plano por cartão de crédito: **R$ 15,00/mês**, com **período de teste de 5 dias**; acesso à consulta condicionado a teste ou assinatura ativa | Must |
| RF-07 | Site `https://infectoconsult.com.br/` (landing page) que apresenta o produto, coleta cadastros/interessados e grava no banco de dados do app | Must |
| RF-08 | Validação do CRM do médico no cadastro (premissa: validação ativa; forma exata a definir) | Must |
| RF-05 | Gestão da assinatura (ver status, trocar cartão, cancelar) | Should |
| RF-06 | Planos futuros, inclusive plano especial para contribuidores | Could |

#### Consulta de protocolos
| ID | Requisito | Prioridade |
|---|---|---|
| RF-10 | Busca por doença, síndrome, sintoma, antimicrobiano ou palavra-chave, com tolerância a erros de digitação | Must |
| RF-11 | Catálogo navegável por categorias (ex.: respiratório, urinário, SNC, pele, abdominal) | Must |
| RF-12 | Execução do protocolo em formato de passos: perguntas simples, resposta por toque, conduta ao final | Must |
| RF-13 | Voltar a passo anterior e alterar uma resposta, recalculando a conduta | Must |
| RF-14 | Navegação livre entre as páginas/seções do protocolo (sem obrigar o fluxo guiado) | Must |
| RF-15 | Resumo da conduta com esquema terapêutico (fármaco, dose, via, duração, ajustes) | Must |
| RF-16 | Referências bibliográficas visíveis por protocolo e por trecho | Must |
| RF-17 | Favoritos e recentes | Should |
| RF-18 | Compartilhar/copiar a conduta (texto) | Could |
| RF-19 | Modo offline para protocolos favoritos (PWA) | Could |

#### Autoria de protocolos
| ID | Requisito | Prioridade |
|---|---|---|
| RF-20 | Editor de blocos de fácil escrita (título, texto, lista, tabela, alerta, imagem) | Must |
| RF-21 | Blocos interativos: **pergunta** (única/múltipla escolha, sim/não, numérica), **condição** (se-então) e **conduta** (esquema terapêutico) | Must |
| RF-22 | Estrutura livre: sem padrão obrigatório de seções ou sequência; protocolos simples (só texto) e complexos (algoritmo). O conteúdo é organizado em **abas** definidas pelo autor (ex.: Decisor, Líquor, Tratamento, Profilaxia) | Must |
| RF-36 | **Tipos de página:** Síndrome clínica, Raciocínio clínico, Patógeno e Medicamento (este com modelo de consulta rápida: prescrição, ajuste renal, interações, monitorização) | Must |
| RF-37 | **Metadados clínicos** filtráveis: Ambiente (PS, Enfermaria, UTI, Ambulatório), População, Sistema, Classe, Tipo de síndrome, Tags, Prioridade editorial e **data da próxima revisão** (com alerta de vencimento) | Must |
| RF-38 | Flag "Publicar no site" e "Página premium" por protocolo (conteúdo público de vitrine no site × conteúdo restrito a assinantes) | Should |
| RF-23 | Histórico de versões com autor, data, resumo da alteração e comparação entre versões (diff) | Must |
| RF-24 | Cadastro de referências (artigo, diretriz, DOI/URL) vinculáveis ao protocolo ou a um trecho | Must |
| RF-25 | Fluxo de publicação: rascunho → revisão → publicado; só o publicado aparece para leitores | Must |
| RF-33 | **Revisão por 2º médico:** o autor (médico credenciado, especialista no assunto) envia o protocolo; **o sistema sugere/escolhe o revisor por competência** e o **Admin pode atribuir ou trocar**, definindo **prazo** (proposta: 7 dias, com lembrete e escalonamento ao Admin ao vencer); o revisor **recebe notificação** (e-mail, push do PWA) e, ao entrar no app, vê a **pendência de revisão**; pode aprovar (publica) ou devolver com comentários. Autor e revisor devem ser pessoas diferentes | Must |
| RF-34 | Cadastro de áreas de competência do médico (para direcionar revisões) | Must |
| RF-35 | Central de notificações no app (pendências de revisão, devolutivas, publicações) | Must |
| RF-26 | Pré-visualização do protocolo como o leitor verá | Should |
| RF-27 | Visualização gráfica do algoritmo (fluxograma) durante a edição | Should |
| RF-28 | Importação dos protocolos da base do Notion | Must |

#### Administração
| ID | Requisito | Prioridade |
|---|---|---|
| RF-30 | Gestão de usuários, perfis e assinaturas | Must |
| RF-31 | Painel com usos por protocolo, protocolos mais consultados e assinaturas | Should |
| RF-32 | Log de auditoria de alterações em protocolos | Must |

### Requisitos não funcionais
| ID | Requisito |
|---|---|
| RNF-01 | **Desempenho:** abrir um protocolo em até 2 s em 4G; resposta a cada passo em menos de 300 ms |
| RNF-02 | **Mobile-first:** uso com uma mão, alvos de toque grandes, funcional a partir de 360 px |
| RNF-03 | **Segurança:** TLS, OAuth, controle de acesso por perfil aplicado no backend, segredos fora do repositório |
| RNF-04 | **LGPD:** coleta mínima (dados do médico); **nenhum dado de paciente** é coletado ou armazenado; política de privacidade e consentimento |
| RNF-05 | **Pagamento:** dados de cartão nunca passam pelo servidor próprio (tokenização no gateway) |
| RNF-06 | **Disponibilidade:** meta de 99,5%; backup diário do MongoDB com teste de restauração |
| RNF-07 | **Acessibilidade:** contraste WCAG AA, fonte ajustável |
| RNF-08 | **Idioma e fuso:** PT-BR, America/Sao_Paulo |
| RNF-09 | **Responsabilidade clínica:** aviso de que o conteúdo apoia, e não substitui, o julgamento clínico; versão e data do protocolo sempre visíveis |
| RNF-10 | **Evolução:** conteúdo estruturado e indexável para uso futuro por IA (RAG) e WhatsApp |

## 1.4 Experiência do usuário

**Personas**
| Persona | Necessidades |
|---|---|
| Plantonista de PS/UTI | Resposta em segundos, uma mão, ambiente estressante, poucas perguntas |
| Infectologista contribuidor | Escrever protocolos com liberdade, versionar, citar referências |
| Revisor/coordenador clínico | Revisar, aprovar e publicar com rastreabilidade |
| Admin do produto | Gerir usuários, assinaturas e conteúdo |

**Princípios de experiência**
1. Menos toques até a conduta: a busca é a primeira coisa da tela inicial.
2. Padrões conhecidos (Instagram, Spotify, Strava): barra inferior, cards, busca, favoritos.
3. Perguntas de volta curtas, uma por tela, com respostas em botões grandes.
4. Sempre possível voltar, editar a resposta ou saltar para outra seção.
5. Conteúdo sempre com versão, data e referências à vista.

**Jornadas principais**
| Pergunta do usuário | Tela | Resposta |
|---|---|---|
| "Paciente com suspeita de pneumonia" | Busca → protocolo | Perguntas (CURB-65, comorbidades) → conduta |
| "Qual a dose de ceftriaxona na meningite?" | Busca → seção do protocolo | Esquema terapêutico |
| "Quero cadastrar um protocolo de pielonefrite" | Autoria → editor | Rascunho → revisão → publicado |
| "Quero assinar" | Planos → pagamento | Acesso liberado |

## 1.5 Métricas de sucesso
| Métrica | Meta (3 meses após o lançamento) |
|---|---|
| Tempo médio até a conduta | ≤ 60 s (a validar) |
| Protocolos publicados | ≥ nº migrado do Notion (a definir) |
| Assinantes pagantes | a definir com o negócio |
| Retenção mensal de assinantes | ≥ 80% (proposta) |
| Protocolos com referências | 100% |

## Decisões
| # | Tema | Decisão |
|---|---|---|
| D1 | Modo de conteúdo | Claude propõe, usuário valida |
| D2 | Plataforma | PWA responsivo (Next.js) |
| D3 | Hospedagem | Servidor próprio do cliente (não Vercel) |
| D4 | Banco de dados | MongoDB |
| D5 | Login | Google e Microsoft |
| D6 | Pagamento | Cartão de crédito, 1 plano inicial |
| D7 | Preço e teste | R$ 15,00/mês, teste de 5 dias (v0.2) |
| D8 | Revisão | Todo protocolo é revisado por um 2º médico competente no tema, com notificação e pendência no app (v0.2) |
| D9 | CRM | Premissa: validação ativa (v0.2) |
| D10 | Domínio | `infectoconsult.com.br`, também usado como site que coleta informações para o banco (v0.2) |
| D12 | Revisor | Sistema escolhe por competência; Admin pode atribuir; com prazo (v0.3) |
| D13 | Gateway | Recomendado Asaas (v0.3, aguardando confirmação) |
| D11 | Identidade | Logo fornecido (`docs/assets/`); cores derivadas do logo; temas claro e escuro (v0.2) |

## Pontos em aberto
1. ~~Estrutura do Notion~~ — analisada (ver contexto). Falta apenas acesso às 17 páginas completas para migrar o conteúdo; por ora temos 6 HTMLs e a página do Fluconazol. Exportação completa pode vir depois.
2. Gateway de pagamento: recomendação **Asaas** (custo/benefício, ver `06`/chat); confirmar taxas vigentes antes de contratar.
3. Dados do site: proposta de formulário com nome, e-mail, CRM/UF, especialidade e consentimento LGPD. Confirmar.
4. Como o CRM é validado na prática (consulta manual ao CFM/CRM pelo Admin, ou integração)?
5. Prazo padrão de revisão: 7 dias? Quem recebe o escalonamento?
10. O status "Testando no PWA" do Notion vira qual estado no app? (proposta: "Em teste", visível só para contribuidores/revisores)
6. Contribuidores ganham plano gratuito ou desconto na v1?
7. Disclaimer e termos de uso: há texto jurídico pronto? (o site já traz aviso "exclusivamente informativa e educacional")
8. Haverá modo offline na v1?
9. Direitos de autoria dos protocolos (o site cita Dr. Marcello Leal): como os autores são creditados no app?
