# Plano de Desenvolvimento: Protótipo Visual Mobile-First (Sistema de Reservas)

## 🎯 Objetivos
Criar uma proposta sólida de protótipo visual interativo em HTML/CSS/JS para simular um aplicativo mobile-first voltado para descoberta de eventos, consulta de promoções e reservas de casas noturnas em Goiânia. O protótipo será ideal para demonstração em conversas iniciais com parceiros e clientes (como o Luan e donos de casas).

## 📋 Lista de Tarefas (Todos)

- [x] **Fase de Planejamento e Design**: Criar proposta estruturada para apresentação e alinhar os pilares do app.
- [x] **Estrutura Base do App**: Criar `index.html` com layout mobile-first premium, simulação de frame de celular para desktop, e design responsivo.
- [x] **Listagem de Casas**: Implementar aba de descoberta de casas (Môi, Cajuína, Mosaic, etc.) com busca e filtros por Setor/Gênero.
- [x] **Programação & Promoções**: Exibir detalhes reais das casas e eventos conforme mapeado em `01-base-informacional.md` (Girls&Wine, DáoPlay, etc.).
- [x] **Fluxo de Reserva Interativo**: Permitir simulação completa de reserva (nome, telefone, quantidade de pessoas) com feedback visual de sucesso.
- [x] **Área 'Minhas Reservas'**: Listagem das reservas realizadas com QR Code simulado e status de presença.
- [x] **Aba 'Vibes' (Feed de Vídeos Verticais)**: Criar o feed imersivo de vídeos verticais estilo TikTok/Reels com rolagem fluida (`snap-y`), autoplay com `IntersectionObserver` de alta performance, mutar/desmutar sincronizado, progress bar de reprodução e integração nativa com o modal de reserva.
- [x] **Polimento Visual & UX**: Efeitos de neon, transições suaves de abas, ícones elegantes (Lucide Icons) e visual premium em Dark Mode (perfeito para o nicho de baladas).
- [x] **Validação & Entrega**: Revisar todos os fluxos e documentar resultados em `tasks/todo.md`.

## 🏗️ Decisões de Design (UX/UI)
- **Visual Nightlife Premium**: Cores escuras dominantes (background quase preto, cinzas profundos) combinados com acentos neon vibrantes (roxo, rosa, ciano).
- **Abas Inferiores (Bottom Nav)**: Navegação típica de app mobile (Descobrir, Vibes, Benefícios, Listas).
- **Responsividade Dupla**: No desktop, exibe um frame simulando um iPhone moderno centralizado na tela. No celular, expande para ocupar 100% da tela como um Web App nativo.
- **Interatividade Real**: Sem backend, mas usa estado no JavaScript (e persistência local opcional via localStorage) para salvar reservas adicionadas.
- **Experiência Vibes Imersiva**: Oculta o cabeçalho padrão para imersão total de ponta a ponta na aba Vibes, deixando apenas a barra de navegação visível sob efeitos dinâmicos de desfoque.

## 📄 Revisão de Resultados
- **Aba Vibes**: Implementada e 100% otimizada para dispositivos móveis com controle inteligente de áudio e renderização suave. Os vídeos curtos representam fidedignamente o estilo visual e lineup das principais festas e bares de Goiânia (Subcult, Beat Proibido, Môi e Fluxo).
- **Consistência de Dados**: O botão "Garantir Lista" na aba Vibes invoca a função nativa `openReservationModal(eventId, houseId)` passando as chaves correspondentes. Isso possibilita que os usuários se registrem diretamente a partir do feed de vídeos curtos.
- **Portabilidade**: Desenvolvido integralmente em vanilla HTML/CSS/JS com dependências de CDN de carregamento ultra-rápido (Tailwind, Lucide).

*Última atualização: Julho de 2026.*

---

# Fase de Produto: das notas de reunião aos requisitos (ago/2026)

- [x] Mapear o material existente (`01`-`03`) e o protótipo `index.html`
- [x] **Processo notas → prazo**: `base/04-processo-notas-para-prazo.md` (5 etapas, 12 decisões bloqueantes, método de estimativa PERT)
- [x] **Escopo do MVP**: `base/05-escopo-mvp.md` (features com critério de aceite, fora-de-escopo explícito, estimativa e 3 faixas de prazo)
- [x] **Infra e custo para 7 casas**: `base/06-infra-e-custos.md` (modelo de carga, ~R$300/mês, alerta de custo de SMS e de vídeo)
- [ ] **Reunião de decisões (Etapa 1)** — fechar as 12 decisões com o Luan e os sócios
- [ ] **Proposta de UX/layout** — canvas com as telas do MVP, a ser feito depois que o escopo for aprovado
- [ ] **Apresentar faixa de prazo aos sócios** com data de recompromisso

*Atualizado: 19/08/2026.*

