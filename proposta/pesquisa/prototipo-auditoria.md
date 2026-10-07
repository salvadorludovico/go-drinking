# Auditoria do protótipo `index.html` — por que ele é "razoável mas confuso"

Arquivo auditado: `/Users/salvador/Code/side-projects/go-drinking/index.html` (3440 linhas, sem alterações locais em relação ao commit `38212fd`). Documentos de referência: `base/05-escopo-mvp.md`, `base/07-modulo-freelas.md`, `base/08-jornadas.md`. Capturas principais em `capturas/` (iPhone 390x844, relógio simulado em sexta 22:30 via `?dia=sex&hora=22:30`).

## Resumo em uma frase

A parte de descoberta (Hoje, Agenda, página da casa) é boa e tem um motor de horário sólido; a confusão vem de **três públicos (cliente, operador da casa, freelancer) e duas ferramentas de apresentação (relógio simulado, troca de identidade visual) empilhados dentro de um único app de consumidor**, com o mesmo conteúdo repetido em três telas e com vocabulário que muda a cada passo do fluxo (lista, mesa, reserva, ingresso).

Uma observação prévia: o pedido menciona as abas "Casas" e "Fidelidade". **Nenhuma das duas existe na versão atual.** Fidelidade foi removida no redesenho (`git log -S idelidade` mostra que ela existiu até o commit `38212fd`). Não há aba nem lista de casas; a única forma de ver uma casa sem noite em destaque é a busca do Hoje. Porém `base/07-modulo-freelas.md:72` ainda diz que a entrada dos Freelas é "um cartão no fim da aba Casas" — o documento está desatualizado em relação ao protótipo.

---

## 1. Inventário de telas

### 1.1 Barra inferior (4 abas) — `index.html:371-389`

| Aba | Como chegar | O que faz | Onde está |
|---|---|---|---|
| **Hoje** (inicial) | abre o app; `?aba=hoje` (aliases `discover`, `promos`) | Cabeçalho com data e "N casas abertas agora", busca, cartão herói da noite em destaque (com botão "Entrar na lista"/"Reservar mesa"), carrossel "Abertas agora", "Valendo agora" (promoções), "Mais tarde hoje", "Amanhã", "Nesta semana" e, no fim, o cartão "Trabalhe na noite" | HTML `260-294`, render `1405-1462` |
| **Agenda** | aba; `?aba=agenda&agenda=hoje\|amanha\|fds`; links "Ver agenda", "Ver tudo", "Fim de semana" do Hoje | Chips de dia (Hoje, Amanhã, Fim de semana, mais 5 dias) e cartões por casa com horário, entrada e promoções | HTML `297-306`, render `1839-1872` |
| **Vibes** | aba; `?aba=vibes`; miniatura "Vibes" na página da casa | Feed vertical de vídeo em tela cheia (5 casas com `.mp4` local), som, barra de progresso, botão "Ver noite" leva à casa | HTML `340-345`, motor `2594-2783`, render `3366-3436` |
| **Ingressos** | aba; `?aba=ingressos` (alias `reservas`); menu > "Meus ingressos"; automático após reservar | Segmentos Próximos/Passados, cartão com QR ilustrativo, código `GD-xxxx-xxxx`, botão "Retirar nome da lista" | HTML `314-325`, render `2361-2470` |

### 1.2 Telas internas (sem aba)

| Tela | Como chegar | O que faz | Onde está |
|---|---|---|---|
| **Página da casa** | toque em qualquer cartão de noite (Hoje, Agenda, Vibes, busca, Ingressos vazio); `?casa=<id>` | Capa, status, noite selecionada com faixas de entrada e line-up, promoções, miniatura Vibes, "Outras noites", Instagram; barra inferior fixa com preço e "Reservar mesa"/"Entrar na lista"; botão compartilhar copia `?casa=<id>` | `1971-2127`, topo/CTA `348-369` |
| **Trabalhe na noite (Freelas)** | `?aba=freelas`; cartão no fim do Hoje (`283`); menu > "Trabalhe na noite" (`482`); painel da casa > "Ver como o freela vê" (`3297`) | Perfil do freela com Cadastro Nacional da Pessoa Jurídica (CNPJ) "validado", "Minhas escalas" com etapas, "Vagas abertas" com filtro por função | `309-311`, render `2994-3067` |
| **Painel da casa (modo gerente)** | **só** pelo menu do avatar > interruptor "Modo gerente" (`494`). Não tem parâmetro de URL | "Na lista", "Já entraram", lista de nomes com "Validar entrada", "Equipe freela" com registro de entrada/saída e "Fechamento para a contabilidade", e um segundo controle de "Simular horário" | `2785-2871` |

