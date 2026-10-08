# Plano: cinco estados e ritmo visual no protótipo

Data: 2026-10-07. Branch: `worktree-ux-cinco-estados` (worktree em `.claude/worktrees/ux-cinco-estados`). Plano escrito pelo Fable 5.1; execução delegada a subagents com Opus 5.5, uma tarefa por vez, cada uma com commit próprio.

## Padrão cobrado

Toda superfície interativa entrega cinco estados por padrão: feliz, vazio, erro, carregando e celular. Botão que dispara ação tem estado de carregamento. Formulário que envia tem estado de erro. Lista de dados tem texto de vazio. Nenhum estilo padrão do navegador sobrevive. Ritmo visual: espaçamento, alinhamento, hierarquia tipográfica e disciplina de cor.

## Diagnóstico (resumo das três auditorias)

Detalhes com linhas em `auditoria.md` nesta pasta. Resposta curta à pergunta "estamos seguindo o padrão?": em parte. A base visual está acima da média e algumas telas já cumprem os cinco estados; o que falta é sistemático, não pontual.

O que já atende:
- Nenhum `alert()`, `confirm()`, `prompt()`, `<select>` ou picker nativo. `confirmar()` e `escolher()` existem e são usados.
- Sistema visual com tokens, uma família tipográfica, escala `.t-*` nos tamanhos do iOS, um destaque só. Nenhum `text-xs`/`text-sm` do Tailwind.
- Estados vazios com texto nas abas Ingressos, Agenda, busca do Hoje, Freelas e Equipe. A aba Ler QR tem loading, erro de permissão e erro de leitura em três tons: é a referência interna.
- Celular: safe areas no topo e na base, inputs com 16px ou mais (sem zoom ao focar), `playsinline muted` nos vídeos, barra inferior sem sobreposição.

O que não atende:
- **Carregando:** de 16 botões que mutam estado, 1 tem estado em voo ("Quero essa vaga"). Confirmar reserva, receber código, verificar código, validar entrada, assinar contrato e registrar turno são instantâneos. Mapa e rota carregam sem indicador. Não existe spinner reutilizável nem skeleton.
- **Erro:** o formulário de reserva depende do balão nativo do navegador (`required` sem `novalidate`). O código de verificação aceita qualquer número; a classe de erro existe e nunca é aplicada. Toast só tem variante de sucesso. Compartilhar falha em silêncio.
- **Vazio:** Vibes sem vídeo fica preto; busca da portaria sem resultado fica em branco; painel do gerente sem noite mostra zeros.
- **Celular:** sheets ficam atrás do teclado do iOS (sem `visualViewport`), a página de trás rola junto (sem `overscroll-behavior`), `vh` em vez de `dvh`, capa de 460px em iPhone de 667px, long-press abre menu nativo de imagem, alvos de toque de 30 a 36px nos pontos de decisão.
- **Estilos nativos que sobrevivem:** checkbox do contrato, foco de input removido sem substituto, "x" nativo do campo de busca, `user-scalable=no`.
- **Ritmo visual:** 74 valores distintos de espaçamento (20% em meios-passos), 7 raios para o mesmo papel de cartão, 3 estilos de "título de 15–17px" competindo, 2 títulos de seção, cabeçalho de aba montado de um jeito em cada aba, 14 cinzas, mesmo verde em 3 alfas, cores hardcoded no leitor de QR que quebram a troca de identidade.

## Como verificar cada tarefa

- Servidor local da worktree: porta 8766 (`index.html`). Moldura de captura: porta 8767 (`frame.html` no scratchpad da sessão).
- Captura: `shot.sh "<query do app>" <nome> [largura] [altura] [js] [pre]`. O PNG sai em `scratchpad/shots/`; abrir com a ferramenta Read para olhar.
- Larguras obrigatórias: 320x568 (menor), 390x844 (padrão), 430x932 (maior).
- Estados que não se alcançam por URL abrem com o parâmetro `js` (ex.: `openReservationModal('id','moi','lista')`, `openMenu()`, `openHouseDetail('moi')`, `abrirLogin()`); localStorage semeia-se com `pre`.
- Sem regressão: as capturas de referência de antes das mudanças ficam em `scratchpad/shots/ref-*.png`.

## Regras para quem executa

