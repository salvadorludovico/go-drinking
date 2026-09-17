# Do Guardanapo ao Prazo: o processo em 5 etapas

> Para: Salvador (CTO). Objetivo: sair das anotações de reunião e chegar num prazo
> que você possa defender na frente dos sócios sem chutar.

## Por que não dá para estimar hoje

As anotações atuais (`01`, `02`, `03` + overview da reunião) misturam três coisas
que precisam ficar separadas:


| Camada        | Exemplo do material atual                                      | Serve para       |
| --------------- | ---------------------------------------------------------------- | ------------------ |
| **Desejo**    | "experiência igual ao Uber", "fidelidade Prata/Ouro/Diamante" | Alinhar visão   |
| **Decisão**  | "pagamento fica fora do MVP", "CPF obrigatório para reservar" | Travar escopo    |
| **Requisito** | "reserva só é criada se houver vaga na capacidade do turno"  | Estimar e testar |

Estimativa só existe na terceira camada. Enquanto `02-definicoes-pendentes.md`
tiver ~60 checkboxes em aberto, qualquer prazo é ficção — e o risco é seu, porque
quem promete data é o CTO.

---

## Etapa 1 — Fechar as decisões bloqueantes (1 reunião, ~2h)

Não são as 60 perguntas do doc `02`. São **12** que mudam arquitetura ou prazo.
As demais podem ser decididas durante o desenvolvimento sem retrabalho.


| #  | Decisão                                                        | Por que trava o prazo                                                                |
| ---- | ----------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| 1  | Reserva confirma automática ou o gerente aprova?               | Muda o modelo de estado e exige painel em tempo real                                 |
| 2  | Existe capacidade/lotação por noite, ou reserva é ilimitada? | Sem capacidade, não há concorrência nem overbooking — economiza ~1 semana        |
| 3  | Quem opera o painel da casa no dia 1: gerente ou nós?          | "Nós" permite adiar o painel inteiro para a Fase 2                                  |
| 4  | Qual a casa piloto e quem é o dono da operação lá?          | Sem um humano responsável, o piloto não gera dado                                  |
| 5  | Check-in é QR code validado ou confiança/lista impressa?      | QR exige scanner, tolerância a offline e endpoint de validação                    |
| 6  | Login: só telefone+OTP, ou e-mail+senha, ou social?            | OTP tem custo por SMS e muda todo o onboarding                                       |
| 7  | CPF é obrigatório no cadastro ou só na primeira reserva?     | Obrigatório no cadastro derruba conversão; afeta a métrica do piloto              |
| 8  | Fidelidade paga (Ouro R$15/mês) entra no MVP?                  | Se sim, pagamento**volta** para o escopo — contradiz a decisão da reunião         |
| 9  | Vernissage/Sympla: integramos ou só linkamos?                  | Integração de terceiro é o item de maior variância                               |
| 10 | Vibes (vídeos) fica no MVP?                                    | É o maior custo de infra e de curadoria de conteúdo                                |
| 11 | Push notification no dia 1?                                     | PWA no iOS exige "adicionar à tela de início" — impacta a promessa de remarketing |

**Formato de saída:** uma tabela `Decisão | Escolha | Data | Quem decidiu`.
Decisão sem dono e sem data volta a ser discussão em duas semanas.

## Etapa 2 — Escrever requisitos como comportamento (2-3 dias, você sozinho)

Cada feature vira uma frase testável. Não "sistema de reservas", mas:

> Dado que a noite de sexta do Môi tem 120 vagas e 120 reservas confirmadas,
> quando um usuário tenta reservar, então o app oferece lista de espera e não cria reserva.

Isso é o `05-escopo-mvp.md`. Serve para três coisas ao mesmo tempo: estimar,
testar e provar para o sócio que a feature está pronta. **Se você não consegue
escrever o critério de aceite, a decisão da Etapa 1 não foi fechada de verdade.**

## Etapa 3 — Estimar por fatia vertical, não por camada (meio dia)

Não estime "backend: 2 semanas, frontend: 3 semanas". Estime fatias que entregam
valor de ponta a ponta, porque só elas podem ser demonstradas e cortadas:

- Sim: "Usuário reserva mesa e recebe confirmação" (backend + app + notificação)
- Não: "CRUD de eventos"

Para cada fatia: estimativa otimista (O), provável (M), pessimista (P).
Use **PERT**: `(O + 4M + P) / 6`. Some as fatias e aplique os multiplicadores da
Etapa 4. A vantagem de PERT sobre chute único é que ele te obriga a nomear o
pessimista — e é o pessimista que você vai viver.

## Etapa 4 — Converter esforço em data de calendário (1 hora)

Aqui é onde a maioria dos prazos morre. Três multiplicadores:

1. **Você não tem 40h/semana de código.** Reunião, suporte, decisão, contexto.
   Um dev sênior em produto novo entrega ~25h/semana de trabalho de fato.
2. **Integração e polimento = +30%** sobre a soma das fatias.
3. **Piloto não é lançamento.** Reserve 2 semanas entre "funciona" e "confiável".

Fórmula honesta:

```
semanas = (soma_PERT_em_horas x 1.3) / 25   ->  arredonde para cima
data    = hoje + semanas + 2 (estabilizacao)
```

Apresente aos sócios como **faixa com data de recompromisso** ("MVP no piloto
entre 15 e 29 de outubro; reavalio a faixa no dia 20 de setembro"), nunca como
data única. Data única transforma qualquer atraso de 3 dias em quebra de
confiança.

## Etapa 5 — Instrumentar o piloto antes de expandir (contínuo)

O piloto tem que responder uma pergunta de negócio, não técnica. Sugestão:

> **Das pessoas que reservaram pelo app, quantas apareceram?**

Se o show-rate for alto, o app tem valor para a casa e a assinatura mensal se
justifica. Se for baixo, o problema é o produto, não a escala — e não adianta
plugar as outras 6 casas. Defina o número-meta **antes** de subir, com o Luan.

---

## Como isso vira a conversa com os sócios

O que eles querem ouvir não é a data. É que existe um método:

1. "Fechamos 12 decisões — aqui estão, assinadas."
2. "Cada decisão virou N comportamentos testáveis."
3. "Cada comportamento tem estimativa de 3 pontos."
4. "A soma, com a produtividade real de 1 dev, dá esta faixa."
5. "Reavalio a faixa nesta data. Se escorregar, você fica sabendo antes, não depois."

Esse é também o argumento da sua participação societária: você não está vendendo
horas de código, está vendendo previsibilidade de entrega e a decisão técnica que
evita queimar caixa (ex.: manter pagamento fora do MVP, não construir um Zig do zero).

## Sequência recomendada

```
Semana 0 | Etapa 1 (reuniao de decisoes)   <- faca isso na quarta
Semana 0 | Etapa 2 (requisitos)  +  UX/prototipo em paralelo
Semana 1 | Etapas 3 e 4 -> apresentar a faixa de prazo aos socios
Semana 1+| Execucao, com a Etapa 5 ja instrumentada
```