### 1.3 Modais e folhas

| Modal | Como chegar | O que faz | Onde está |
|---|---|---|---|
| **Reserva / lista** | botão do herói no Hoje; barra fixa da página da casa | Nome, WhatsApp, pessoas (1-10), faixas de entrada, promoções valendo; "Confirmar"/"Reservar" grava em `localStorage` e pula para Ingressos | `392-444`, `2176-2291` |
| **Vaga (freela)** | "Ver termos" numa vaga; "Contrato" numa escala | Termos → "aprovando" (aprovação automática em 1,5 s) → contrato com aceite → assinado | `447-458`, `3124-3270` |
| **Menu do avatar** | avatar no topo do Hoje (`264`) — único lugar onde o avatar existe | Bloco "Conta" (Meus ingressos, Trabalhe na noite) e bloco "Demonstração" (Modo gerente, Identidade visual, Dia/Hora simulados) | `461-519`, `2489-2592` |
| **Toast** | qualquer ação | Mensagem de confirmação | `522-525`, `2293` |

### 1.4 Parâmetros de URL — `index.html:1122-1201`

`?casa=<id>`, `?aba=hoje|agenda|vibes|ingressos|freelas` (e os nomes antigos `discover|promos|reservas`), `?agenda=hoje|amanha|fds` (só com `aba=agenda`), `?dia=sex&hora=22:30` (relógio simulado). Navegar dentro do app **não** atualiza a URL (não existe `pushState`/`popstate`), então o gesto "voltar" do navegador sai do app e um link só pode ser compartilhado para a casa, nunca para a noite.

### 1.5 Troca de papéis — como é apresentada

- **Cliente**: identidade fixa `USUARIO = { nome: 'Salvador', telefone: '(62) 99000-0000' }` (`1154`), sobrescrita pelo último nome digitado no modal de reserva (`2276-2280`). Menu mostra "Cliente desde set/2026" fixo (`471`). Não há cadastro, login nem visitante.
- **Operador da casa**: interruptor "Modo gerente" escondido no bloco "Demonstração" do menu do cliente (`491-495`). A casa operada é `activeHouseId || 'moi'` (`2790`), ou seja, **depende de qual casa você abriu por último sem passar pelo "voltar"** (o voltar zera `activeHouseId` em `2130`). Na prática quase sempre é o Môi, e não há seletor de casa. A barra inferior some (`1904`), a única saída é "Sair" (vai para Hoje) ou "Ver como o freela vê".
- **Freelancer**: não é papel, é tela. Não há troca de identidade; o freela é outro objeto fixo `freelaDemo = { nome: "Salvador", cnpj: ... }` (`2934`), separado de `USUARIO`. Se o cliente mudar o nome na reserva, o freela continua "Salvador". Quando a tela Freelas está aberta, a barra inferior marca **Hoje** como ativa (`1906`), então visualmente o freela está "dentro do Hoje".

---

## 2. Problemas de arquitetura de informação

### 2.1 O mesmo conteúdo em três lugares (Hoje × Agenda × Casa)

- O Hoje não é "hoje": ele termina com "Amanhã" e "Nesta semana" (`1451-1456`), com links para a Agenda. A Agenda tem chip "Hoje", que repete o Hoje em outro formato, e chip "Amanhã", que repete a seção "Amanhã" do Hoje. Nas capturas `01b-hoje-pagina-inteira.png` e `02-agenda.png`, as mesmas noites (Cajuína, Beat Proibido, Môi, Fluxo) aparecem nas duas abas com layouts diferentes.
- A página da casa tem "Outras noites" (`2051-2069`), que é a agenda daquela casa. São três visões da mesma tabela `programacao`, e o usuário não tem como saber qual é a "certa".
- O próprio código admite a dúvida: `const ABA_INICIAL = 'hoje'; // 'agenda' é a candidata a virar a inicial` (`1142`).
- Promoções estão em quatro lugares: "Valendo agora" do Hoje (`1555`), "Promoções de hoje" (`1580`, que usa o mesmo `id="secao-valendo"`), rodapé dos cartões da Agenda (`1771`) e a página da casa (`2030`). A antiga aba Promos sobrevive só como alias de URL que rola até essa seção (`1940-1943`).

