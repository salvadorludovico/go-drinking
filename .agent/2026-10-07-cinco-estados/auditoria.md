# Auditorias do protótipo (2026-10-07)

Três auditorias somente-leitura sobre `index.html` (5360 linhas, commit `d79f3cc`), feitas por subagents. Linhas citadas referem-se a esse commit.

## Auditoria A: superfícies interativas e seus estados

Legenda: ✅ existe · ❌ falta · n.a. não se aplica (dado síncrono/hardcoded, sem requisição possível) · "Mobile" avalia layout em largura de celular (`max-w-md` na linha 299, `pt-safe`/`pb-safe`, `env(safe-area-inset-*)`). Nenhuma chamada nativa a `alert()`/`confirm()`/`prompt()` foi encontrada.

### A) Tabela de superfícies

| Superfície | Linhas | Happy | Empty | Error | Loading | Mobile | Observação |
|---|---|---|---|---|---|---|---|
| Aba Hoje (cabeçalho, resumo, chips) | HTML 311–346; `renderHoje` 1754–1811; `atualizarCabecalhoHoje` 1725–1748 | ✅ | ✅ | n.a. | n.a. | ✅ | Resumo "Nenhuma casa aberta agora" (1737); chips escondidos sem casa aberta (1742). Porém se `noitesDaSemana` vier vazia, `html` fica `''` e `#hoje-conteudo` fica em branco (1777–1807): não há cópia de vazio para o corpo da aba. |
| Hoje: busca | input 322; `htmlBusca` 1953–1989 | ✅ | ✅ | n.a. | n.a. | ✅ | "Nada encontrado / Nenhuma casa ou festa com …" (1960–1964). |
| Hoje: "Valendo agora" | `htmlValendoAgora` 1904–1927 | ✅ | ✅ | n.a. | n.a. | ✅ | Cópia "Nenhuma promoção valendo neste momento." (1924), só quando há encerradas mas nenhuma ativa; sem promoções a seção some (1911). |
| Hoje: Hero / rail / listas de noites | `heroHtml` 1817–1855; `cartaoRailHtml` 1857–1871; `listaNoitesHtml` 1873–1888 | ✅ | n.a. | n.a. | n.a. | ✅ | Botão de garantia no hero (1850) só abre o painel. |
| Aba Agenda (lista) | HTML 348–373; `renderAgenda` 2188–2229; `blocoDiaHtml` 2164–2186 | ✅ | ✅ | n.a. | n.a. | ✅ | "Nada programado / Nenhuma casa publicou programação para este dia." (2177–2180); chips de dia mostram "nada" (2206); rodapé com casas fechadas (2182–2183). |
| Agenda: modo Mapa | HTML 362–372; `atualizarMapaAgenda` 2546–2578; `criarMapaBase` 2496–2523 | ✅ | ✅ | ✅ | ❌ | ✅ | Erro sem Leaflet: cópia na 2547–2550. Falha no estilo vetorial cai silenciosamente para tiles Esri (2517, 2498–2506). Sem spinner/esqueleto enquanto estilo e tiles carregam: caixa `bg-[#1c1c1e]` vazia (363). Itinerantes sem geo explicados no rodapé (2900–2901). |
| Mapa: localização do cliente | `pedirLocalizacao` 2368–2382; `textoOrigem` 2384–2392; `desenharRodapeMapa` 2891–2902 | ✅ | n.a. | ✅ | ✅ | ✅ | Loading só textual: "Buscando sua localização…" (2386). Permissão negada/fora da cidade/sem suporte cai para origem demo com cópia e botão "Usar a minha" (2387–2390, 2895–2897). Guarda contra duplo pedido (2369). |
| Mapa: cartão do pino | `mostrarCartaoMapa` 2909–2952 | ✅ | ✅ | n.a. | ✅ | ✅ | "sem programação nestes dias" (2928); "Calculando distância…" (2944). |
| Mapa: rota real (OSRM, Open Source Routing Machine) | `buscarRotaReal` 2276–2302; `desenharRota` 2727–2749; `buscarTemposReais` 2304–2329 | ✅ | n.a. | ✅ | ❌ | ✅ | Falha/timeout de 6 s cai para arco ilustrativo (2746) e tabela de tempos volta à estimativa (2328), ambos silenciosos. Nenhum indicador enquanto a rota não chega. |
| Aba Vibes | HTML 407–412; `renderVibes` 5286–5356; `initVibesEngine` 4347–4445 | ✅ | ❌ | ❌ | ❌ | ✅ | Sem casa com `videoUrl`, o contêiner fica preto sem cópia (5295–5299). Nenhum `onerror` no `<video>`; `src` é sempre `logo-casas/<id>.mp4` (5311), independente de `videoUrl`: arquivo ausente = cartão preto com poster. Sem spinner de buffer; só barra de progresso (5349–5351). |
| Aba Ingressos | HTML 381–392; `updateReservasUI` 3636–3690; `ingressoHtml` 3567–3634 | ✅ | ✅ | n.a. | n.a. | ✅ | Três vazios com cópia: visitante (3650–3657, com CTA "Entrar com celular"), próximos vazio com sugestão da noite (3670–3686), passados vazio (3688). QR (Quick Response) cai para código escrito sem a lib (3547). |
| Tela Casa (detalhe) | HTML 394–397; `openHouseDetail` 3101–3267 | ✅ | ✅ | n.a. | n.a. | ✅ | "Sem programação publicada" (3127); CTA escondido sem noite (3263); "Onde é" para itinerante (2962–2970). |
| Casa: "Como chegar" / distância | `comoChegarHtml` 2962–2986; `distanciaCasaHtml` 2954–2960; `montarMapaCasa` 2988–2999 | ✅ | ✅ | ✅ | ✅ | ✅ | "Ver a distância daqui" (2960) → "Buscando sua localização…" (2959). Mini-mapa sem loading (mesma lacuna do mapa da Agenda). |
| Casa: CTA fixo no rodapé | HTML 426–435; 3240–3264 | ✅ | ✅ | n.a. | n.a. | ✅ | Um ou dois botões (lista/mesa), 3258–3259. |
| Casa: Compartilhar | 421; `compartilharCasa` 3275–3284 | ✅ | n.a. | ❌ | n.a. | ✅ | Sem `navigator.share` nem `clipboard`, o toque não faz nada e não avisa (3280–3283). |
| Aba Freelas (vagas) | HTML 375–378; `renderFreelas` 4914–4987 | ✅ | ✅ | n.a. | n.a. | ✅ | "Nenhuma vaga para essa função agora." (4959). "Minhas escalas" simplesmente não aparece sem escalas (4990). |
| Painel gerente: aba Painel | `htmlPainelGerente` 4550–4587 | ✅ | ❌ | n.a. | n.a. | ✅ | Sem noite em destaque o bloco é `''` (4558): números ficam em 0 sem cópia explicando. |
| Painel gerente: aba Lista | `htmlListaGerente` 4589–4624; `filtrarListaGerente` 4626–4631 | ✅ | ✅ | n.a. | n.a. | ✅ | Vazio: "Nenhum nome na lista de X ainda." (4591–4595). Busca sem resultado esconde todas as linhas e não diz nada (4628–4630). |
| Painel gerente: aba Ler QR | `htmlLeitorQr` 4655–4677; `iniciarCamera` 4684–4706; `processarLeitura` 4732–4786 | ✅ | ✅ | ✅ | ✅ | ✅ | Melhor superfície do app: "Abrindo a câmera…" (4670), "Câmera indisponível neste navegador." (4689), "Sem acesso à câmera. Libere a permissão ou simule abaixo." (4704), cartão ok/aviso/erro para QR inválido, outra casa, cancelada, já validada, noite acabada (4745–4769). Seção "Simule a leitura" some sem pendentes (4657), sem cópia. |
| Painel gerente: aba Equipe | `htmlEquipeFreela` 5204–5267 | ✅ | ✅ | n.a. | n.a. | ✅ | Vazio: "Nenhum freela escalado. N vagas publicadas." + link (5211–5219). |
| Painel de reserva (lista/mesa) | HTML 478–535; `openReservationModal` 3337–3409; `handleReservationSubmit` 3430–3489 | ✅ | ✅ | ❌ | ❌ | ✅ | "Noite ainda sem horário publicado." (3393). Validação é só `required` nativo (495, 499): balão do navegador, nada inline. Envio instantâneo: fecha e mostra toast (3484–3485), sem estado em voo. Stepper desabilita nos limites (3332–3333). |
| Painel de login (telefone → código → nome) | HTML 621–638; `renderLogin` 3885–3955; 3962–4031 | ✅ | n.a. | ❌ | ❌ | ✅ | Botões desabilitados até o dado ficar válido (3966–3967, 3944/3949), mas nenhuma mensagem inline. "Receber código" troca de tela na hora (3970–3976). Qualquer código passa (4005→4008–4015); classe `.otp-caixa.erro` (246) existe e nunca é aplicada. Reenvio com contagem desabilitada (3978–3990) é o único feedback temporal. |
| Modal da vaga (termos → aprovando → contrato → assinado) | HTML 537–549; `renderVagaModal` 5067–5162; 5164–5200 | ✅ | n.a. | n.a. | ✅/❌ | ✅ | Etapa "aprovando" tem spinner 1,5 s (5116–5123, 5164–5172): único estado em voo simulado do app. "Assinar contrato" (5141→5174) e "Enviar nota" (5013→5192) são instantâneos. Checkbox trava o botão (5140–5141). |
| Menu do avatar (conta + demonstração) | HTML 551–610; `renderMenu` 3768–3795 | ✅ | n.a. | n.a. | n.a. | ✅ | Identidade visual usa `escolher()` (3797–3803). |
| Painel confirmar/escolher | HTML 612–619; 3715–3752 | ✅ | n.a. | n.a. | n.a. | ✅ | Primitivo; ver seção D. |
| Onboarding | HTML 640–654; `abrirOnboarding` 4086–4171; 4240–4283 | ✅ | ✅ | n.a. | ❌ | ✅ | Ícones de fallback sem destaque/promo (4094, 4136, 4191). "Ativar localização" (4249) fecha o onboarding e pede a posição; o feedback só aparece se a pessoa abrir o mapa ou uma casa. |
| Toast | HTML 656–660; `showSuccessToast` 3491–3496 | ✅ | n.a. | ❌ | n.a. | ✅ | Só variante de sucesso: ícone `circle-check` verde fixo (658). "Áudio Mutado" (4344) e "Modo visitante" (4055) saem com o mesmo check. |
| Barra compacta / barras de abas | 301–305; 437–476; `mostrarView` 3017–3045 | ✅ | n.a. | n.a. | n.a. | ✅ | Navegação pura. |

