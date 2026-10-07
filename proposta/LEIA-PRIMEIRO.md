# GoDrinking: leia primeiro

> Escrito em 01/10/2026 para quem volta ao projeto depois de um tempo parado. Leitura de uns 15 minutos. As afirmações sobre mercado têm fonte nos arquivos de `pesquisa/`; aqui fica só a conclusão. Onde algo não foi confirmado, está dito.

## 1. Em um minuto

- **O que é:** um app para quem sai à noite em Goiânia ver o que rola hoje em cada bar e boate, quanto custa entrar agora, qual promoção ainda vale, e garantir a entrada (lista free, mesa ou camarote) sem mandar mensagem no direct. Para a casa, é uma lista e uma porta digitais, com o número de quem realmente apareceu.
- **Onde está:** existe um protótipo visual em um único arquivo HTML e oito documentos de planejamento. Não existe backend, cadastro nem banco de dados, e nenhuma das 13 "decisões bloqueantes" listadas em agosto foi tomada. A data de recompromisso que os documentos marcaram para os sócios, 30/09/2026, passou sem entrega.
- **A notícia mais importante da pesquisa:** o núcleo do Produto Mínimo Viável (MVP) já existe no mercado. O REVO, de São Paulo, faz lista, mesa, camarote, portaria por código QR (Quick Response) e Customer Relationship Management (CRM, gestão de relacionamento com o cliente). A **Zig**, que você queria usar como fonte de dados, também vende lista de convidados, reservas, CRM e app do consumidor, e declara à imprensa que quer "ser o aplicativo da balada". Em Goiânia, o BaladAPP, comprado pela Ticketmaster em 2025, domina a venda de ingresso, camarote e mesa para eventos.
- **O espaço que sobra:** ninguém junta, para bares e boates de Goiânia, a programação de hoje, as promoções com horário de validade, a lista e a mesa num lugar só. Esse é o diferencial possível. Ele depende de uma coisa operacional, e não técnica: alguém publicar a programação certa toda semana.
- **A Zig não tem Interface de Programação de Aplicações (API) pública.** O acesso é negociado caso a caso. Pela Lei Geral de Proteção de Dados (LGPD), a base de clientes é da casa, não nossa. "Puxar a base" só funciona com contrato com cada casa e para uso em nome dela.
- **Planos pagos e freelas são negócios diferentes do MVP.** Os dois têm armadilhas que os documentos atuais não viram. A principal: garçom, bartender, caixa e recepção **não podem ser MEI** pela lista oficial da Receita, o que invalida o "só MEI" do módulo de freelas.
- **Minha recomendação:** reposicionar o MVP como "o guia de hoje da noite de Goiânia, com lista na mão", lançar em semanas e não em meses, medir comparecimento numa casa, e deixar mesa paga, Zig, planos e freelas para depois que isso funcionar. O plano está na seção 9.

## 2. O projeto em contexto

**Quem está envolvido.** Você (Salvador) é o responsável técnico (CTO). O Luan S. Barbosa idealizou o projeto, é DJ do duo Beat Proibido e é a ponte com as casas. Há outros sócios citados nas atas, sem nome nos documentos. Um deles propôs o módulo de freelas e tem um escritório de contabilidade.

**Casas mapeadas:** Môi, Point, Mosaic, Vernissage, Fluxo e Cajuína. Os documentos também tratam Beat Proibido (atração) e Cultura Subcult (festa itinerante) como se fossem casas, e é daí que vêm contagens que variam entre 6, 7 e 8 casas. Um documento diz "as seis casas do Luan", outro diz que ele é co-criador do app. **Não está escrito em lugar nenhum se o Luan é dono, sócio ou só conhecido dessas casas.** Isso muda tudo: é a diferença entre ter seis clientes e ter seis contatos.

**Linha do tempo:**