### 2.2 Falta o que o usuário procuraria: a lista de casas

Não existe diretório de casas. Uma casa sem noite próxima (ou que o usuário quer ver pelo nome) só aparece pela busca do Hoje, que substitui todo o conteúdo do Hoje (`1418-1423`). A busca não existe na Agenda nem no Vibes.

### 2.3 Três públicos num app só

- **Freelas** (fora do MVP segundo `05` e `08:11`, `08:217`) tem **quatro portas de entrada**: cartão no fim do Hoje (`283`), item no menu do cliente em "Conta" (`482`), link no painel da casa (`3297`) e `?aba=freelas`. O comentário em `280-281` diz que fica no fim "de propósito", mas o mesmo item está promovido no menu "Conta" do cliente.
- **Operador** dentro do app do cliente contradiz `05` F5: "Tela web (não app) com a lista do dia" (`05:85`). O painel ainda mistura portaria (público: segurança na porta) com fechamento contábil de freelas (público: gerente/financeiro) e com a ferramenta de demonstração de horário.
- **Ferramentas de apresentação** misturadas com o produto: "Identidade visual" (troca a cor de destaque e **substitui o avatar do usuário pelo logo da casa**, `2536-2557`), "Dia simulado", "Hora simulada" — duplicados no menu (`497-515`) e no painel da casa (`2854-2868`), além do parâmetro `?dia&hora`. Quem recebe o link sem contexto encontra um menu de perfil que é 70% controles de demonstração (`08-menu-perfil.png`).

### 2.4 Vocabulário que muda a cada passo

Um único fluxo usa seis nomes para a mesma coisa:

| Momento | Texto | Linha |
|---|---|---|
| Botão (bar) | "Reservar mesa" | `1471`, `2118` |
| Botão (boate) | "Entrar na lista" | idem |
| Campo do modal, mesmo para bar | "Nome na lista" | `416` |
| Toast | "Mesa reservada" / "Você está na lista" | `2283` |
| Aba e menu | "Ingressos" / "Meus ingressos" | `388`, `479` |
| Cartão | "vale uma entrada" | `2420` |
| Cancelar, mesmo para mesa | "Retirar nome da lista" | `2424` |
| Painel | "Nomes confirmados", "Validar entrada" | `2846`, `2807` |
| Variáveis/aliases | `reservations`, `reservas`, `gyn_reservas` | `1150`, `1887` |

"Ingresso" sugere algo pago; no MVP não há pagamento (`05` seção 5). Na captura `07-ingressos-com-reserva.png`, o toast diz "Mesa reservada" sobre a aba "Ingressos" com um botão "Retirar nome da lista".

### 2.5 Marca

O produto se chama GoDrinking nos documentos, mas a palavra não aparece no `index.html`. O título da página e o nome do Progressive Web App (PWA) são **"LUAN"** (`index.html:7`, `manifest.json`), que é o nome do parceiro dono das casas (`08:15`), e o ícone é o logo do Beat Proibido (`9`). O `logo-casas/README.txt` também chama o app de "LUAN". Para um sócio, isso parece um app feito para uma pessoa, não um produto.

### 2.6 Contradições com o MVP documentado