### B) Botões de ação que mutam estado ou simulam requisição

| Botão (texto) | Markup | Handler | Loading? | Nota |
|---|---|---|---|---|
| Confirmar / Entrar na lista / Reservar mesa · N pessoas | 517 (`#res-submit`) | `handleReservationSubmit` 3430–3489 | ❌ | Fecha o painel e mostra toast na mesma chamada (3484–3485); depois `switchTab('ingressos')` em 350 ms (3489). Visitante é desviado para o login (3436–3444). |
| Retirar nome da lista / Cancelar reserva | 3627 | `cancelReserva` 3692–3703 | ❌ | Usa `confirmar()` com `perigo: true` (3694) ✅; mutação instantânea. |
| Receber código no WhatsApp / Prefiro receber por SMS | 3909, 3912 | `enviarCodigo` 3970–3976 | ❌ | Desabilitado até 11 dígitos (3966–3967). Troca de etapa sem "Enviando…". |
| Reenviar código | 3928 | `reenviarCodigo` 3992–3996 | parcial | Contagem regressiva com `disabled` (3984–3985) e toast; não há estado em voo no próprio reenvio. |
| (auto) código completo | input 3924 | `aoDigitarCodigo` 3998–4006 → `verificarCodigo` 4008–4015 | ❌ | 250 ms de atraso (4005) sem indicador; nenhum caminho de erro. |
| Continuar (nome) | 3949 | `concluirLogin` 4017–4031 | ❌ | Desabilitado até 2 caracteres (3944). |
| Sair | 3787 | `sairDaConta` 4033–4039 | ❌ | Sem `confirmar()`; instantâneo com toast. |
| Validar entrada (lista da portaria) | 4601 | `confirmPresence` 4642–4647 → `marcarPresenca` 4633–4640 | ❌ | Sem `confirmar()` e sem desfazer: toque errado é irreversível na demo. |
| Confirmar entrada (leitor QR) | 4772 | `confirmarLeitura` 4788–4802 | ❌ | Instantâneo; re-renderiza a aba QR e reabre a câmera (4801). |
| Quero essa vaga | 5110 | `candidatarVaga` 5164–5172 | ✅ | Spinner + "Candidatura enviada. Aguardando a aprovação…" por 1,5 s (5116–5123). |
| Assinar contrato | 5141 | `assinarContrato` 5174–5190 | ❌ | `disabled` até o aceite (5141); assinatura instantânea com toast. |
| Enviar nota | 5013 | `enviarNotaFiscal` 5192–5200 | ❌ | |
| Registrar entrada / Registrar saída (freela) | 5225, 5227 | `registrarTurno` 5269–5283 | ❌ | |
| Exportar para a contabilidade | 5252 | inline `showSuccessToast('Planilha enviada à contabilidade')` | ❌ | Só o toast; nenhuma mutação nem simulação. |
| Compartilhar | 421 | `compartilharCasa` 3275–3284 | n.a. | Sem feedback se share e clipboard não existirem. |
| Ativar localização / Usar a minha / Ver a distância daqui | 4249, 2897, 2960 | `pedirLocalizacao` 2368–2382 | ✅ (texto) | Guarda `origemTipo === 'pedindo'` (2369); feedback "Buscando sua localização…". O botão em si não é desabilitado. |
| Som do Vibes | 5320 | `toggleVibesAudio` 4317–4345 | n.a. | Toast com ícone de sucesso mesmo ao mutar. |

