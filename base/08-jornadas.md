# Jornadas do Produto Mínimo Viável (MVP) — GoDrinking

> Status: **rascunho para a reunião de decisões** (Etapa 1 do [`04-processo-notas-para-prazo.md`](04-processo-notas-para-prazo.md)). As 13 decisões bloqueantes continuam abertas, então toda bifurcação que depende delas está marcada no próprio diagrama.

## 1. A pergunta que este documento responde

Não é "como o app funciona". É **o que precisa acontecer, passo a passo, para o Luan querer botar as seis casas dele para rodar nisso.**

Consequência de escopo, decidida em 17/09/2026: monetização, modelo de receita e cobrança **saem deste documento**. Primeiro o app tem que ser bom o bastante para o dono querer usar de graça. Quem define preço para um produto que o cliente ainda não quis usar está negociando sozinho.

Escopo coberto: descoberta (programação e promoções), reserva, entrada na porta, e Vibes como porta de entrada. Fora: Freelas, Fidelidade, pagamento, painel self-service.

## 2. Como ler os diagramas

| Marca | Significa |
|---|---|
| `[Tela]` | Já existe no [`index.html`](../index.html) e funciona |
| `[Tela]!` | **Não existe** — é trabalho novo |
| `«#n»` | Ponto que depende da decisão nº *n* do [`04`](04-processo-notas-para-prazo.md) |
| `▲` | Momento da verdade: se falhar aqui, o usuário sai e não volta |

---

## 3. J0 — Luan decide rodar (a jornada que realmente importa)

As outras cinco jornadas existem para alimentar esta. O Luan não compra tela bonita; ele compra **noite cheia com menos trabalho de direct**.

```
Luan abre o app num sabado 22h
        │
   [Hoje]  ── ve as 6 casas dele, cada uma com o que rola AGORA ▲
        │         (se a informacao estiver desatualizada aqui, acabou)
        │
   [Pagina da casa] ── a sexta dele, do jeito que ele posta no Instagram,
        │              so que legivel e com a promocao expirando sozinha
        │
   [Painel da casa] ── 34 nomes na lista de hoje, 19 ja entraram ▲
        │              (este numero nao existe hoje no negocio dele)
        │
   Pergunta que ele faz sozinho: "quantos desses 34 apareceram?"
        │
   ─► show-rate. E a unica metrica que justifica trocar o direct pelo app.
```

**O que o Luan precisa ver na demo, nesta ordem:** hoje à noite → a casa dele → a lista da porta → o número de quem apareceu. Quatro toques. Se a demo passar por cadastro, termo de privacidade ou tela de configuração antes disso, o argumento se dilui.

**Risco não-técnico, e é o maior do piloto:** alguém tem que manter a programação atualizada toda semana. O [`05`](05-escopo-mvp.md) já resolveu isso tirando o painel self-service do escopo — **nós publicamos** `«#3»`. Vale confirmar com ele na reunião, porque é a promessa que sustenta a J5.

---

## 4. J1 — Visitante descobre sem ter conta

Ninguém cria conta para ver o que vai fazer hoje à noite. A conta só pode ser cobrada no momento em que ela dá algo em troca.

```
Chega pelo link do Instagram da casa, sabado 22h30
        │
   [Hoje] ── "Acontecendo agora" + entrada free ate 20h + promo valendo
        │      busca por casa, festa ou estilo
        ├──────────────────────────────┐
        ▼                              ▼
   [Agenda]                      [Pagina da casa]
   a semana inteira              noite de hoje em destaque, resto da semana abaixo
                                       │
                                  toca "Reservar" ──► J2
```

Tudo nesta jornada já existe e está bom. As três perguntas que o [`tasks/todo.md`](../tasks/todo.md) definiu como teste de UX — *o que rola hoje*, *quanto custa entrar agora*, *qual promoção ainda vale* — são respondidas na primeira tela.

**A única lacuna é de negócio, não de tela:** `«#7»` decide se o Cadastro de Pessoas Físicas (CPF) é pedido no cadastro ou só na primeira reserva. Pedir cedo derruba conversão e contamina a métrica do piloto.

---

## 5. J2 — Cliente reserva (o núcleo do MVP)