| Item | Documento | Protótipo |
|---|---|---|
| Conta, CPF, OTP, LGPD (F1) | obrigatório, visitante não reserva (`05:31-37`) | não existe; reserva com nome e WhatsApp livres, usuário fixo |
| Capacidade e lista de espera (F3) | 121º vai para espera (`05:46-48`) | toda reserva nasce `status: 'confirmada'` (`2272`), sem limite, sem bloqueio de duplicata |
| Cancelamento até 2h antes (F3) | `05:44` | pode cancelar até o fim da noite (`2422`) |
| QR de uso único (F4) | `05:52-55` | QR é desenho pseudoaleatório (`2327`), sem leitura; painel valida por botão, inclusive reservas de outros dias |
| Operação da casa em tela web (F5) | `05:58` | modo escondido dentro do app do cliente |
| Busca por nome e exportação no painel (F5) | `05:59-60` | não existem |
| Painel self-service, vagas publicadas pela casa | fora do MVP (`05:111`) | painel publica "vagas" e "fechamento contábil" |
| Freelas | fora do MVP (`08:217`) | quatro entradas visíveis |
| Vibes | fora (`05:13`), mantido como demo (`08:139`) | aba principal |
| Fidelidade | fora | removida — coerente |

### 2.7 Coisas que fingem funcionar

- **Painel da casa mostra as reservas do próprio aparelho** (`2793`, lê `localStorage`). "Na lista: 2" é o próprio Salvador. Conta todas as datas e não só a noite de hoje, embora o rótulo seja "Na lista" (`09b-painel-gerente-inteiro.png`).
- **Aprovação de vaga automática** em 1,5 s com spinner "Aguardando a aprovação de..." (`3244-3252`).
- **"CNPJ validado"** é um selo fixo (`3051`).
- **"Exportar para a contabilidade"** só mostra um toast (`3335`).
- **"Mostre seu QR na portaria para registrar a entrada no turno"** (`3084`) — o freela não tem QR em lugar nenhum.
- **"Assinatura eletrônica com validade jurídica (Lei 14.063/2020)"** (`3225`) sobre um checkbox.
- **QR "vale uma entrada"** é ilustrativo e nunca é lido.
- `videoUrl` do Vimeo em cada casa (`570`, `640`...) não é usado como vídeo; só serve de sinalizador de "tem vídeo". O vídeo real vem de `logo-casas/<id>.mp4` (`3398`). Se alguém trocar a URL, nada muda.
- Objeto `theme` de cada casa (fontes `Share Tech Mono`, `Playfair Display`, raios de borda, cores de fundo) — só `theme.primary` é usado (3 ocorrências). As fontes nem são carregadas. Cerca de 120 linhas de dado morto que sugerem um recurso de "tema por casa" que foi abandonado.

### 2.8 Modelo de dados que não representa a realidade

`programacao` só tem `diaSemana` (`552-569`). Tudo vira evento semanal eterno: "SUBCULT 3.0", que é uma festa itinerante numerada, aparece "Amanhã" e todo sábado (`01b-hoje`, `03-vibes`); "Rataria Popular" com "Transmissão ao vivo do jogo do Brasil" (`821`) repete toda quarta; Beat Proibido tem "pré-jogo/pós-jogo" toda sexta. Não há como cadastrar evento com data, edição especial, feriado ou casa fechada numa semana. Isso afeta diretamente a J5 (nós publicamos a programação) e a confiança da J0.

---

## 3. Saúde do código

### 3.1 Estrutura

| Bloco | Linhas | Tamanho |
|---|---|---|
| `<head>` + Tailwind config + CSS | 1-243 | ~240 |
| Markup estático | 244-527 | ~280 |
| Dados das casas (`housesData`) | 530-915 | ~385 |
| Motor de tempo (funções puras) | 916-1140 | ~225 |
| Estado, init, URL | 1141-1202 | ~60 |
| Hoje, Agenda, navegação, casa, reserva, ingressos, menu, painel, Vibes, Freelas | 1203-3436 | ~2230 |

Tudo em um `<script>` global. Renderização por `innerHTML` com template string e 55 `onclick="..."` inline que interpolam ids. Há ~20 variáveis globais mutáveis (`currentTab`, `abaAnterior`, `activeHouseId`, `isManagerMode`, `identidadeId`, `reservations`, `USUARIO`, `clockOffsetMs`, `mostrarEncerradas`, `agendaDia`, `noiteSelecionadaId`, `pessoasReserva`, `ingressosFiltro`, `isVibesMuted`, `vibesObserver`, `vibesEngineInitialized`, `escalas`, `freelaFiltro`, `vagaModalState`...). A cada 60 s, `redesenharTudo()` (`1132`) refaz a tela inteira.