| Quando   | O que aconteceu                                                                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jul/2026 | Protótipo HTML criado em 15/07, com 27 commits num dia só. Documentos 01 a 03: visão, ~60 perguntas, roadmap de "MVP em 4 a 6 semanas".                             |
| Ago/2026 | Documentos 04 a 06: método de estimativa, escopo do MVP com critérios de aceite (265 horas, cerca de 16 semanas), infra. Protótipo ganha motor de horário.          |
| Set/2026 | Redesenho no estilo iOS, aba Agenda, módulo Freelas no protótipo e documento 07. Jornadas (documento 08). Mensagem do Luan sobre um CRM de Brasília acoplado à Zig. |
| Hoje     | Nenhuma das 13 "decisões bloqueantes" foi tomada. Zero código de produto.                                                                                           |

## 3. O escopo, e o que ele vale para cada lado

O escopo que você descreveu tem cinco peças. Abaixo, o que cada uma é e para quem gera valor.

| Peça                       | Como funciona                                                                                                                                        | Valor para o cliente                                            | Valor para o dono da casa                                                                   |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Programação**            | Cada Noite tem data, horário, nome da festa, atrações e faixas de entrada ("free até 20h, depois R$10"). O app calcula o que está acontecendo agora. | Responde "onde eu vou hoje" sem abrir seis perfis de Instagram. | Aparece para quem está decidindo, na hora em que decide.                                    |
| **Promoções do dia**       | Ofertas com janela de validade ("2 taças por R$30 até 22h"). Expiradas aparecem apagadas.                                                            | Motivo para sair cedo e para abrir o app numa terça.            | Enche o começo da noite e os dias fracos, que é onde a casa perde dinheiro.                 |
| **Lista free**             | O cliente toca "Entrar na lista", recebe um Passe com QR, e a condição vale até um horário.                                                          | Garante a entrada free ou com desconto sem pedir no direct.     | Substitui a lista de papel e o WhatsApp do promoter, e mostra quem veio.                    |
| **Mesa e camarote (VIP)**  | Lugar físico para um grupo. Em boate, vendido como pacote com valor revertido em consumação.                                                         | Garante o lugar do grupo antes de sair.                         | É onde está o dinheiro da noite. Também é onde o não comparecimento mais dói.               |
| **Porta e check-in**       | O operador lê o QR ou busca pelo nome. Cada Passe entra uma vez só.                                                                                  | Fila mais rápida.                                               | O número que a casa não tem hoje: dos que garantiram, quantos vieram.                       |
| **Zig (base de clientes)** | Cruzar quem veio pelo app com quanto gastou, a partir dos dados da Zig da casa.                                                                      | Nada diretamente.                                               | Prova de retorno: "os clientes do app gastaram R$X". Depois, campanhas para a própria base. |

**O que os documentos atuais não cobrem desse escopo:**

- **Mesa, camarote e VIP não estão modelados.** O escopo atual (documento 05) fala de "reserva" e "lista" como se fossem a mesma coisa, e o protótipo troca de nome a cada tela ("Reservar mesa", "Nome na lista", "Ingressos"). São três produtos com regras diferentes. O glossário em `CONTEXT.md` propõe um nome para cada.
- **Mesa e camarote sem pagamento têm um problema sério.** Lista free tem comparecimento de 50 a 70% no melhor caso, segundo o próprio REVO. Com sinal pago, sobe para algo entre 85 e 95%. O mercado inteiro (Discotech, Xceed, SevenRooms, a própria Zig) cobra sinal em mesa e camarote. Os documentos tiraram pagamento do MVP, o que é razoável para lista, mas inviável para camarote.
- **"Consumação mínima" como condição de entrada é venda casada** pelo Código de Defesa do Consumidor (CDC), e o Procon autuou uma casa por isso em setembro de 2026. O camarote precisa ser modelado como pacote com valor revertido em consumação, com a redação validada por um advogado.
- **A Zig estava explicitamente fora do MVP** nos documentos 04 e 05. Você agora a colocou dentro. A seção 5 explica por que eu manteria fora do primeiro corte, mas preparada.