```
Visitante toca "Reservar"
        │
        ├── ja tem conta ──────────────────────────────┐
        │                                              │
        └── nao tem ──► [Cadastro]!  ▲                 │
                         nome, CPF, e-mail, nascimento │
                         login por telefone + One-Time │
                         Password (OTP) «#6»           │
                         aviso de privacidade (Lei     │
                         Geral de Protecao de Dados,   │
                         LGPD) — nao e opcional        │
                              │                        │
                         volta ao ponto EXATO ─────────┤
                         (sexta do Moi, 4 pessoas)  ▲  │
                                                       ▼
                                          [Modal de reserva]
                                          entrada, promos valendo,
                                          quantas pessoas
                                                       │
                                          tem vaga? «#2»
                                          ┌────────────┴────────────┐
                                     sim  ▼                    nao  ▼
                              «#1» confirma automatico    [Lista de espera]!
                                   ou gerente aprova              │
                                          │                  aviso quando vagar
                                          ▼
                                   [Ingressos] ── QR, data, casa
                                          │
                                   [E-mail de confirmacao]!
                                   [Lembrete no dia]!
                                          │
                                   [Cancelar ate 2h antes]!
```

**Onde este fluxo quebra hoje:** o protótipo tem `USUARIO` fixo em [index.html:1154](../index.html#L1154) — não existe cadastro, login, CPF nem LGPD. Também não existe capacidade, lista de espera nem cancelamento. O modal de reserva em si, com faixas de entrada e promoções valendo, já está pronto e é bom.

**Duas decisões mudam a arquitetura aqui, não só a tela:**

- `«#2»` sem capacidade por noite, não há concorrência nem *overbooking* — economiza cerca de uma semana e apaga o ramo da lista de espera inteiro.
- `«#1»` se o gerente aprova em vez de confirmar automático, o painel em tempo real volta para dentro do MVP (+24h) e a jornada ganha um estado "aguardando" que o cliente precisa entender sem ligar para a casa.

---

## 6. J3 — A noite: a porta

É aqui que o app prova valor para o Luan, e é a jornada com mais risco operacional, porque acontece em pé, com fila, som alto e internet ruim.

```
23h10, fila na porta
        │
   Cliente abre [Ingressos] e mostra o QR (Quick Response)
        │
   Operador com [Painel da casa] na mao
        ├── «#5» escaneia o QR com a camera [FALTA]!
        └── «#5» acha o nome na lista e toca "Validar entrada" [existe]
        │
   ┌────┴────────────────────────────┐
   ▼                                 ▼
 valido                        ja usado as 23h14!
 marca presenca ▲              (mesmo QR, segunda leitura)
   │
   ▼
 Painel atualiza: 34 na lista · 20 entraram ──► volta para J0
```

**Diagnóstico honesto do que existe:** o painel em [index.html:2785](../index.html#L2785) já lista reservas, conta pessoas e valida entrada por botão. O QR em [index.html:2327](../index.html#L2327) é ilustrativo — desenho estável por reserva, sem leitura nem validação de uso único. Não há busca por nome dentro do painel (a busca existente é de casas, na descoberta) e não há tolerância a internet instável.

**O corte mais barato do projeto está aqui.** O [`05`](05-escopo-mvp.md) estima 42h e duas semanas de calendário para a fatia de lista + QR + validação offline. Se a casa piloto aceitar conferência por nome, some. Vale medir na primeira noite antes de construir o scanner: se o operador acha qualquer nome em menos de cinco segundos, o QR é conforto, não necessidade.

---

## 7. J4 — Vibes como porta de entrada

Decidido em 17/09/2026 que Vibes fica na conversa, contra o corte do [`05`](05-escopo-mvp.md). A razão é a J0: é o que faz o Luan e os sócios entenderem o produto em dez segundos. Mas o custo muda conforme o papel que ele recebe.

```
   [Vibes] ── video vertical da festa, autoplay, som sincronizado
        │
        └── "Ver programacao" ──► [Pagina da casa] ──► J2
```

A jornada é de uma seta só, e é essa a força dela: vídeo → intenção → reserva, sem fricção. O que precisa ser decidido `«#10»` não é a tela, é **de onde vem o vídeo**:

| Modelo | Custo | Quando |
|---|---|---|
| Curadoria nossa, poucos vídeos, arquivo fixo | Quase zero — é o que existe hoje | Piloto |
| Casa envia o vídeo, nós publicamos | Baixo, some com a J5 | Piloto, se o Luan quiser |
| Upload aberto, rede de distribuição de conteúdo, moderação | Maior custo de infra do projeto (ver [`06`](06-infra-e-custos.md)) | Fase 2 |

**Recomendação:** manter Vibes no piloto no primeiro ou segundo modelo. O terceiro é o que o [`05`](05-escopo-mvp.md) cortou, e o corte continua certo.

---

## 8. J5 — Nós publicamos a programação

Invisível para o usuário e decisiva para o piloto: se esta jornada emperrar, a J0 mostra informação velha e o Luan desiste na primeira semana.

```
Casa manda a semana (direct, WhatsApp, print do Instagram)
        │
   [Admin]! ── cadastra noite: horario, nome, DJs, promocoes com validade,
        │      faixas de entrada (free ate X, depois R$Y)
        ▼
   Publicado ──► aparece em [Hoje], [Agenda] e [Pagina da casa]
```

Hoje os dados moram em `housesData`, dentro do próprio [`index.html`](../index.html). Não existe tela de administração `«#3»`.

**Pergunta para a reunião, e é operacional, não técnica:** quem manda a programação, em que dia da semana, e o que acontece quando não manda? Uma casa que atrasa a semana derruba a confiança das outras cinco.

---

## 9. Lacunas: protótipo → MVP

| Fatia | Já existe | Falta | Jornada |
|---|---|---|---|
| Conta e identidade (F1) | — | cadastro, CPF, OTP, LGPD, retorno ao contexto | J2 |
| Descoberta (F2) | Hoje, Agenda, página da casa, busca, promoções com validade | — | J1 |
| Reserva (F3) | modal com entrada, promoções e pessoas | capacidade, lista de espera, cancelamento, concorrência | J2 |
| Lista e QR (F4) | QR ilustrativo, Ingressos | leitura de câmera, uso único, tolerância a offline | J3 |
| Operação da casa (F5) | painel com lista, contagem e validação por botão | busca por nome, exportar lista | J3 |
| Comunicação (F6) | — | e-mail de confirmação, lembrete, push | J2 |
| Fundações (F7) | — | *backend* inteiro, deploy, backup, monitoramento, métricas do piloto | todas |

A leitura que interessa: **a descoberta está pronta e a reserva está meio pronta.** O que falta é quase todo invisível — conta, persistência, comunicação e infraestrutura. É exatamente por isso que a demo parece mais avançada do que o projeto está, e é isso que precisa ser dito aos sócios antes que eles concluam sozinhos que falta pouco.

## 10. Os quatro momentos da verdade

Se cada um destes funcionar bem, o resto pode ser mediano e o piloto sobrevive:

1. **Primeira tela, sábado 22h** — a pessoa vê o que rola agora e quanto custa entrar, sem tocar em nada.
2. **Cadastro no meio da reserva** — a pessoa volta exatamente para a noite e a quantidade de pessoas que escolheu. Perder esse contexto é perder a reserva.
3. **A porta** — o operador resolve cada pessoa em menos de cinco segundos, com ou sem internet.
4. **O número do Luan** — quantos dos que reservaram apareceram. Sem esse número, o piloto não conclui nada.

## 11. Fora deste mapa, de propósito

Freelas ([`07`](07-modulo-freelas.md)), Fidelidade, pagamento, painel self-service da casa, integração com Zig ou com o Customer Relationship Management (CRM) acoplado a ela, e integração com Sympla. Todos continuam onde o [`05`](05-escopo-mvp.md) colocou. Monetização sai por decisão de 17/09/2026: vem depois que o Luan quiser rodar.

## 12. Próximo passo

Este documento é a pauta da reunião da Etapa 1. Percorra as seis jornadas na ordem e pare em cada `«#n»`: as sete decisões que aparecem aqui (`#1`, `#2`, `#3`, `#5`, `#6`, `#7`, `#10`) são as que mudam tela, arquitetura ou prazo. As outras seis do [`04`](04-processo-notas-para-prazo.md) podem esperar.

Saída esperada da reunião: tabela `Decisão | Escolha | Data | Quem decidiu`. Com ela fechada, as jornadas viram telas no protótipo e a estimativa do [`05`](05-escopo-mvp.md) deixa de ter faixa dupla.

---

**Criado em:** 17/09/2026
**Base:** [`04`](04-processo-notas-para-prazo.md), [`05`](05-escopo-mvp.md), [`index.html`](../index.html)
