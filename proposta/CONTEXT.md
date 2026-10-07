# Glossário do domínio

> Status: **proposta.** Os documentos atuais usam "reserva", "lista", "ingresso" e "evento" como sinônimos, e é daí que vem boa parte da confusão do protótipo. Este glossário fixa um significado por palavra. Termos marcados com (?) precisam de confirmação com o Luan.

## Quem

| Termo | Significado |
|---|---|
| **Cliente** | Quem sai à noite. Usa o app para decidir para onde ir e garantir a entrada. |
| **Visitante** | Cliente sem conta. Vê tudo, não garante nada. |
| **Casa** | Local fixo que abre com recorrência: bar ou boate. Tem endereço, capacidade e uma equipe. Ex.: Môi, Point, Fluxo. |
| **Bar** | Casa onde o produto principal é sentar e consumir. A ação natural é **reservar mesa**. |
| **Boate** | Casa onde o produto principal é a pista. A ação natural é **entrar na lista** ou comprar ingresso. Algumas casas são as duas coisas em horários diferentes (?). |
| **Atração** | Artista ou DJ. Não tem endereço. Aparece numa Noite de uma Casa. Ex.: Beat Proibido. |
| **Produtora** | Marca de festa sem casa fixa, que ocupa locais diferentes. Vende ingresso fora do app (Sympla, Shotgun). Ex.: Cultura Subcult. |
| **Dono** | Quem decide se a casa usa o app e quem paga por ele. |
| **Operador da porta** | Quem confere a entrada na noite. Usa o painel da casa, em pé, com fila e som alto. |
| **Admin** | Nós. No piloto, somos nós que publicamos a programação. |

## O quê

| Termo | Significado |
|---|---|
| **Noite** | Uma abertura da casa em uma data: horário, nome da noite, atrações, faixas de entrada e promoções. Pode ser **recorrente** ("toda quinta é Girls&Wine") ou **avulsa** ("final da Copa"). Substitui "evento" e "programação" nos textos novos. |
| **Programação** | O conjunto das Noites de uma casa numa semana. É uma visão, não um objeto. |
| **Faixa de entrada** | Preço da entrada válido até um horário. "Free até 20h, depois R$10" são duas faixas. |
| **Promoção** | Oferta de consumo com janela de validade dentro de uma Noite. "2 taças por R$30 até 22h". Não é um destino do app, é um atributo da Noite. |
| **Lista** | Nome na lista de uma Noite. Garante uma condição de entrada (free ou desconto) até um horário. Não garante lugar físico. Custo zero para o cliente. |
| **Mesa** | Lugar físico reservado para um grupo numa Noite. Em bar, costuma ser grátis com tolerância de atraso. Em boate, costuma vir com consumação mínima. |
| **Camarote / Área VIP** | Espaço premium com capacidade fixa, quase sempre com **consumação mínima** e, no mercado, com **sinal** pago antecipado (?). |
| **Consumação mínima** | Valor que o grupo se compromete a consumir. Se gastar menos, paga a diferença. |
| **Sinal** | Valor pago antecipado para segurar mesa ou camarote, abatido da consumação. É o principal remédio do mercado contra o não comparecimento. |
| **Garantia** | Nome genérico do que o cliente recebe: lista, mesa ou camarote. Vira um **Passe** com QR na carteira do app. |
| **Passe** | O cartão com QR que o cliente mostra na porta. Um por Garantia. No protótipo atual se chama "Ingresso", o que confunde com ingresso pago. (?) |
| **Ingresso** | Direito de entrada **pago**. Fora do MVP; quando existir, também vira Passe. |
| **Check-in** | Validação do Passe na porta. É o único dado que prova que a pessoa veio. |
| **Comparecimento** | Percentual de Garantias que fizeram check-in. A métrica central do piloto. Os docs antigos chamam de "show-rate". |
| **No-show** | Garantia sem check-in. Em mesa e camarote, custa dinheiro para a casa. |

## Integrações

| Termo | Significado |
|---|---|
| **Zig** | Sistema de pagamento sem dinheiro (cashless) e Ponto de Venda (PDV) usado pelas casas. Sabe quem entrou e quanto gastou. O usuário chama de "ZigPay". |
| **Base de clientes da casa** | Quem já consumiu na casa, segundo a Zig. Pertence à casa, não a nós. |
| **Funil completo** | Viu a Noite → garantiu → fez check-in → consumiu R$X. As três primeiras etapas são nossas; a última é da Zig. |