## 4. Concorrentes por funcionalidade

Detalhe e fontes em `pesquisa/concorrentes.md`.

| Funcionalidade              | Quem já faz                                                                                                                                                                                 | O que copiar                                                                                                                                                     |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Programação de hoje**     | Agregadores fracos (Curta Mais, VibeIndex, Balada Certa), com dados rasos ou velhos em Goiânia. Shotgun e Sympla para festas com ingresso. **O concorrente real é o Instagram da casa.**    | Seguir casa ou DJ e receber aviso (Shotgun). "X amigos vão" (Shotgun, REVO).                                                                                     |
| **Promoções do dia**        | Ninguém faz bem como produto central. Apps de happy hour existem lá fora, pequenos e locais. Em Goiânia, clubes de 2 por 1 (Prime Gourmet, Duo Gourmet) cobrem drinks, mas não por horário. | É a brecha. Também é a parte mais cara de manter atualizada.                                                                                                     |
| **Lista free**              | REVO, Zig, Sympla, Lets.events, BaladAPP, e o promoter com WhatsApp.                                                                                                                        | Três portas para a mesma lista: app, link do promoter com cota e ranking por check-in, e WhatsApp (REVO). Condição numa frase só: "Lista free até 23h".          |
| **Mesa e camarote**         | BaladAPP (Goiânia), REVO, Zig Mesas, Discotech e Tablelist (EUA), Xceed (Europa).                                                                                                           | Mapa de mesas e upsell (Xceed). Explicar o gasto com um exemplo e pedir sinal por link (Discotech). Cancelamento com um botão e prazo visível.                   |
| **Porta e check-in**        | Todos os acima. Ingresse e Xceed funcionam offline.                                                                                                                                         | Busca por nome, Cadastro de Pessoa Física (CPF) ou telefone quando o QR falha. Funcionar sem internet. O Gulp morreu também porque o porteiro achava o QR lento. |
| **CRM e dados para a casa** | Zig, REVO, SevenRooms, Repediu (CRM que já integra com a Zig).                                                                                                                              | Marcar o cliente sozinho: primeira vez, frequente, quem gasta muito, quem já faltou (SevenRooms). Comparecimento por promoter.                                   |

**Os cinco para estudar antes de desenhar qualquer tela:**

1. **REVO** (São Paulo): é o produto mais parecido com o que vocês querem. Cobra mensalidade da casa, com 7 dias grátis, e oferece app grátis para o público. Diz ter 40 mil usuários em São Paulo. Não achei sinal dele em Goiânia (não confirmado).
2. **Zig**: está dentro das casas e tem R$ 265 milhões captados. Pode ser parceira ou concorrente, e provavelmente será as duas coisas.
3. **BaladAPP**: incumbente de Goiânia em ingresso, camarote e mesa, agora da Ticketmaster. Não faz programação diária nem promoções.
4. **Xceed** (Barcelona): a melhor referência de produto. Cada evento oferece lista, ingresso e mesa no mapa, com portaria offline. Cobra uma taxa por transação.
5. **Discotech** (Estados Unidos): a melhor referência de como explicar e vender mesa.

**Lições de quem morreu** (YPlan, Dojo, IRL, Flowtab, Gulp, TheFork no Brasil):

- **Descoberta sozinha não se paga.** Noventa por cento das pessoas procuram o que fazer uma vez por semana ou menos.
- **Ninguém sobreviveu cobrando do consumidor por descoberta.** Quem sobreviveu cobra da casa, por mensalidade ou por percentual de mesa e ingresso.
- **Comprar crescimento com anúncio não funciona.** No Brasil, a audiência está com promoters e mídia local.

## 5. Zig: API, dados e o que dá para fazer

Detalhe e fontes em `pesquisa/zig.md`.