### C) Formulários e inputs: validação e exibição de erro

| Input | Linhas | Validação | Como o erro aparece |
|---|---|---|---|
| `#res-name` (Nome na lista / Em nome de) | 495; `prepararQuemVai` 3417–3428 | `required` nativo, ligado só quando logado (3420). Pré-preenchido com `sessao.nome` (3422). Sem `minlength`. | Balão nativo do navegador (`<form onsubmit>` em 491, sem `novalidate`). Nenhuma mensagem inline. |
| `#res-phone` (WhatsApp) | 499 | `required` nativo quando logado (3421); `type="tel"` sem `pattern`, sem máscara. | Balão nativo. Aceita qualquer texto. |
| Stepper de pessoas | 505–509; `alterarPessoas` 3328–3335 | Limita 1–10; botões `disabled` nos limites. | Não há erro possível. ✅ |
| `#login-tel` | 3903–3905; `aoDigitarTelefone` 3962–3968 | Máscara `(62) 99999-9999` (3850–3855); exige 11 dígitos para habilitar os botões; Enter com número incompleto retorna em silêncio (3971). | Só pelo `disabled` dos botões. Sem mensagem "número incompleto". |
| `#login-codigo` (OTP, one-time password) | 3922–3926; `aoDigitarCodigo` 3998–4006 | Só dígitos, `maxlength=4`; 4 dígitos disparam `verificarCodigo` (4005). Qualquer código é aceito (4008–4015). | Nenhum. `.otp-caixa.erro` (246) definida e nunca usada. |
| `#login-nome` | 3943–3946 | `disabled` em "Continuar" enquanto `< 2` caracteres; guarda silenciosa (4019). | Só pelo `disabled`. |
| `#search-input` (Hoje) | 322; `searchFilter` 1992–1994 | Nenhuma necessária. | Vazio "Nada encontrado" (1960–1964). ✅ |
| Busca da lista da portaria | 4610–4613; `filtrarListaGerente` 4626–4631 | Nenhuma. | Sem resultado: lista fica em branco, sem cópia. ❌ |
| Checkbox "Li o contrato" | 5140 | Trava `disabled` do botão (5141). | n.a. ✅ |