---

# UX: clareza sobre programação e promoções (ago/2026)

## 🎯 Objetivo
O cliente do bar precisa responder três perguntas em segundos: **o que rola hoje**,
**quanto custa entrar agora** e **qual promoção ainda está valendo**. Hoje o protótipo
não responde nenhuma das três sem dois toques, porque a informação de tempo é texto
solto (`dia: "SÁBADO / 27.SET"`, `descricao: "Válida até 23h59"`) — o app não consegue
calcular nada, então empurra a interpretação para o usuário.

## 🩺 Diagnóstico do protótipo atual
- **Descobrir**: o cartão da casa mostra gênero, setor e Instagram — nada sobre hoje.
- **Página da casa**: as noites da semana têm todas o mesmo peso; não existe "hoje".
- **Entrada** (`entradaFree`) é o dado nº 1 de decisão e está no menor texto do cartão.
- **Benefícios**: promoções de terça e de hoje são visualmente idênticas; sem horário.
- **Datas fixas** ("24.JUN") envelhecem e fazem a demo parecer desatualizada.

## 📋 Tarefas
- [x] **Modelo de dados temporal**: `diaSemana`, `inicio`, `fim`, faixas de `entrada[]`
      e janela (`inicio`/`fim`) por promoção, substituindo strings.
- [x] **Motor de tempo**: próxima ocorrência de cada noite (com virada de dia),
      status da noite (agora/hoje/futura), status da promoção (ativa/expirada/começa às),
      contagem regressiva e preço de entrada vigente.
- [x] **Relógio simulável**: `?dia=&hora=` e controle no modo Gerente, para a demo
      não depender do horário real da reunião.
- [x] **Descobrir**: linha de data no topo com casas abertas agora; cartão passa a
      responder "o que rola hoje / entrada / promo ativa"; ordenação por quem está
      aberto; casa fechada hoje entra apagada. Instagram sai do cartão (não decide nada).
- [x] **Página da casa**: agenda começa em hoje; noite atual expandida e demais noites
      em linhas compactas (acordeão); entrada promovida a linha de destaque;
      promoções com status e contagem regressiva; expiradas visíveis porém apagadas.
- [x] **Benefícios**: filtro primário por tempo (Agora / Hoje / Semana), ordenado por
      "acaba primeiro", com estado vazio que diz quando a próxima começa.
- [x] **Reserva**: modal mostra entrada vigente e o que ainda está valendo.
- [x] **Vibes**: rótulo do evento passa a usar a próxima ocorrência calculada.

## 🏗️ Princípios aplicados (less-is-more)
- **Justificação**: cada adição pagou com uma remoção (ícone de Instagram e de pino
  no cartão saíram para caber a linha de "hoje").
- **Dominância tipográfica**: status é peso e tamanho de texto, não caixa colorida.
- **Honestidade**: promoção expirada não some — aparece apagada, porque sumir gera
  a dúvida "será que eu perdi?".

## 📄 Revisão de Resultados

### O que mudou no modelo de dados
Cada noite deixou de guardar rótulos e passou a guardar tempo:

```js
{ id, diaSemana: 5, inicio: "19:00", fim: "03:00",   // fim <= início ⇒ vira o dia
  entrada: [ { ate: "20:00", valor: 0 }, { valor: 10 } ],
  promocoes: [ { nome, detalhe, inicio?, fim? } ] }  // sem fim ⇒ vale a noite toda
```

Tudo o que aparece na tela ("HOJE", "acaba em 20 min", "fecha às 3h", "SEXTA · 28.AGO")
é derivado disso. Nenhuma data é digitada à mão, então o protótipo não envelhece —
o problema de "QUARTA / 24.JUN" some por construção.

**Custo operacional:** a casa passa a informar dia da semana, hora de abertura/fechamento,
faixas de entrada e a validade de cada promoção. É mais campo do que hoje, e é
exatamente o que a `F2` do `05-escopo-mvp.md` já exigia no critério de aceite.

### O que o cliente ganha em cada tela
| Tela | Antes | Agora |
|---|---|---|
| Descobrir | gênero, setor, Instagram | dia e hora atuais, quantas casas abertas, e por casa: status, noite, entrada e promoção ativa |
| Página da casa | 3 cartões iguais, "Agenda da Semana" | começa em hoje, noite atual expandida, demais em linhas compactas; entrada em destaque; promoção com relógio |
| Benefícios | tudo junto, sem horário | filtro Agora/Hoje/Semana, ordenado por quem acaba primeiro, expiradas apagadas no fim |
| Reserva | regra fixa em texto | entrada vigente + o que ainda está valendo naquela noite |

### Decisões de UX que merecem discussão
- **Promoção expirada não some, fica apagada e riscada.** Sumir gera a dúvida
  "será que eu perdi alguma?". Aparecer apagada responde antes da pergunta.