**O que é a Zig.** Ela faz pagamento sem dinheiro (cashless), Ponto de Venda (PDV) e ingressos. Nasceu da fusão da ZigPay com a NetPDV em 2022 e movimenta mais de R$ 6 bilhões por ano. Em Goiânia, a venda de ingressos dela (Zig Tickets) aparece em vários eventos. Não consegui confirmar quais das casas mapeadas usam o cashless ou o PDV da Zig.

**A API não é aberta.** Não há portal de desenvolvedores, documentação pública nem webhooks documentados. O blog da Zig diz que a API é aberta "conforme necessidade do cliente e viabilidade técnica", ou seja, por negociação comercial. A prova de que a integração existe é o Repediu, um CRM de restaurantes com integração pronta que recebe dados de cliente e de venda.

**De quem é o dado.** A política da própria Zig diz que a casa é a controladora dos dados e a Zig é a operadora. Para nós recebermos esses dados, precisamos de contrato com cada casa. Se quisermos usar os dados para nós mesmos, por exemplo para convidar esses clientes para o app, a LGPD exige consentimento específico de cada pessoa. O CPF dado no caixa do bar foi coletado para pagar, não para marketing de terceiros.

**O CRM de Brasília** que o Luan citou não foi identificado. A Unie, de Brasília, é candidata, mas não há integração dela com a Zig confirmada. Basta perguntar o nome ao Luan.

**Caminho recomendado:**

| Fase        | O que fazer                                                                                                                                                                                             | Por quê                                                                                            |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| MVP         | Não integrar. Montar a base própria: quem viu, garantiu e fez check-in, com consentimento. Guardar telefone e CPF de um jeito que permita cruzar depois.                                                | Não depende de ninguém e já entrega o número que a casa não tem.                                   |
| Fase 2      | A casa exporta a planilha de vendas da Zig, e nós cruzamos por CPF ou telefone para mostrar quanto gastaram os clientes do app. Assinar contrato de operador de dados com a casa.                       | Prova de retorno sem esperar a Zig. Falta confirmar se o painel da Zig exporta vendas por cliente. |
| Em paralelo | Conversa comercial com a Zig, citando o caso do Repediu. Pergunta: "existe exportação automatizada de vendas por cliente para um parceiro autorizado pela casa? Quais campos, que custo, que contrato?" | Se sair, vira integração. Se não sair, nada travou.                                                |

**O risco estratégico:** se uma casa piloto já usa Zig, ela pode ter lista, reserva e CRM da própria Zig sem pagar nada a mais. O argumento de venda não pode ser "dados para a casa". Tem que ser "trazemos gente nova e mostramos quem veio por nossa causa".

## 6. Planos com níveis (segundo plano)

Detalhe e fontes em `pesquisa/planos.md`.

**Como o mercado faz.** Quase sempre o app cobra o consumidor e a casa banca o benefício como marketing, sem receber parte da mensalidade. É o modelo de Hooch, Duo Gourmet, Prime Gourmet e Tastecard. Quem pagou a casa por uso sem teto faliu: o MoviePass queimou US$ 40 milhões num mês. O caso mais parecido com a ideia de vocês é o Nachtpas, de Amsterdã, lançado em abril de 2026. São quatro clubes, €24,50 por mês, entrada ilimitada mais um acompanhante, sujeito a lotação. As 150 vagas esgotaram; o resultado do piloto ainda não saiu.

**Em Goiânia,** desconto em drink já é mercado ocupado: o Prime Gourmet anuncia de 200 a 350 parceiros na cidade por cerca de R$ 200 por ano. **Entrada grátis em dia fraco não tem concorrente encontrado.**

**Riscos:**

- **Seleção adversa:** quem usa muito fica, quem usa pouco cancela, e o lucro da assinatura vem justamente de quem não usa.
- **Casa recusando o benefício na noite cheia:** há reclamações disso contra o Duo Gourmet no Reclame Aqui.
- **Fraude:** QR compartilhado ou printado.
- **Regra da Apple:** cobrança de assinatura digital dentro de app iOS precisa passar pela loja.