### D) Primitivos de feedback reutilizáveis

- **Toast**: `showSuccessToast(msg)` em 3491–3496. Markup `#toast-success` em 656–660 (`role="status"`, `aria-live="polite"`, classe `glass`, ícone fixo `circle-check` com `c-live`, texto em `#toast-message`). Some em 2 s. Não há variante de erro ou neutra.
- **`confirmar({ titulo, mensagem = '', acao = 'Confirmar', perigo = false })`** em 3733–3741: retorna `Promise<boolean>`. Monta no painel `#escolha-sheet` (612–619) via `abrirEscolha(html)` (3715–3721) e resolve por `fecharEscolha(valor)` (3723–3731). Botão "Cancelar" fixo no markup (618). Escape fecha (1506).
- **`escolher({ titulo, opcoes: [{ valor, rotulo }], atual })`** em 3743–3752: retorna `Promise<valor | null>`.
- **Spinner**: nenhum CSS reutilizável. Única ocorrência inline em 5120: `<div class="w-9 h-9 border-[3px] border-[#3a3a3c] border-t-white rounded-full animate-spin"></div>`. Atenção: `@media (prefers-reduced-motion: reduce)` em 250–252 zera todas as animações; loading precisa de texto junto.
- **Skeleton**: não existe.
- **Estados de botão no CSS**: `.btn-primary:disabled` em 128; `.stepper:disabled` em 154; `disabled:opacity-40` inline em 3912 e 3928.
- **Erro em campo**: `.otp-caixa.erro` em 246, nunca aplicada; `input:focus` força `border-color: var(--primary)` (263–266); não há classe de erro para `.row`/`.bare`.
- **Padrão de vazio já usado**: bloco centrado com círculo de 56 px + ícone Lucide + `t-headline` + `t-sub c-2` + CTA opcional, em 3651–3656 e 3671–3675; variante compacta `group-list px-4 py-6 text-center t-sub c-2` em 4592–4594, 4959 e 5213–5218; variante "Nada programado" em 2177–2180.
- **Cópia de loading textual existente**: "Buscando sua localização…" (2386, 2959), "Calculando distância…" (2944), "Abrindo a câmera…" (4670).

### E) Dez lacunas mais visíveis numa demonstração

1. **Confirmar reserva/lista sem estado em voo** (`handleReservationSubmit` 3430–3489; botão 517). O painel fecha e o toast aparece no mesmo tick.
2. **"Receber código no WhatsApp" troca de tela na hora** (`enviarCodigo` 3970–3976).
3. **Código de verificação sem erro e sem "Verificando…"** (4005, 4008–4015). Qualquer 4 dígitos passam; `.otp-caixa.erro` (246) já existe.
4. **Vibes sem vazio, sem erro e sem loading** (`renderVibes` 5286–5356). Sem `onerror` no `<video>` nem spinner de buffer.
5. **Portaria: "Validar entrada" e "Confirmar entrada" instantâneos e sem confirmação** (4601→4642–4647; 4772→4788–4802).
6. **Inconsistência no fluxo de freela**: "Quero essa vaga" tem spinner, mas "Assinar contrato", "Enviar nota" e "Registrar entrada/saída" são instantâneos.
7. **Validação nativa do navegador no painel de reserva** (`required` em 495 e 499, formulário 491 sem `novalidate`).
8. **Mapa sem loading** (2496–2523; 2546–2578; 2727–2749).
9. **Busca da lista da portaria sem resultado fica em branco** (4626–4631).
10. **Toast só tem variante de sucesso** (656–660, 3491–3496). Correlatos: "Exportar para a contabilidade" só toast (5252), `cancelReserva` sem voo (3692–3703), Compartilhar silencioso (3280–3283), Painel do gerente sem cópia quando não há próxima noite (4558).

Referências que já atendem ao padrão: aba Ler QR (4655–4809) e aba Ingressos (3636–3690).

## Auditoria B: breakpoints mobile e estilos nativos do navegador

### A) Estilos nativos do navegador que sobrevivem