- **Uma noite expandida por vez.** Sete cartões completos viram muro; o cliente
  decide sobre uma noite de cada vez.
- **Instagram saiu do cartão** e foi para a página da casa. Não decide para onde ir.
- **Entrada virou o dado mais visível da noite.** É o que faz sair de casa ou não.

### Extras para a demo
- **Relógio simulável:** modo Gerente → "Simular horário", ou `?dia=sex&hora=21:40`
  na URL. A reunião nunca é às 22h de sexta; sem isso o app abre vazio.
- **Link direto:** `?casa=moi` abre a casa, `?aba=promos` abre a aba. Serve para o
  "vem pro Môi hoje" colado no direct cair na tela certa.
- **Auto-atualização a cada minuto:** as contagens regressivas correm na frente do cliente.

### Verificação
- `node --check` no script principal.
- 9 cenários de tempo (sexta 19h30/21h30, sábado 22h20/23h30, domingo 2h da manhã,
  terça sem nada aberto, quarta antes de abrir, quinta ao meio-dia, sábado 22h30):
  todos passaram — incluindo virada de dia e noite que atravessa a madrugada.
- Smoke test de renderização: 8 casas × 5 horários × todas as telas
  (casa, modal, 3 filtros de promoção, Vibes, portaria), sem `undefined`/`NaN`.

*Atualizado: 25/08/2026.*

---

# UX: refatoração para experiência premium (set/2026) — APLICADA

## 🎯 Objetivo
Cada tela responde uma pergunta só, e o usuário sabe em 1 segundo qual é. Referência: Apple (títulos grandes, uma tipografia, cartões Wallet, materiais translúcidos) e Uber (uma pergunta no topo da home, botão de ação fixo no rodapé).

## 🩺 Diagnóstico (capturas em 393×852, sexta 22h30 simulada)
- **Nada é principal na home.** Saudação, CTA do Vibes, busca e 7 cartões têm o mesmo peso. Cada cartão tem borda de uma cor diferente, então a tela vira um arco-íris sem foco.
- **O topo gasta o espaço nobre com ferramentas de demo.** "Curadoria / LUAN", o seletor de vibe, o botão Cliente/Gerente e o selo "Horário simulado" não servem para quem vai sair hoje.
- **Tudo em caixa-alta de 9–11px.** Sem escala tipográfica não há hierarquia; tudo grita igual.
- **Nenhuma imagem.** Um app de noite sem foto nem vídeo nos cartões; o Vibes tem esse material e ele não aparece na descoberta.
- **Página da casa sem ação principal.** Não há botão "Entrar na lista" visível na primeira dobra. O "Voltar para casas" é um botão grande que ocupa o lugar do conteúdo.
- **O tema da casa troca a fonte inteira** (serifa na Cajuína). A identidade da casa vira quebra de consistência do app.
- **Nomes não batem:** a aba "Benefícios" abre "Promoções"; a aba "Listas" abre "Minhas Reservas".
- **Redundâncias:** Vibes aparece duas vezes na home (CTA e aba); "ENTRADA … Entrada R$15" repete o rótulo.
- **Visual quebrado:** na captura da casa aparece um brilho branco atrás da barra de abas (a confirmar no iPhone).
- **Listas vazia** é uma caixa tracejada sem nenhuma sugestão.

## 🧭 Proposta
1. **Navegação em 3 abas:** Hoje · Vibes · Ingressos. Promoção é atributo da noite, não destino: aparece na home e na casa. Gerente e seletor de vibe vão para o avatar/perfil (ou `?demo=1`).
2. **Home "Hoje":** título grande "Sexta, 18 set" que encolhe ao rolar, e embaixo "5 casas abertas agora". Depois vêm:
   - **Hero:** a noite mais relevante agora, com vídeo do Vibes em loop mudo.
   - **"Abertas agora":** carrossel de cartões com imagem.
   - **"Valendo agora":** promoções com contagem regressiva.
   - **"Mais tarde e amanhã".**
   - **Busca:** por puxar para baixo ou pelo ícone.
3. **Cartão da casa:** imagem em cima, nome, e uma linha "Pagodão do Caju · até 2h". O preço fica à direita e em destaque ("R$15" / "Free até 23h"). Gênero e setor vão para uma linha secundária discreta. Uma cor de acento para o app todo; a identidade da casa fica só no logo e na imagem.
4. **Página da casa:** vídeo/foto ocupando a largura toda, voltar como chevron sobre o material translúcido, título grande. O botão principal fica fixo no rodapé: "Entrar na lista · Free até 23h". As outras noites ficam numa lista compacta.
5. **Reserva:** painel de baixo com altura fixa e contador de pessoas. No sucesso, o ingresso "cai" na aba Ingressos com animação.
6. **Ingressos no estilo Apple Wallet:** um cartão por reserva com QR grande e a próxima no topo. O estado vazio sugere o que está rolando hoje.
7. **Sistema visual:**
   - **Tipografia:** uma família só (pilha `-apple-system`/Inter), escala 34/22/17/15/13, caixa-alta só em rótulos raros.
   - **Grade e alvos de toque:** grade de 8pt, raio de 20 nos cartões, alvos de 44pt.
   - **Movimento:** mola, com escala de 0,97 ao tocar.