- Só `index.html` muda, salvo quando a tarefa disser outra coisa. Nada de arquivo novo na raiz.
- Reusar os primitivos existentes: tokens em `:root`, escala `.t-*`, `.btn-primary`, `.row`, `.group-list`, `confirmar()`, `escolher()`, `#toast-success`. Nunca `alert()`, `confirm()`, `prompt()`, `<select>` ou picker nativo.
- Português do Brasil nos textos de interface, no mesmo tom das telas atuais (curto, direto, sem exclamação).
- Commit por tarefa, mensagem no padrão do repositório (`feat:`/`fix:`/`chore:` em português), sem co-autor.
- Ao terminar, relatar: o que mudou (linhas), capturas feitas (nomes) e o que ficou de fora.

## Tarefas

Ordem de execução: sequencial, uma por subagent (Opus 5.5), porque todas editam o mesmo `index.html`. Cada tarefa termina com commit e capturas. Linhas citadas são do commit `d79f3cc`; depois da T1 elas deslocam, então procurar pelo nome da função ou pelo trecho.

Ordem: T1 → T10 → T2 → T3 → T4 → T5 → T6 → T7 → T8 → T9 → T11 → TF.

### Eixo 1: cinco estados

- [ ] **T1. Primitivos de feedback** (base para as demais)
  - CSS, junto dos outros componentes do bloco "SISTEMA VISUAL": `.spinner` (anel de 18px, `border: 2px solid`, cor `currentColor` com topo transparente, `animation: spin`), `.spinner.lg` (36px, substitui o anel inline do modal da vaga, linha 5120); `.campo-erro` (borda `--danger` em `.row` ou `.otp-caixa`); `.msg-erro` (`t-foot c-danger`, `role="alert"`). Sob `prefers-reduced-motion`, o spinner vira um anel estático; por isso todo estado em voo leva texto junto.
  - JS: `emVoo(botao, texto)`: desabilita o botão, guarda o `innerHTML`, troca por `<span class="spinner"></span>texto`, devolve uma função que restaura. `aguardar(ms)` retorna Promise. Toast ganha tipos: `mostrarToast(msg, { tipo: 'sucesso' | 'erro' | 'neutro', acao: { rotulo, fn } })`; `showSuccessToast` continua existindo como atalho para `tipo: 'sucesso'`. Ícones: `circle-check` verde, `circle-alert` em `--danger`, `info` em `--label-2`. Toast com ação dura 5 s, sem ação 2 s.
  - JS: `vazioHtml({ icone, titulo, texto, acaoHtml })` reproduzindo exatamente o bloco de 3651–3656, e `vazioCompactoHtml(texto)` reproduzindo 4592–4594. Trocar as ocorrências existentes (3651–3656, 3671–3675, 4592–4594, 4959, 5213–5218, 2177–2180) pelos helpers sem mudar o visual.
  - Usos imediatos: "Áudio mutado" (4344) e "Modo visitante" (4055) passam a `tipo: 'neutro'`.
  - Verificação: capturas `t1-toast-erro`, `t1-toast-neutro` (via `js`), `ref-ingressos-390` igual ao antes.

- [ ] **T2. Painel de reserva: erro inline e envio em voo**
  - `<form>` da linha 491 ganha `novalidate`; `required` nativo deixa de ser o mecanismo.
  - Validação própria em `handleReservationSubmit`: nome com 2+ caracteres; WhatsApp com 11 dígitos, usando `mascararTelefone` (3850) no `oninput`, como o login. Erro: `.campo-erro` na `.row` do campo, `.msg-erro` logo abaixo com texto curto ("Diga seu nome para a lista." / "Celular com DDD, 11 números."), `aria-invalid="true"`, foco no primeiro campo inválido. Erro some ao digitar.
  - Envio: `emVoo(botão, 'Confirmando…')`, `aguardar(800)`, então o fluxo atual (fechar, toast, ir para Ingressos). Backdrop e botão de fechar ficam inertes durante o voo.
  - `cancelReserva` (3692): depois do `confirmar()`, em voo no botão "Retirar nome" por 600 ms.
  - Verificação: capturas `t2-reserva-erro` (submeter vazio logado; usar `pre` para semear sessão logada, ver `definirSessaoDemo`), `t2-reserva-voo` (capturar durante os 800 ms com `wait` curto), em 320 e 390.