**Recomendação:**

- **No MVP:** níveis gratuitos conquistados por frequência, alimentados pelo check-in.
- **Plano pago só com quatro condições:**
  - pelo menos 3 meses de histórico de check-in;
  - umas 8 casas aceitando o benefício em dias fracos;
  - um jeito de cobrar recorrente fora do app;
  - um jeito de medir quanto o membro gasta.
- **Teste enxuto:** pré-venda de 100 vagas de "membro fundador", com até 2 entradas por mês de terça a quinta, bancadas pelas casas e cobradas por link de pagamento externo.

## 7. Freelas pela plataforma (segundo plano)

Detalhe e fontes em `pesquisa/freelas.md`. Nada aqui é parecer jurídico.

**O documento atual se apoia numa premissa errada.** Ele propõe "só MEI" na primeira versão. Mas garçom, bartender, recepção, caixa e auxiliar de cozinha **não estão** na lista oficial de ocupações permitidas ao Microempreendedor Individual (MEI), conferida no anexo da Receita Federal atualizado em outubro de 2025. Pior: a mesma norma proíbe o MEI de ceder mão de obra para serviço que se repete, "ainda que de forma intermitente". A validação do Cadastro Nacional da Pessoa Jurídica (CNPJ) que o documento prevê reprovaria quase todo freela, ou registraria em documento um enquadramento irregular.

**A trava de turnos também é perigosa.** Em junho de 2026, a Justiça holandesa requalificou a Temper (plataforma de freelas de hotelaria) como agência temporária, usando como prova de controle justamente o limite de horas por cliente imposto pela plataforma. Nos Estados Unidos, a Qwick pagou US$ 2,1 milhões e converteu os trabalhadores da Califórnia em empregados.

**Concorrentes no Brasil:** estaff, Closeer, Switch, Toopa, My Staff, Freela Certo e UmFreela. Cobram de 10 a 16% da casa e tratam o freela como autônomo. Lá fora, o modelo dominante é a plataforma como empregadora, com margem de 20 a 55%.

**Recomendação, se e quando entrar:**

- **Papel do app:** é software da casa. A casa contrata e o app só registra.
- **Freela avulso:** entra como autônomo com Recibo de Pagamento Autônomo (RPA).
- **Freela recorrente:** vai para o contrato intermitente da Consolidação das Leis do Trabalho (CLT), com a convocação gerada a partir da programação da casa.
- **Habitualidade:** o limite vira alerta para migrar o freela ao intermitente, não um bloqueio.
- **Pagamento:** Pix direto da casa ao freela.
- **Antes de escrever código:** passar por um advogado trabalhista e pela convenção coletiva de bares de Goiânia.

É um segundo negócio, com outro cliente e outro risco. Não deve disputar atenção com o MVP.

## 8. Crítica do que está escrito

Os documentos têm coisas boas e têm problemas que vêm do jeito como foram escritos: várias sessões de agente, cada uma empilhando sobre a anterior sem revisar.

**O que vale aproveitar:**

- **O motor de horário do protótipo.** Faixas de entrada, janela de promoção e noite que atravessa a madrugada são a peça mais sólida do projeto.
- **O método de estimativa do documento 04.** Fatias verticais, três pontos e data como faixa estão corretos.
- **Os critérios de aceite do documento 05.** O formato está certo e as cláusulas de concorrência e de QR de uso único são boas.
- **O alerta sobre mensagem de texto (SMS) no documento 06.** O custo de verificação por SMS é real e a saída por e-mail ou WhatsApp é boa.

**Os problemas, do mais grave ao menos grave:**