## ✅ Decisões (17/09/2026)
- **Primeiro passo:** protótipo visual separado para aprovação, antes de mexer no `index.html`. Canvas: https://claude.ai/artifact/L3BMutCTR6vXJTDJ9PNEzZ
- **Cliente/Gerente e seletor de vibe:** vão para o menu do avatar, junto com o relógio simulado.
- **Imagens:** frames dos vídeos do Vibes. O vídeo do Fluxo tem texto sobreposto em quase todos os frames, então o Fluxo usa o logo, assim como as casas sem vídeo (Cajuína, Vernissage, Mosaic).

## 📋 Aplicação (17/09/2026)
- [x] Canvas aprovado
- [x] Sistema visual: tokens, tipografia do sistema, uma cor de destaque, materiais translúcidos
- [x] Home "Hoje": destaque, "Abertas agora", "Valendo agora", "Amanhã", "Nesta semana", busca
- [x] Página da casa: capa ocupando a largura toda, botão de ação fixo, tema da casa só no logo e na imagem
- [x] Reserva em painel inferior com contador de pessoas; Ingressos no estilo Wallet (QR, status, próximos e passados)
- [x] Menu do avatar: Modo gerente, identidade visual (troca só a cor de destaque) e relógio simulado
- [x] Freelas e painel do gerente no mesmo visual (lógica da outra sessão preservada)
- [x] Nova aba **Agenda**: todas as casas por dia (Hoje, Amanhã, Fim de semana, próximos dias) com horário, entrada e promoções
- [x] Links antigos (`?aba=discover|promos|reservas`) continuam funcionando; `?aba=agenda&agenda=fds` abre o fim de semana
- [x] Correção: `?dia=sab` era ignorado (comparava SAB com SÁB)
- [ ] Verificar no iPhone real (Safari): blur, áreas seguras, rolagem do Vibes
- [ ] Decidir se a Agenda vira a tela inicial (constante `ABA_INICIAL` no `index.html`)

## 📄 Revisão de Resultados
- **Teste de fluxo (Playwright, 390×844, sexta 22h30 simulada):** home → casa → entrar na lista → ingresso → menu → busca → Vibes → gerente → ingressos vazios → segunda à tarde → quinta 20h → Freelas → links antigos → desktop. Sem erros de JavaScript.
- **Regressão do Freelas (teste da outra sessão):** vaga → contrato → escala → turno na portaria → nota → fechamento 1/1. Passou.
- **Agenda:** madrugada de sábado mostra a noite de sexta como "Agora"; fim de semana calculado certo na quarta (sex–dom) e no domingo (só domingo); voltar da casa retorna para a Agenda.
- **Ruído conhecido:** o console mostra "arquivo não encontrado" para casas sem capa (`<id>-capa.jpg`); é o mecanismo de fallback para o logo.
- **Capas:** frames dos vídeos em `logo-casas/*-capa.jpg` (Beat Proibido, Môi, Point, Subcult). O vídeo do Fluxo tem texto de agenda por cima em quase todos os frames, então ficou sem capa.

---

# Módulo Freelas — "Trabalhe na noite" (set/2026, pós-MVP)

Ideia de um sócio: vaga → termos → contrato assinado → tributos, acoplando a estrutura contábil dele.

- [x] **Documento**: `base/07-modulo-freelas.md` (divisão app × contabilidade, modalidades MEI/RPA/intermitente, riscos, versão enxuta, estimativa por tarefa, perguntas em aberto)
- [x] **Protótipo**: tela `?aba=freelas` (entrada no fim da aba Casas, fora da barra inferior), modal termos → aprovação → contrato → assinado, "Minhas escalas" com etapas, e bloco "Equipe freela" na Portaria com entrada/saída do turno e fechamento para a contabilidade
- [ ] Descobrir qual sistema contábil o sócio usa (define o formato da exportação)
- [ ] Consultar advogado trabalhista sobre limite de turnos (risco de vínculo)

## Revisão
- Teste ponta a ponta no Chrome headless (390px): candidatura, assinatura, entrada/saída na portaria, envio de nota, contagem 1/1 no fechamento; sem erros de JS.
- Demo cobre só MEI; RPA e intermitente ficam para a fase 2, conforme o documento.

*Atualizado: 17/09/2026.*