| # | Onde (linhas) | O que o usuário vê | Correção recomendada |
|---|---|---|---|
| A1 | Checkbox nativo do contrato: `<input type="checkbox" ... class="w-5 h-5 shrink-0 accent-[#30d158]">` (5141) | Caixa de seleção do sistema, só tingida de verde. Único controle nativo visível; destoa do `.switch` desenhado (167–170). | Criar `.check` com `appearance:none` + `::after` (marca em SVG inline), 22–24px, nos tokens do `.switch`. |
| A2 | `input:focus { border-color: var(--primary) !important; outline: none !important }` (248–251). Inputs visíveis são `.bare` com `border: 0`, então o `border-color` não aparece; o `!important` vence o `:focus-visible` global (266–269). | Busca (324), nome/WhatsApp (505, 509), telefone (3903), nome no login (3943) e busca da portaria (4619) não mostram foco. | `.search-field:focus-within, .row:focus-within { box-shadow: inset 0 0 0 1.5px var(--primary) }` e remover o `outline:none !important`. |
| A3 | `:focus-visible { outline: 2px solid var(--accent); outline-offset: 2px }` dentro de `overflow: hidden` (`.group-list` 120, cartões 2136, 3596, 4934) | Anel de foco cortado nas bordas. | `outline-offset: -2px` ou `box-shadow: inset` dentro de `.group-list`. |
| A4 | Sem `-webkit-touch-callout` nem `user-select`. Imagens 1669–1670, 1675, 2429, 4217, 3825. Link real no cartão da Agenda `<a href="?casa=...">` (2135). | No iPhone, segurar o dedo abre "Salvar imagem"; segurar cartão da Agenda abre pré-visualização de link; segurar texto seleciona. | `img, .press, .pino { -webkit-touch-callout: none; user-select: none }`; cartão da Agenda vira `<button>`. |
| A5 | `input[type="search"]::-webkit-search-cancel-button { filter: invert(0.6) }` (262) | Glifo nativo do WebKit, outro no Chrome. | `appearance: none` + "x" próprio (padrão de 491/631). |
| A6 | `--font-body` com Geist via Google Fonts `display=swap` (19, 83–84) | Em Android/Windows troca de fonte visível (FOUT). | Aceitar `system-ui` como final ou self-host com `preload`. |
| A7 | Tailwind Play CDN (22): classes só existem depois do script. | Possível flash com painéis empilhados em primeira carga lenta. | `.hidden { display: none !important }` no `<style>` próprio. |
| A8 | Scrollbar nativa da página em desktop (296, 299). | Barra cinza na borda da janela, fora da coluna. | `html { scrollbar-width: thin; scrollbar-color: #3a3a3c transparent }` + `::-webkit-scrollbar`. |

Já coberto: tap-highlight (94); placeholder (263–265); `.switch` com `appearance:none`; `.bare`; nenhum `<select>`, date/time/number/color, textarea ou radio; nenhum `alert(`/`confirm(`/`prompt(`; controles de vídeo ocultos (291).

### B) Mobile e responsividade

| # | Onde | Onde quebra | Correção |
|---|---|---|---|
| B1 | **Sheets fixas × teclado do iOS.** Reserva (479–534), Login (622–638 + 3903–3912). Sem `visualViewport`; só `focarDepois` com 380 ms (3957–3960). | iPhone: teclado não redimensiona o layout viewport; sheet em `bottom-0` fica atrás do teclado; botão principal some ao digitar. Em PWA o teclado `tel` não tem "Done". | `visualViewport.addEventListener('resize')` ajustando `bottom` da sheet; `enterkeyhint` em 505, 509, 3903, 3943. |
| B2 | **Scroll-chaining atrás das sheets.** `openReservationModal` (3407), `openMenu` (3761), `abrirLogin` (3868), `abrirEscolha` (3718), `openVagaModal` (5047) não travam o scroll; `overflow=hidden` só em Vibes (3027) e Onboarding (4167). Sem `overscroll-behavior`. | Ao chegar ao fim da sheet, a página de trás rola; no iOS elástico. | `.sheet { overscroll-behavior: contain }` e `body { position: fixed; top: -scrollY; width: 100% }` ao abrir. |
| B3 | `max-h-[92vh]` (481, 554, 624), `max-h-[90vh]` (540), `max-h-[70vh]` (616) vs `100dvh` no mapa (363). | Safari: sheet até ~8% mais alta que o visível; grabber e "x" saem da tela. | `max-height: 92dvh` com fallback `92vh`. |
| B4 | Herói `h-[400px]` (1829), capa `h-[460px]` (3215), rail `h-[240px]` (1862), miniatura Vibes `h-[212px]` (3205), mapa da casa `h-[160px]` (2976). | iPhone SE (667 px): capa ocupa ~83%; CTA abaixo da dobra. Paisagem: só imagem. | `height: min(400px, 52dvh)` e `min(460px, 58dvh)`; `aspect-ratio` no rail. |
| B5 | Rodapé do herói 1845–1851: `t-headline` sem `truncate` ao lado de `btn-primary sm` `nowrap`. | 320–360 px: texto quebra em 2–3 linhas dentro dos 400 px. Julgamento, não medido. | `truncate` no `t-headline` (1847) ou `flex-col` abaixo de 360 px. |
| B6 | Segmented "Horário" com 4 opções a 13 px (581–586). | 320 px: ~64 px por segmento para "Sáb 22h30". Julgamento, não medido. | `padding: 0 4px; min-width: 0; overflow: hidden; text-overflow: ellipsis` ou abreviar. |
| B7 | `viewport-fit=cover` sem `env(safe-area-inset-left/right)`; `px-4` fixo. | Paisagem com notch: conteúdo sob o recorte. | `.px-safe` com `max(16px, env(...))` no contêiner (299) e barras fixas (302, 415, 427, 438, 459). |
| B8 | Desktop: sem `@media (hover:hover)`; rails sem barra nem arrasto por mouse. | Só `:active` como feedback; rails só com trackpad. | `.press:hover { opacity: .9 }` sob `(hover:hover)`. |
| B9 | `border-x border-[#1c1c1e]` (299) em qualquer largura. | Linha de 1 px nas bordas do celular. | `md:border-x`. |
| B10 | `user-scalable=no, maximum-scale=1.0` (5). | Pinch-zoom bloqueado; desnecessário, todos os inputs têm ≥16 px. | Manter só `width=device-width, initial-scale=1, viewport-fit=cover`. |
| B11 | `pb-28` (299) × tab bar 49 px + safe area; casa `pb-16` (3224) + CTA (428). | Sem sobreposição. Verificado. | Nenhuma. |
| B12 | Cabeçalho pegajoso da Agenda (2170) × barra compacta (303). | Alinhado. | Nenhuma. |
| B13 | `.vibes-safe-bottom { bottom: 1.5rem }` (283–285) não usa `env()`. | Não quebra; só engana. | Renomear ou comentar. |