- [ ] **T3. Login por celular: envio, verificação e erro de código**
  - `enviarCodigo` (3970): em voo "Enviando…" por 900 ms antes de trocar para a etapa do código. Enter com número incompleto mostra `.msg-erro` "Faltam números. Celular com DDD." sob o campo, em vez de retornar em silêncio (3971).
  - Código: o aviso "Simulação: nenhuma mensagem é enviada." passa a dizer também o código válido da demo, por exemplo "Simulação: o código é 2468." Ao completar 4 dígitos, etapa "Verificando…" (spinner + texto no lugar do botão de reenviar ou abaixo das caixas) por 700 ms. Código diferente do válido: caixas com `.otp-caixa.erro` (246, já existe), `.msg-erro` "Código incorreto. Confira e tente de novo.", campo limpo e foco de volta. Reenviar continua com a contagem.
  - `concluirLogin` (4017): "Continuar" em voo "Entrando…" 600 ms. `sairDaConta` (4033) passa por `confirmar({ titulo: 'Sair da conta?', acao: 'Sair', perigo: true })`.
  - Verificação: capturas `t3-login-enviando`, `t3-login-verificando`, `t3-login-codigo-erro`, em 320 e 390.

- [ ] **T4. Portaria e painel do gerente**
  - `confirmPresence` (4642): botão "Validar entrada" em voo "Validando…" 500 ms; depois toast `sucesso` com ação "Desfazer" (5 s) que reverte `marcarPresenca`.
  - `confirmarLeitura` (4788): em voo "Confirmando…" 500 ms antes de re-renderizar.
  - `filtrarListaGerente` (4626): sem resultado, mostrar `vazioCompactoHtml('Nenhum nome com "<busca>".')`.
  - `htmlPainelGerente` (4558): sem noite em destaque, `vazioCompactoHtml('Nenhuma noite publicada. Os números aparecem quando a próxima noite estiver na agenda.')` no lugar dos zeros.
  - Leitor QR: quando não há pendentes, a seção "Simule a leitura" mostra uma linha `t-foot c-3` "Nenhum ingresso pendente para simular." em vez de sumir (4657).
  - Verificação: capturas `t4-lista-busca-vazia`, `t4-painel-sem-noite`, `t4-toast-desfazer` (modo gerente: ver `toggleManagerMode` 4291; semear reservas com `pre` em `gyn_reservas`).

- [ ] **T5. Freelas: mesma régua para todas as ações**
  - `assinarContrato` (5174), `enviarNotaFiscal` (5192), `registrarTurno` (5269), "Exportar para a contabilidade" (5252): em voo com texto ("Assinando…", "Enviando…", "Registrando…", "Exportando…") entre 500 e 900 ms, depois o toast existente. "Candidatar" (5164) passa a usar `.spinner.lg` e `emVoo` em vez do anel inline.
  - "Minhas escalas" (4990): quando vazio e a pessoa já se candidatou/assinou, mostrar `vazioCompactoHtml('Nenhuma escala ainda. Quando uma casa aprovar você, ela aparece aqui.')`; sem candidatura, a seção continua sem aparecer.
  - Verificação: capturas `t5-vaga-assinando`, `t5-escalas-vazio`.

- [ ] **T6. Vibes e Mapa: vazio, erro e carregamento**
  - Vibes (`renderVibes` 5286): sem casa com vídeo, `vazioHtml` com ícone `video-off`, "Nenhum vídeo hoje", "As casas publicam os vídeos da noite por aqui." e botão "Ver agenda". Cada `<video>` ganha `onerror`: o cartão troca para o poster com a logo e uma linha "Vídeo indisponível" (sem botão quebrado). Eventos `waiting`/`playing` ligam e desligam um `.spinner.lg` central com texto "Carregando…".
  - Mapa (`criarMapaBase` 2496, `montarMapaCasa` 2988): sobre a moldura, uma camada `glass` com `.spinner` + "Carregando mapa…" até o evento `load` do Leaflet ou do estilo MapLibre (com teto de 6 s; passado o teto, some sem erro, porque os tiles Esri cobrem o fallback).
  - Rota (`desenharRota` 2727, `buscarRotaReal` 2276): no cartão do pino, "Traçando rota…" enquanto a chamada ao OSRM (Open Source Routing Machine) está em curso; se cair no arco ilustrativo, a linha de tempo recebe "· estimativa" em `c-3`.
  - `compartilharCasa` (3275): sem `navigator.share`, tenta `clipboard.writeText` e mostra toast `neutro` "Link copiado"; sem clipboard, toast `erro` "Não deu para compartilhar neste navegador."
  - Verificação: capturas `t6-vibes-vazio` (via `js` que esvazia `videoUrl` antes de `renderVibes()`), `t6-mapa-carregando` (`wait` curto), `t6-video-erro`.

### Eixo 2: celular e estilos padrão do navegador