1. **Análise demais, decisão de menos.** São mais de 100 mil caracteres de planejamento, cerca de 60 perguntas, 13 "decisões bloqueantes" e nenhuma delas tomada desde agosto. Os documentos tratam a reunião de decisões como o próximo passo desde agosto. O projeto não está travado por falta de análise.
2. **O mercado nunca foi pesquisado.** Nenhum documento cita REVO, BaladAPP, os produtos de lista e reserva da Zig ou qualquer concorrente. O documento 02 chega a dizer que o CRM de Brasília "pode ser concorrente", sem perceber que a própria Zig já é.
3. **Números inventados apresentados como fato:** 200 mil seguidores, 4% de conversão, R$ 500 por mês por casa, 66 horas de painel, "3 a 6 vezes o pico". Nenhum diz de onde veio. Viram premissa de outras contas, como infra, receita e prazo, e ganham uma precisão que não têm.
4. **Documentos que se contradizem sem dizer qual vale.**
   - O documento 03 promete "MVP em 4 a 6 semanas" e um stack com React, Node, Redis e API do Instagram.
   - Os documentos 05 e 06 falam em 16 semanas e Supabase.
   - O documento 05 corta o Vibes; o 08 traz de volta.
   - O documento 07 cita uma "aba Casas" que o protótipo já removeu.
5. **Premissas de negócio não verificadas sustentando tudo.** A principal é "as seis casas do Luan". Se ele não decide pelas casas, a jornada que o documento 08 chama de "a que realmente importa" não existe.
6. **Erros de domínio que custariam caro.**
   - "Só MEI" no módulo de freelas.
   - "Consumação mínima" como condição de entrada, que é venda casada.
   - Mesa e camarote sem sinal.
   - CPF obrigatório no cadastro sem necessidade clara: o telefone resolve a identificação e o cruzamento com a Zig.
7. **Tom de consultoria.** Frases como "momento da verdade", "consequência desconfortável", "acabou" e "é isto que exige" dão convicção a opiniões não testadas. O texto parece mais decidido do que o projeto está.
8. **Nome do produto indefinido.** O app se chama "LUAN" no título e no manifest, "GoDrinking" nos documentos e "Sistema de Reservas" no documento 01. O ícone é o do Beat Proibido.

**Sobre o protótipo** (auditoria completa em `pesquisa/prototipo-auditoria.md`, capturas em `pesquisa/capturas/`). Ele é "razoável mas confuso" por motivos concretos:

- **Três públicos num app só.** O painel do operador é um interruptor escondido no menu do avatar do cliente. O módulo Freelas tem quatro entradas diferentes.
- **O mesmo conteúdo em três lugares.** A aba Hoje termina com "Amanhã" e "Nesta semana", a Agenda repete, e a página da casa repete de novo. As promoções aparecem em quatro lugares.
- **O fluxo de garantir entrada troca de nome a cada passo:** "Reservar mesa", "Nome na lista", "Mesa reservada", "Ingressos".
- **Partes que fingem funcionar.** O painel da porta mostra as reservas do próprio aparelho, de qualquer data. O selo "CNPJ validado" é fixo. A aprovação de vaga é automática em 1,5 segundo.
- **Bugs.**
  - O Passe mostra a entrada do começo da noite: quem garante às 22h30 vê "Free até 20h" quando já custa R$ 10.
  - Vagas de freela com turno já começado continuam abertas.
  - O modelo de dados não suporta festa de data única: tudo é semanal para sempre.
- **Código.** São 3.440 linhas num arquivo, cerca de 20 variáveis globais, HTML montado por concatenação de texto e Tailwind por CDN (não serve para produção). É descartável, exceto o motor de horário.

## 9. O que eu faria agora

**Reposicionamento:** "o guia de hoje da noite de Goiânia, com lista na mão". O diferencial é a programação e as promoções de hoje, juntas, com horário, em todas as casas. A lista e a porta são o que transforma a visita ao app em dado que a casa valoriza. Mesa paga, Zig, planos e freelas vêm depois, nessa ordem, cada um destravado por um resultado.