### C) Inventário

Tamanhos de texto: escala própria `t-large` 34 ×8 · `t-title1` 28 ×4 · `t-title2` 22 ×9 · `t-title3` 20 ×9 · `t-headline` 17 ×27 · `t-body` 17 ×30 · `t-callout` 16 ×16 · `t-sub` 15 ×69 · `t-foot` 13 ×81 · `t-cap` 12 ×12. Tailwind `text-xs/sm/base/lg`: 0. Arbitrários: `text-[11px]` ×5 (3190, 3611–3613, 4999), `text-[20px]` (521), `text-[22px]` (3191), `text-[30px]` (563). CSS: 9 px (atribuição do mapa 190), 10 px (rótulo da tab 177), 11 px (`.tag-agora`, `.pino-nome`, `.pino-min`, `.selo`), 13 px (`.chip-glass`, `.chip-casa`, `.segmented button`).

Alvos de toque abaixo de 44 px:

| Tamanho | Elemento | Linhas |
|---|---|---|
| 30 px | Fechar "x" da reserva, da vaga, do login; "voltar" do login | 491, 542, 627, 631 |
| 32 px | `.segmented button` (160–161) | 352–353, 384–385, 575–576, 581–584 |
| 32 px | `.chip-casa` (156) | 1744 |
| 36 px | `.stepper` (164) | 517, 519 |
| 36 px | `.btn-secondary` (129): Maps/Uber, Sair, Ler outro, Contrato, Registrar saída | 2360, 2363, 4533, 4782, 5025, 5227 |
| 36 px | `btn-primary sm` com `style="height: 36px"`: Validar entrada, Registrar entrada | 4602, 5225 |
| 36 px | Avatar `w-9 h-9` | 316 |
| 36 px | Chips de função dos freelas `h-9`; voltar "Hoje" `h-9` | 4920, 4958 |
| 40 px | `.icon-glass` (134): voltar, compartilhar, som | 418, 421, 5324 |
| 40 px | Centralizar mapa `w-10 h-10` | 365 |
| só texto | "Ver agenda/Ver tudo", "N promoções já encerraram", "Usar a minha", "Ver a distância daqui", "Ver como o freela vê" | 1814, 1918, 2897, 2959, 5217 |

Confirmados ≥44 px: `.tab-btn` 49, `.row` 48, `.btn-primary` 50/54, `.btn-primary.sm` 44, `h-11` nos botões de texto, `h-12` cancelar, `h-14` em `escolha`, pinos 44, chips de dia ~54.

### D) Bloco "CORREÇÕES DE iPhone" (271–293)

Cobre: disputa `.hidden`/`flex-col` do Vibes; `.safe-bottom`; controles de vídeo ocultos. Coberto fora do bloco: inputs ≥16 px (sem zoom ao focar); `playsinline muted`; `pt-safe`/`pb-safe`; `:active` com `cursor:pointer`.

Falta: `visualViewport` (B1); `dvh` nas sheets (B3); `overscroll-behavior` (B2); `-webkit-touch-callout`/`user-select` (A4); insets laterais (B7); `enterkeyhint` em todos os inputs (505, 509, 3903, 3924, 3943, 4619).

### E) Top 10 por visibilidade numa demo em celular real

1. Botão principal da sheet escondido pelo teclado (B1).
2. Página de trás rola/elástico ao arrastar a sheet (B2).
3. Topo da sheet cortado no Safari com conteúdo longo (B3).
4. Long-press abre callout nativo de imagem/link (A4).
5. Alvos de 30–36 px nos pontos de decisão: "x" das sheets, segmented, steppers, `.btn-secondary`.
6. Checkbox nativo no contrato do freela (A1).
7. Capa de 460 px e herói de 400 px em iPhone de 667 px (B4).
8. Rodapé do herói amontoado a 320–360 px (B5).
9. Troca de fonte visível em Android (A6) e possível flash do Play CDN (A7).
10. Linhas de 1 px nas bordas (B9) e `user-scalable=no` (B10).

## Auditoria C: ritmo visual (espaçamento, alinhamento, tipografia, cor)

Contagens de espaçamento, raios e `style=` inline vieram de `grep`; tipografia e cor foram tabuladas por leitura integral ("≈" onde a contagem é manual).

### A) Frequências

**Espaçamento (classes Tailwind): 328 usos, 74 valores distintos.** Dominantes: `px-4` ×57, `gap-2` ×16, `gap-3` ×16, `gap-0.5` ×16, `space-y-2` ×13, `space-y-3` ×10, `space-y-2.5` ×10, `pt-4` ×10, `pt-2` ×10. Meios-passos (x.5): 66 usos (20%). Valor arbitrário único: `py-[18px]` (3144). Pixels distintos: 18. Inline `style=` com padding/margin: 302, 416 (safe-area), 428, 583, 4602 e 5225 (`height: 36px; padding: 0 14px` sobre `.btn-primary.sm`). Variantes `sm:`/`hover:`: 0.