- [ ] **T7. Sheets no celular: teclado, elástico e altura**
  - Toda sheet (`#reservation-modal` 479, menu 554, login 624, vaga 540, escolha 616): `max-height` em `dvh` com fallback `vh` na linha anterior; `.sheet { overscroll-behavior: contain }`.
  - Travar o documento ao abrir qualquer sheet e destravar ao fechar: helper `travarFundo()`/`destravarFundo()` com `body { position: fixed; top: -scrollY; width: 100% }` e restauração do `scrollY`. Usar em `openReservationModal`, `openMenu`, `abrirLogin`, `abrirEscolha`, `openVagaModal` e nos respectivos `close*`/`fechar*`. Vibes e Onboarding continuam com o mecanismo que já têm.
  - Teclado do iOS: um único listener em `visualViewport` (`resize` e `scroll`) que, quando há sheet aberta, define `--teclado` (altura ocupada) e as sheets usam `bottom: var(--teclado, 0px)`. Sem `visualViewport`, nada muda.
  - `enterkeyhint` nos inputs: reserva nome `next`, WhatsApp `done`, telefone do login `send`, código `done`, nome do login `done`, buscas `search`.
  - Verificação: capturas `t7-reserva-aberta-320`, `t7-login-aberto-320` (grabber e "x" visíveis; conteúdo longo rola dentro da sheet). Teclado não se simula no headless; registrar como "não verificado em dispositivo".

- [ ] **T8. Controles e toque: nada nativo sobrevive, alvos de 44 px**
  - Checkbox do contrato (5141): classe `.check` própria com `appearance: none`, 24 px, borda `--fill-3`, marcado com fundo `--live` e check em SVG inline (`::after`); área de toque pela `.row`.
  - Foco: remover `outline: none !important` de `input:focus` (248–251); `.search-field:focus-within, .row:focus-within { box-shadow: inset 0 0 0 1.5px var(--primary) }`; `.group-list :focus-visible { outline-offset: -2px }`.
  - `img, .press, .pino, .tab-btn { -webkit-touch-callout: none; -webkit-user-select: none; user-select: none }`; o cartão da Agenda (2135) deixa de ser `<a href>` e vira `<button type="button">` com o mesmo `onclick`.
  - Campo de busca: `::-webkit-search-cancel-button { appearance: none }` e botão "x" próprio (padrão de 491) que aparece quando há texto.
  - Alvos de toque: "x" das sheets (491, 542, 627, 631) sobem para 36 px visuais com área de 44 (`::before` transparente ou `p-1 -m-1`); `.segmented` para 36 px; `.stepper` para 44 px; `.btn-secondary` para 40 px e os `style="height: 36px"` (4602, 5225) removidos; links de texto ("Ver agenda", "Usar a minha", "Ver a distância daqui", "N promoções já encerraram", "Ver como o freela vê") ganham `min-height: 44px; display: inline-flex; align-items: center`.
  - Viewport (linha 5): `width=device-width, initial-scale=1, viewport-fit=cover`. Coluna (299): `md:border-x`. `.px-safe` com `max(16px, env(safe-area-inset-left/right))` no contêiner e nas barras fixas (302, 415, 427, 438, 459).
  - `<style>` próprio ganha `.hidden { display: none !important }` antes de tudo, como seguro contra o flash do Tailwind Play CDN.
  - Verificação: capturas `t8-contrato-check` (modal da vaga na etapa do contrato), `t8-busca-com-x`, `t8-hoje-390` idêntica à `ref-hoje-390` exceto pelas bordas laterais.

- [ ] **T9. Alturas fixas que não cabem em celular pequeno**
  - Herói do Hoje (1829): `height: min(400px, 52dvh)`; capa da casa (3215): `min(460px, 58dvh)`; cartão do rail (1862): `aspect-ratio: 4 / 5` com `height: auto`; miniatura Vibes (3205) e mapa da casa (2976) mantêm, são pequenas.
  - Rodapé do herói (1845–1851): `truncate` no `t-headline` e no detalhe; abaixo de 360 px, botão passa para a linha de baixo (`flex-wrap` com o botão `basis-full`).
  - `.segmented button`: `padding: 0 4px; min-width: 0; overflow: hidden; text-overflow: ellipsis; white-space: nowrap`.
  - `@media (hover: hover) { .press:hover { opacity: 0.9 } }`.
  - Verificação: capturas `t9-hoje-320x568`, `t9-casa-moi-320x568`, `t9-hoje-390`, `t9-menu-320` (segmented "Horário" com os quatro rótulos inteiros ou com reticências, nunca vazando).

### Eixo 3: ritmo visual