**Sequência proposta.** Os prazos são julgamento, não medidos, e assumem você trabalhando lado a lado com IA, em tempo parcial.

| Etapa              | Entrega                                                                                                                                                                                      | Pergunta que responde                                                 | Prazo                               |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- | ----------------------------------- |
| 0. Conversas       | 3 a 5 conversas com donos ou gerentes (comece pelas casas do Luan): como fazem lista e mesa hoje, se usam Zig, REVO ou BaladAPP, quanto pagariam.                                            | Existe dor que justifique trocar o WhatsApp? Quem decide e quem paga? | 1 semana, em paralelo com a etapa 1 |
| 1. Guia de hoje    | Site rápido para celular (Progressive Web App, PWA) com programação e promoções reais, publicadas por nós, compartilhado pelo Instagram das casas e do Luan. Reaproveita o motor de horário. | Pessoas abrem um guia da noite mais de uma vez por semana?            | 2 a 3 semanas                       |
| 2. Lista com QR    | Cadastro leve (telefone, código por WhatsApp ou e-mail), entrar na lista, Passe com QR, portaria web com busca por nome, numa casa piloto.                                                   | Qual o comparecimento? A porta fica mais rápida ou mais lenta?        | 3 a 4 semanas                       |
| 3. Mesa e camarote | Pacote com sinal via Pix, por um Provedor de Serviços de Pagamento (PSP) com split, para o dinheiro não passar por nós. Regras de cancelamento visíveis. Texto revisado por advogado.        | A casa vende mesa pelo app? O sinal derruba o não comparecimento?     | 3 a 4 semanas                       |
| 4. Zig             | Cruzamento por planilha exportada pela casa e contrato de operador de dados.                                                                                                                 | Clientes do app gastam mais? Isso vira argumento de venda?            | 1 a 2 semanas, depois do piloto     |
| Depois             | Painel para a casa publicar a própria programação, níveis gratuitos, teste de "membro fundador", freelas.                                                                                    | Cada um depende de um resultado das etapas anteriores.                | —                                   |

**As decisões que só você e os sócios podem tomar** estão em `decisoes.md`, cada uma com a minha recomendação. São 13. Só as 4 primeiras travam a etapa 1, e outras 3 travam a etapa 2.

**Sobre a organização do repositório,** a proposta está em `estrutura-proposta.md`. Em resumo: documentos por assunto e não por data, decisões num lugar só, pesquisa com data e fonte, o protótipo numa pasta separada, e um arquivo de estado atual atualizado ao fim de cada sessão. Assim, voltar ao projeto leva dois minutos e não uma auditoria. Nada foi movido nem apagado.

## Arquivos desta pasta

| Arquivo                           | O que é                                                                              |
| --------------------------------- | ------------------------------------------------------------------------------------ |
| `LEIA-PRIMEIRO.md`                | Este documento                                                                       |
| `decisoes.md`                     | As decisões em aberto, com recomendação                                              |
| `CONTEXT.md`                      | Glossário: um significado para cada palavra (Lista, Mesa, Camarote, Passe...)        |
| `estrutura-proposta.md`           | Nova organização do repositório e plano de migração                                  |
| `CLAUDE.proposto.md`              | Regras para agentes, a virar o `CLAUDE.md` da raiz se aprovado                       |
| `pesquisa/concorrentes.md`        | Concorrentes no Brasil e fora, padrões de interface, comparecimento, mesa e camarote |
| `pesquisa/zig.md`                 | Zig: empresa, produtos, API, LGPD, caminhos de integração                            |
| `pesquisa/planos.md`              | Assinaturas e níveis: casos, economia, riscos, teste enxuto                          |
| `pesquisa/freelas.md`             | Plataformas de freelas, legislação, recomendação                                     |
| `pesquisa/prototipo-auditoria.md` | Auditoria do `index.html` com referências de linha                                   |
| `pesquisa/capturas/`              | Capturas do protótipo em tamanho de iPhone                                           |