**Raios: Tailwind 10 classes, CSS 16 valores.** `rounded-full` ×24, `rounded-[18px]` ×10, `rounded-[14px]` ×6, `rounded-xl` ×5, `rounded-t-[28px]` ×4, `rounded-[24px]` ×3, `rounded-[22px]` ×3, `rounded-[10px]` ×2, `rounded-2xl` ×2, `rounded-[12px]` ×1. Raios de container para o mesmo papel: 24, 22, 18, 16, 14, 12, 10 (sete). Inline `border-radius: 27px` ×4 (527, 5121, 5144, 5157) sobre `.btn-primary` (25px).

**Tipografia.** Uma família só (SF Pro → Geist); `font-heading`/`font-body` do `tailwind.config`: 0 usos; `.mono` ×3. Escala `.t-*`: t-large ×7, t-title1 ×3, t-title2 ×8, t-title3 ×8, t-headline ×26, t-body ×25, t-callout ×15 (sempre com `font-semibold`), t-sub ≈62 (≈20 com `font-semibold`), t-foot ≈75, t-cap ×11. Fora da escala: `text-[11px]` ×5 (3190, 3611–3613, 4999), `text-[20px]` (515), `text-[22px]` (3191), `text-[30px]` (560). Pesos: `font-semibold` ≈50, `font-medium` 4, `font-bold` 1 (3191). `tracking-wide` ×3 (3611–3613), `tracking-widest` ×1 (3622). Três "títulos de 15–17px semibold" competindo: `t-sub font-semibold`, `t-callout font-semibold`, `t-headline`. Dois títulos de seção: `t-title2` (Hoje/Freelas) vs `t-title3` (Casa/Gerente).