Dependências: `cdn.tailwindcss.com` (o próprio Tailwind avisa no console que não é para produção) e `unpkg.com/lucide@latest` (`25`) — versão não fixada, pode quebrar sem nenhuma mudança no repositório. Fonte Geist carregada mas o CSS prioriza a do sistema.

### 3.2 Bugs encontrados

1. **Ingresso mostra o preço errado.** `ingressoHtml` calcula a entrada no horário de início da noite: `infoEntrada(prog, occ, occ.inicio)` (`2373`). Reservando o Môi às 22:30, quando a entrada é R$10, o cartão diz "ENTRADA Free até 20h" (`07-ingressos-com-reserva.png`). Promete algo que a casa não vai cumprir na porta.
2. **Vagas de freela já começadas continuam abertas.** `contextoVaga` usa `ocorrencia()` (`2973`), que devolve a noite em andamento; o turno começa antes da noite (`antesMin`). Às 22:30 de sexta a tela oferece "Garçom · Hoje 17h – 2h30" com botão "Ver termos" (`10-freelas.png`).
3. **Vibes nunca re-renderiza.** É montado uma única vez (`2629`) e o relógio de 60 s pula a aba (`1167`). Mudar o horário simulado deixa "Rolando agora"/"Amanhã" desatualizados no feed. A ordem dos vídeos é a do array (`3374`), não a relevância: sexta 22:30, com quatro casas abertas, o primeiro vídeo é Subcult "Amanhã" (`03-vibes.png`).
4. **Casa do painel depende de histórico invisível** (`2790`), como descrito em 1.5.
5. **Painel conta e valida reservas de qualquer data** (`2793`, `2881`): dá para "validar entrada" de uma reserva de quinta numa sexta.
6. **Reserva duplicada**: nada impede reservar a mesma noite várias vezes (`2275`).
7. **Tela Freelas acende a aba Hoje** (`1906`) e o "voltar" dela sempre vai para Hoje (`3039`), mesmo vindo do painel da casa.
8. **Toast cobre o título** ao entrar no painel e ao reservar (`09b`, `07`), porque fica no topo, sobre o título grande.
9. `confirmPresence` grava em `localStorage` sem `try` (`2885`), ao contrário das outras gravações — em modo privado do Safari antigo lança exceção.
10. Capas ausentes para Cajuína, Mosaic, Vernissage e Fluxo geram 404 no console a cada render (fallback funciona, mas o ruído é constante).

### 3.3 Evoluir ou jogar fora?

**Tratar como descartável, extraindo duas peças.** Motivos para não evoluir: sem backend, sem rotas, sem componentes, estado global com efeitos colaterais em toda função de render, HTML por concatenação de strings, dependências de CDN sem versão e um modelo de dados que não suporta eventos datados. Tudo o que o `08` lista como "falta" (conta, persistência, concorrência, QR real, admin) exige uma base diferente.

Peças que valem ser portadas, com testes:

- **Motor de tempo** (`916-1140`, mais `infoEntrada`/`faixasEntradaHtml` em `1246-1307`): funções puras (`ocorrencia`, `statusNoite`, `statusPromo`, `entradaVigente`, virada da meia-noite, "a noite de ontem ainda é hoje às 2h"). É o ativo mais valioso do protótipo e responde às três perguntas do `tasks/todo.md`.
- **Esquema de faixas de entrada e janelas de promoção** (`entrada: [{ate, valor, nota}]`, `promocoes: [{inicio, fim}]`): bom ponto de partida para o modelo de dados real, acrescentando data e exceções.

O design visual (padrão iOS, hierarquia de tipografia, cartão herói, página da casa) serve como referência de layout para o produto, não como código.

---

## 4. Capturas de tela

Chrome headless via `playwright-core` instalado no scratchpad, 390x844, escala 2x, relógio simulado em sexta 22:30 (exceto a 13). Pasta: `capturas/` (seleção das principais).