- [ ] **T10. Tokens e classes: zero mudança visual, muito menos dispersão** (roda logo depois da T1, para as tarefas seguintes usarem as classes novas)
  - CSS: `.card { background: var(--fill-1); border-radius: 18px; }` substitui `bg-[#1c1c1e] rounded-[18px]` e variações de cartão (23 usos de `bg-[#1c1c1e]`); `.chevron { color: var(--label-3); }` substitui `text-[#636366]` ×8; `--label-1b: #ebebf5` com `.c-1b` substitui `text-[#ebebf5]`, `text-[#aeaeb2]` e `text-white/80|70|60` em texto sobre imagem. `--label-3` continua `#8e8e93` (mudar o contraste fica fora desta rodada).
  - Chips semânticos: `.chip-live`, `.chip-accent`, `.chip-info` (`--info: #64d2ff`) com fundo em alfa 0.16, substituindo os `style="background: rgba(…)"` de 3574, 3576, 4146, 4971, 5152. Em 4768, `var(--accent)`/`var(--danger)` no lugar dos hex (corrige a troca de identidade no leitor de QR).
  - Botões: `.btn-primary { border-radius: 9999px }`, `.btn-primary.lg { height: 54px }` para as folhas; remover os `style="height…; border-radius…"` de 527, 5121, 5144, 5157 e os `style="height: 36px; padding…"` de 4602 e 5225 (viram `.btn-secondary`).
  - Rótulos: 3611–3613, 3190, 4999 passam a `t-cap`; 3191 passa a `t-title2`; `text-[20px]` (515/521) e `text-[30px]` (560/563) viram classes da escala mais próxima (`t-title3`, `t-title1`).
  - Limpeza: apagar `--secondary`, `--bg-card`, `--border-color`, `--border-radius`, `--button-radius` e o bloco `theme` do `tailwind.config`, depois de confirmar por grep que nada os lê (`bg-theme-bg` em 299 passa a `bg-black`). Não mexer nos campos de tema das casas (dados, não estilo).
  - Verificação: todas as capturas `ref-*` refeitas e comparadas; a diferença aceitável é zero ou subpixel.

- [ ] **T11. Ritmo: cabeçalhos, seções, raios e meios-passos** (última, porque é a mais subjetiva)
  - Cabeçalho de aba único: linha de 36px (data ou voltar à esquerda, avatar à direita) + `h1.t-large` + subtítulo `t-sub c-2`, com o mesmo `space-y` em Hoje (312–320), Agenda (350–353), Ingressos (382–383), Freelas (4957–4963) e Gerente (4528). Gap entre seções `space-y-8` em todas as abas e na Casa.
  - Título de seção único: `secaoHtml` (1681–1688, `t-title2`) também na Casa (2965, 2973, 3142, 3161, 3184, 3203) e no Gerente (5213, 5262). `t-title3` fica reservado para título dentro de cartão; se sobrar sem uso, apagar.
  - Raios por papel: 28 sheet · 24 herói · 18 cartão e `.group-list` (120: 16→18) · 14 aninhado · 12 thumb · `full` pílulas. Trocar `rounded-[22px]` (3596, 4142, 4669), `rounded-2xl` (1862, 2204), `rounded-[10px]` (336, 3168).
  - Gutters: `p-4` em 2137, 2932, 3144; `left-4 right-4` nos heróis (1837, 4106) e `px-4` no rodapé do Vibes (5330); `px-4` no `t-cap` de 3677; chip de dia da Agenda (2204) no mesmo formato do chip de filtro do Freelas (4920); estados vazios com `py-8`.
  - Meios-passos: `gap-1.5`→`gap-2`, `gap-2.5`/`gap-3.5`→`gap-3`, `space-y-2.5`→`space-y-3`, `space-y-3.5`→`space-y-4`, `py-3.5`→`py-4`, `px-3.5`→`px-4`, `space-y-7`/`-9`→`space-y-8`. Mantém `gap-0.5` (entrelinha) e registra a exceção no comentário do bloco "SISTEMA VISUAL".
  - Onboarding mantém gutter de 24px (tela imersiva), registrado no mesmo comentário.
  - Verificação: capturas de todas as abas em 390 e 320, comparadas às `ref-*`; o subagent descreve cada diferença e confirma que é intencional. Qualquer tela que ficou pior volta atrás.

### Fechamento

- [ ] **TF. Revisão final (Fable)**: repetir todas as capturas `ref-*` nas três larguras, comparar lado a lado, ler o diff completo, rodar a checagem de `alert(|confirm(|prompt(|<select` e registrar a seção "Revisão" deste plano.

## Revisão

_(preenchida ao fim)_