**Cor.** 14 tokens com redundâncias: `--secondary` = `--label-2`, `--bg-card` = `--fill-1`, `--border-color` = `--fill-2`; `--border-radius`/`--button-radius` 0 usos; `theme.*` do Tailwind: `bg-theme-bg` ×1. Classes: `bg-[#1c1c1e]` ×23, `bg-[#2c2c2e]` ×11, `text-[#636366]` ×8, `text-[#ebebf5]` ×6, `bg-black/60` ×7, `text-neutral-400` ×1 (543). 14 cinzas hex próprios; quatro cinzas médios a menos de 10 unidades (#8e8e93, #98989f, #a3a3a3, #aeaeb2). 8 variantes de opacidade. Hues de destaque: `--accent`, `--live`, `--danger`, #0a84ff (212), #64d2ff (3574). Mesmo verde em três alfas (0.16, 0.18, 0.2). Hairlines em três alfas (0.12, 0.14, white/10). Gradiente inline em 5320 duplicando `.scrim-hero`. Inline com cor: 3574, 3576, 4146, 4971, 5152, 4224–4228 (paleta própria do mini-mapa), 4231, 4768 (`'#ff9f0a'`/`'#ff453a'` em vez de `var(--accent)`/`var(--danger)`), 5320. Cada casa carrega ~9 campos de tema que ninguém lê (só `primary`).

### B) Escala mínima proposta

- **Espaçamento (7):** 4 · 8 · 12 · 16 · 20 · 24 · 32. `gap-1.5`→`gap-2`, `gap-2.5`/`gap-3.5`→`gap-3`, `space-y-2.5`→`space-y-3`, `space-y-3.5`→`space-y-4`, `space-y-7`/`-9`→`space-y-8`, `p-3`/`p-3.5`/`py-[18px]`→`p-4`. Exceção documentada: `gap-0.5` como entrelinha.
- **Raios (5 papéis):** 28 sheet · 24 herói · 18 cartão e `.group-list` · 14 caixa aninhada · 12 thumbnail · `full` para pílulas, botões e avatares.
- **Tipo (7 níveis):** t-large · t-title1 · t-title2 (seção, única) · t-headline (título de cartão e de linha) · t-body · t-sub (`font-semibold` só para valor) · t-foot · t-cap. Sai: t-title3, `t-callout font-semibold`, tamanhos arbitrários.
- **Cor (papéis):** `--fill-1/2/3`, `--label-1` #fff, `--label-1b` #ebebf5 (texto sobre imagem), `--label-2` #98989f, `--label-3` #636366 (hoje #8e8e93, indistinguível), `--sep`, `--accent`, `--live`, `--danger`, `--info` #64d2ff. Chips semânticos com um alfa (0.16).

### C) Inconsistências concretas (29)

1. Bloco de título muda de aba para aba: Hoje 312 `space-y-3.5` com `h-9`; Agenda 350 `space-y-0.5` + `!mt-3` + `pt-3`; Ingressos 382 `space-y-3.5` + `pt-3`; Freelas 4957 `space-y-3` com botão de 36px; Gerente 4528 `flex items-end`.
2. Gap entre seções: Hoje 328 `space-y-9` · Agenda 359 `space-y-8` · Casa 3224 `space-y-7` · Freelas/Gerente 376/400 `space-y-7` · Ingressos 389 `space-y-4`.
3. Título de seção: `secaoHtml` 1681–1688 (`t-title2`, `space-y-3`) vs Casa 2965/2973/3142/3161/3184/3203 (`t-title3`, `space-y-2.5`) vs Gerente 5213/5262 vs 4658 (`t-cap`).
4. Herói 1829: chips `top-4 left-4` e texto `left-5 right-5 bottom-5`; Casa 3218 `left-4 right-4 bottom-5`.
5. Cartão do trilho 1862 `rounded-2xl`; vibes na Casa 3205 `rounded-[14px]`; cartão da agenda 2136 `rounded-[18px]`.
6. Thumbs de lista: 1879 `w-[60px]`, 2138 `w-[72px]`, 2934 `w-16`, 3679 `w-[52px]`. Gaps `gap-3.5` (1878, 1977, 2137) vs `gap-3` (2933, 483).
7. Estados vazios: 1924 `group-list row` · 2177 `py-8` · 4593/5215 `py-6` · 1961 `pt-10` · 3687 `pt-12`.
8. Rodapé "encerradas" 1918 fora do padrão de link de seção (1814).
9. Chip de dia 2204 `rounded-2xl px-3.5 py-2` vs chip de filtro do Freelas 4920 `h-9 px-4 rounded-full`.
10. Divisor de promoções 2121 hairline e alfa próprios; `p-3.5` em 2137 vs `p-4` nos demais cartões.
11. `px-1` como micro-gutter: 371, 2183, 3677, 3889, 557.
12. 3144 `py-[18px]`; `--inset` 64/74/48 (3167, 3188, 5111) caso a caso.
13. 3190–3191 `text-[11px]` + `text-[22px] font-bold leading-7`, onde `t-cap` + `t-title2` servem.
14. "Branco apagado" em cinco versões: `#ebebf5` (1841, 1883, 1982, 3151, 4109, 5085), `#aeaeb2` (1848, 3221), `white/80` (5338, 5346), `/70` (5340), `/60` (5335).
15. 3611–3613 reimplementam `.t-cap` em 11px.
16. Ingresso 3596 `rounded-[22px]`; caixa do QR 3620 `p-3 rounded-[14px]` vs 4151 `p-2.5 rounded-[12px]`; botão cancelar 3631 `h-12` vs `h-14` em escolha.
17. 3574 chip "Entrada validada" com hue #64d2ff única; chips verdes com alfa 0.2/0.18/0.16.
18. 3677 `t-cap px-1` vs `px-4` em todos os outros.
19. 3655 `mt-3` dentro de `gap-2`; 3652 `mb-2`.
20. Sheets 481/554/624 `px-4 pt-2` vs vaga-modal 540 `px-5` + fechar absoluto + `text-neutral-400`.
21. Botões: `.btn-primary` 50/25 sobrescrito inline para 54/27 ×4; `.sm` 44 sobrescrito para 36 ×2. Alturas em uso: 54, 50, 48, 44, 36, 56.
22. Vaga-modal: `space-y-6` (5093, 5125) vs `space-y-5` (5134, 5149).
23. 4768 cores hardcoded; 4772 `box-shadow: inset 0 0 0 1.5px` inline; bordas 0.5/1.5/2/3px.
24. Câmera 4669 `rounded-[22px]` com moldura 4671 `rounded-[18px]`.
25. Onboarding gutter 24px (217, 649) contra 16px no app; Vibes `px-4` no topo (5322) e `px-5` no rodapé (5330).
26. 5320 gradiente inline; 4224–4228 paleta própria do mini-mapa.
27. Avatar de pessoa em três fundos/tamanhos (315, 560, 4966); logos em 9 tamanhos.
28. Ícones em 10 tamanhos; `w-[17px]` (323) e `w-7` (4774) únicos.
29. `tailwind.config` quase morto; `bg-[#1c1c1e]` ×23 e `text-[#636366]` ×8 em vez de classe/token.

### D) Top 10 correções (impacto ÷ esforço)

1. Alinhar o cabeçalho das abas (312–320, 350–353, 382–383, 4957–4963) e o gap de seção (`space-y-8`).
2. Um raio de cartão (18): `rounded-[22px]` ×3, `rounded-2xl` ×2, `rounded-[10px]` ×2, `.group-list` 16→18. Herói 24, aninhado 14, thumb 12, resto `full`.
3. Classe `.card` e `.chevron` substituindo `bg-[#1c1c1e]` ×23 e `text-[#636366]` ×8.
4. Um título de seção (`secaoHtml` em toda parte); aposentar `t-title3`.
5. Botões sem inline (527, 4602, 5121, 5144, 5157, 5225); `.btn-primary.lg` se 54 for desejado.
6. Rótulos ad hoc → `.t-cap` (3611–3613, 3190, 4999); 3191 → `t-title2`.
7. Um "branco apagado" (`--label-1b`); decidir c-3.
8. Chips semânticos por classe com alfa 0.16; `var(--accent)`/`var(--danger)` em 4768.
9. Gutters e padding interno: `p-4` em 2137, 2932, 3144; inset 16 nos heróis; `px-4` no `t-cap` de 3677; onboarding 24→16 ou declarado; vazios com `py-8`.
10. Varrer meios-passos (66 usos), mantendo só `gap-0.5`.

Bônus sem impacto visual: apagar tokens redundantes (69–71, 85–86) e o bloco `theme` do `tailwind.config`; apagar campos de tema das casas que ninguém lê.