| Arquivo | Tela |
|---|---|
| `01-hoje.png`, `01b-hoje-pagina-inteira.png` | Hoje (a versão inteira mostra a barra inferior no meio por ser captura de página completa, não é bug) |
| `02-agenda.png` | Agenda, chip Hoje |
| `03-vibes.png` | Vibes, primeiro vídeo |
| `04-ingressos-vazio.png` | Ingressos sem reservas |
| `05-casa-moi.png`, `05b-casa-moi-inteira.png` | Página do Môi |
| `06-modal-reserva.png` | Modal de reserva |
| `07-ingressos-com-reserva.png`, `07b-...` | Ingresso criado (bug do preço) |
| `08-menu-perfil.png` | Menu do avatar |
| `09-painel-gerente.png`, `09b-...` | Painel da casa |
| `10-freelas.png`, `10b-...` | Trabalhe na noite (bug da vaga já começada) |
| `11-modal-vaga.png` | Termos da vaga |
| `12-busca-funk.png` | Busca |
| `13-hoje-terca-14h.png` | Hoje sem casa aberta (o Hoje vira "Amanhã" + "Nesta semana") |

---

## 5. Arquitetura de informação recomendada

### 5.1 App do cliente (MVP) — 3 abas

| Aba | Conteúdo | Substitui |
|---|---|---|
| **Agora** (ou "Hoje") | Só a noite corrente: herói, abertas agora, promoções valendo, mais tarde hoje. Quando não há nada hoje, mostra a próxima noite com destaque, sem virar uma agenda | Hoje sem as seções "Amanhã" e "Nesta semana" |
| **Explorar** | Seletor de dia no topo (Amanhã, Fim de semana, datas) e, abaixo, lista de casas com busca e filtro por gênero/setor. É aqui que mora o diretório de casas que hoje não existe | Agenda + busca + a "aba Casas" que os documentos citam |
| **Minhas reservas** | Próximas e passadas, QR, cancelamento com a regra das 2h. Conta e perfil ficam num ícone no topo desta aba | Ingressos + menu do avatar (só a parte "Conta") |

Vibes: se for mantido no piloto (decisão `«#10»` do `08`), entra como **quarta aba** ou, melhor, como faixa de vídeos dentro do Agora e da página da casa. A recomendação é a faixa: no `05` ele não move a métrica, e uma aba inteira de vídeo desloca a pergunta principal ("onde eu vou agora?"). Se for para a demo dos sócios, aba; se for para o piloto, faixa.

Página da casa continua como tela empilhada, aberta a partir de qualquer aba, com URL própria por noite (`?casa=moi&noite=moi-sexta`) e histórico do navegador funcionando.

Vocabulário único: escolher **um** substantivo para o objeto ("reserva" serve para mesa e lista) e usar o tipo como atributo: "Reserva · Mesa para 4" e "Reserva · Lista free até 23h". Nada de "ingresso" enquanto não houver venda.

Remover do app do cliente: Modo gerente, Identidade visual, Dia/Hora simulados (passam a ser só `?dia&hora` ou um painel de demonstração acessível por gesto escondido), cartão e item de menu "Trabalhe na noite".

### 5.2 Onde ficam operador e freelancer

| Público | Veículo | Conteúdo |
|---|---|---|
| **Operador da porta** | Web app separado (rota `/portaria`, login da casa), otimizado para celular em pé | Lista da noite de hoje, busca por nome, validação por QR ou toque, contadores "confirmados / entraram" (o número do Luan, J0) |
| **Gerente / nós (admin)** | Web separado (`/admin`), desktop primeiro | Cadastro de noites com data e recorrência, faixas de entrada, promoções, exportação da lista, métricas de show-rate. No MVP só nós usamos (`«#3»`) |
| **Freelancer** | Fora do MVP. Quando entrar, produto ou rota separada (`/trabalhe`), com link no rodapé do site e no painel da casa, nunca dentro da navegação do cliente | Vagas, contrato, escalas. O lado da casa (escalar, registrar turno, fechamento) vai para o `/admin` |

Para a demo aos sócios, o roteiro de quatro toques do `08:38` (hoje à noite → a casa → a lista da porta → o número de quem apareceu) funciona melhor com **duas janelas lado a lado** (app do cliente e portaria) do que com um interruptor escondido no menu do cliente: deixa claro que são produtos diferentes e que a reserva feita de um lado aparece do outro.
