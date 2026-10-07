# Pesquisa: Zig (ZigPay) e integração com a base de clientes das casas

Data da pesquisa: 2026-10-01. Legenda: **[C]** = confirmado em fonte citada; **[I]** = inferência minha a partir das fontes; **[NC]** = não confirmado.

Siglas: Customer Relationship Management (CRM), Ponto de Venda (PDV), Application Programming Interface (API), Lei Geral de Proteção de Dados (LGPD), Cadastro de Pessoa Física (CPF), Gross Merchandise Volume (GMV, volume transacionado), Enterprise Resource Planning (ERP), Comma-Separated Values (CSV), Autoridade Nacional de Proteção de Dados (ANPD), Minimum Viable Product (MVP), Data Processing Agreement (DPA, "Acordo de Processamento de Dados").

---

## TL;DR

1. Zig é a maior plataforma de cashless/PDV/ingressos para entretenimento no Brasil (R$ 265 mi captados, Kaszek lidera a última rodada) e já vende **CRM, SMS, giftback, lista de convidados, gestão de reservas, app do consumidor e marketplace de ingressos**. É **concorrente parcial** do GoDrinking, não só fornecedor.
2. **Não existe portal público de desenvolvedores** da Zig. O blog oficial diz que a Zig "possui API aberta", mas "conforme necessidade do cliente e viabilidade técnica", ou seja, acesso caso a caso via comercial. Pelo menos um CRM terceiro (Repediu) já tem integração pronta com a Zig.
3. Pela LGPD e pela própria política da Zig, **a casa (organizador/estabelecimento) é a controladora** dos dados de consumo coletados no PDV dela, e a Zig é operadora. Para o GoDrinking receber esses dados, precisa de contrato com a casa e de base legal; se a base for consentimento, a LGPD exige consentimento **específico** para compartilhar com outro controlador.
4. Recomendação para o MVP: **não integrar com a Zig**. Construir a própria base (reserva e lista de convidados capturando CPF/telefone com consentimento) e, numa fase 2, cruzar com exportações da Zig enviadas pela casa. Abrir conversa comercial com a Zig em paralelo, sem depender dela.

---

## 1. O que é a Zig hoje

### 1.1 Empresa, tamanho e investidores

| Item | Dado | Status | Fonte |
|---|---|---|---|
| Origem | Fusão em 2022 da ZigPay (fundada por Nérope Bulgarelli, CEO) com a NetPDV | [C] | https://braziljournal.com/zig-recebe-aporte-da-kazsek-para-crescer-como-a-fintech-das-baladas/ |
| Sede | Vitória (ES) segundo o perfil da Zig.Tickets e o foro da política de privacidade; uma matéria a chama de "empresa baiana" | [C] divergente | https://br.linkedin.com/company/zigtickets ; https://ajuda.zig.fun/hc/pt-br/articles/40936276193947-POL%C3%8DTICA-DE-PRIVACIDADE ; https://bpmoney.com.br/bpm-escuta/zig-apos-captar-r-110-mi-empresa-baiana-quer-expandir-no-exterior/ |
| Série B | R$ 110 mi (abr/2024), Cloud9, Across Capital, Endeavor; grande parte para "dados e CRM" | [C] | https://bpmoney.com.br/mercado/zig-capta-r-110-mi-para-antever-o-consumo-em-bares-e-festivais/ |
| Extensão | R$ 155 mi (dez/2024) liderada pela Kaszek; total captado R$ 265 mi; "Queremos ser o aplicativo da balada" | [C] | https://braziljournal.com/zig-recebe-aporte-da-kazsek-para-crescer-como-a-fintech-das-baladas/ ; https://www.bloomberglinea.com.br/startups/rodadas-da-semana-fintech-zig-capta-r-155-mi-com-solucoes-para-shows-e-eventos/ |
| Rodada anterior | R$ 40 mi (2021) de Edgard e Diogo Corona (SmartFit) e Ricardo Goldfarb | [C] | https://bpmoney.com.br/mercado/zig-capta-r-110-mi-para-antever-o-consumo-em-bares-e-festivais/ |
| GMV | R$ 2,5 bi em 2022; "mais de R$ 6 bilhões anuais" com 10 mi de cartões físicos (2024/25) | [C] | https://neofeed.com.br/startups/zig-compra-supertickets-e-entra-no-mercado-de-venda-de-ingressos/ ; https://fusoesaquisicoes.com/acontece-no-setor/zig-capta-r-110-milhoes-para-antever-o-consumo-em-bares-e-festivais/ (via resumo de busca; página retornou 403) |
| Clientes | "cerca de 6 mil clientes" (2023) vs "mais de mil estabelecimentos" (2024); 500 funcionários, 25 hubs; 5 mil eventos em 2023 | [C] números inconsistentes entre fontes | NeoFeed acima; BPMoney acima |
| Site oficial | "+271 milhões de transações", "+10.000 eventos", "4 países", "+10 anos" | [C] | https://zig.fun/ |
| Internacional | México, Portugal (Benfica), Espanha; ~10% da receita | [C] | Brazil Journal e BPMoney acima |
| Aquisição | Superticket (set/2023), virou Zig Tickets (eventos de 2 a 7 mil pessoas, take rate de 12%) | [C] | https://neofeed.com.br/startups/zig-compra-supertickets-e-entra-no-mercado-de-venda-de-ingressos/ |

### 1.2 Produtos

Fonte principal: https://zig.fun/produtos/ e https://zig.fun/

| Produto | O que é | Status |
|---|---|---|
| Zig Cashless | Cartão/pulseira NFC pré ou pós-pago, funciona offline | [C] https://zig.fun/solucoes/zig-cashless/ |
| Cashless Digital | Carteira Apple/Google Wallet | [C] https://zig.fun/produtos/cashless-digital/ |
| Zig Mesas / PDV móvel / totem / autoatendimento pelo celular / bar self-service | Operação de bar e restaurante | [C] https://zig.fun/ |
| Zig Tickets + Marketplace de Ingressos | Venda de ingressos e vitrine de eventos em zig.tickets | [C] https://zig.fun/solucoes/zig-tickets/ ; https://zig.tickets/en-US |
| Controle de acesso / check-in | Integra com outras ticketeiras ("nossa API conecta com outras ticketeiras e empresas de controle de acesso") | [C] https://zig.fun/produtos/controle-de-acesso-integrado/ |
| Analítico de clientes (CRM) | Segmentação, dados demográficos, novos x recorrentes, frequência, ticket médio | [C] https://zig.fun/produtos/perfil-de-clientes/ ; https://blog.zig.fun/conheca-o-dashboard-da-zig/ |
| Ativação por SMS | Campanhas por SMS | [C] https://zig.fun/produtos/ativacao-por-sms/ |
| Giftback | Crédito para próxima compra | [C] https://zig.fun/produtos/giftback/ |
| Integração de marketing para ingressos | Conectar campanhas digitais à venda (ferramentas não especificadas) | [C] https://zig.fun/produtos/integracao-de-marketing/ |
| Gestão de reservas | Reservas com cobrança antecipada e no-show | [C] https://zig.fun/produtos/gestao-de-reservas/ |
| Lista de convidados, cortesias, promoters | Gestão de listas e promoters | [C] https://zig.fun/produtos/lista-de-convidados/ ; https://zig.fun/produtos/gestao-de-cortesias/ |
| Antecipação de consumo | Produto de crédito/antecipação | [C] existe a página https://zig.fun/produtos/antecipacao-de-consumo/ ; detalhes [NC] |
| App do consumidor | Ingressos, saldo, pagamento por QR/Apple Pay/Google Pay, extrato, push promocional, fidelidade, reembolso; 4,8 estrelas com ~7,4 mil avaliações na App Store | [C] https://zig.fun/produtos/aplicativo/ ; https://apps.apple.com/br/app/zig-ingressos-e-consumo-f%C3%A1cil/id1154643255 |
| "Zig Ads" / mídia para marcas | Nenhuma evidência | [NC] |

Clientes citados no site: Rock in Rio, Lollapalooza, Fórmula 1, Primavera Sound, Barretos, Bar Brahma, Coala, Jaguariúna, Oktoberfest Blumenau, entre outros ([C] https://zig.fun/).

### 1.3 Presença em Goiânia/Goiás

- **Zig Tickets é usado em Goiânia** [C]: eventos como BACKSTAGE (Terraço New York), ELETROMEET (Meet Club), Pagode É Sentimento (Saccaria Verano), Festa do Rei e Di Paullo & Paulino (Espaço Dois Ipês), Roberta Miranda (Centro de Convenções PUC), Super Arraiá RTT + Salve (jun/2026). Fontes: https://zig.tickets/eventos/backstage ; https://zig.tickets/eventos/eletromeet ; https://zig.tickets/eventos/pagode-e-sentimento-2505 ; https://zig.tickets/en-US/eventos/festa-do-rei ; https://zig.tickets/en-US/eventos/roberta-miranda ; https://zig.tickets/es-ES/eventos/super-arraia-rtt-salve
- **Quais bares/baladas de Goiânia usam o cashless/PDV da Zig**: [NC]. Não achei lista pública. Ação: perguntar diretamente às casas-piloto.

---

## 2. API, documentação e acesso para parceiros

| Pergunta | Resposta | Status | Fonte |
|---|---|---|---|
| Existe portal de desenvolvedores? | Não encontrei. `api.zig.fun`, `developers.zig.fun`, `docs.zig.fun` resolvem para um curinga de DNS e retornam 404 (testado em 2026-10-01). Nada no GitHub oficial (as organizações `zigfun` e `zigtecnologia` têm 1 repositório irrelevante cada, e a autoria não é confirmada) | [C] ausência | teste via `curl`/`dig`; https://github.com/zigfun ; https://github.com/zigtecnologia |
| A Zig diz ter API? | Sim: "a Zig possui API aberta, permitindo integrações personalizadas com outras ferramentas, conforme necessidade do cliente e viabilidade técnica" (dez/2025) | [C] | https://blog.zig.fun/conheca-o-dashboard-da-zig/ |
| Integrações citadas | Plataformas de delivery, ERPs, outras ticketeiras e controle de acesso | [C] | mesma fonte; https://zig.fun/produtos/controle-de-acesso-integrado/ |
| Central de ajuda tem artigos de API/webhook/exportação? | Busca na central (Zendesk `ajuda.zig.fun`) por "API", "integração", "webhook": 0 resultados | [C] | https://ajuda.zig.fun/hc |
| Webhooks | Sem evidência pública | [NC] |
| Exportação CSV/Excel no dashboard | Não documentado publicamente | [NC]; **[I]** é muito provável que relatórios sejam exportáveis, mas validar com uma casa cliente |
| Dados expostos | O CRM mostra aniversário, consumo mínimo, saldo, histórico de visitas, gasto médio, frequência; a política lista nome, nascimento, CPF, e-mail, telefone entre os dados coletados | [C] | https://blog.zig.fun/crm-para-bares-e-restaurantes/ ; política de privacidade acima |
| Como um parceiro obtém acesso | Não há programa público de parceiros de tecnologia. O único programa público é o de "embaixadores" (indicação comercial) | [C] ausência; [I] acesso negociado caso a caso, provavelmente autorizado por casa | https://lp.zig.fun/programa-embaixadores |
| Custos de acesso | [NC] |

**Evidência prática de que a integração existe:** a Repediu (CRM de restaurantes/delivery) tem página de integração pronta com a Zig: "A venda é registrada na plataforma da Zig e os dados do cliente são enviados para a plataforma da Repediu", com segmentação e disparo por WhatsApp/SMS ([C] https://repediu.com.br/funcionalidades/integracoes/zig/). Isso prova que a Zig libera dados de cliente e venda para terceiros sob contrato. **[I]** O caminho é via parceria comercial, não autosserviço.

**Ponto de atenção sobre o CPF**: a Zig diz ao consumidor que informar o CPF numa casa parceira serve para "identificação do consumo", "segurança nas transações" e "controle e praticidade no pagamento" e "não gera automaticamente um cadastro" ([C] https://ajuda.zig.fun/hc/pt-br/articles/48335352333723). Ou seja, o CPF foi coletado para finalidade operacional, não de marketing de terceiros.

---

## 3. CRMs/ferramentas terceiras e concorrentes da Zig

### 3.1 O "grupo de Brasília com CRM acoplado à Zig"

Não consegui identificar [NC]. Candidatos encontrados, nenhum com integração Zig confirmada:
- **Unie** (Brasília, 2024): ticketeira + clube de assinatura + influenciadores + consumo pré-evento ([C] https://www.metropoles.com/colunas/claudia-meireles/jovens-brasilienses-criam-startup-para-revolucionar-o-setor-de-eventos). Integração com Zig [NC].
- **[I]** É comum grupos grandes construírem CRM interno puxando relatórios da Zig. Vale perguntar o nome ao fundador e checar se usam API (parceria) ou exportação manual.

### 3.2 Ferramentas que se plugam em PDV/cashless

| Ferramenta | O que faz | Integra com Zig? | Reservas/lista? | Preço público | Fonte |
|---|---|---|---|---|---|
| Repediu | CRM com IA para restaurantes/delivery; segmentação, recorrência, WhatsApp/SMS; ~80 integrações | **Sim** [C] | Não [I] | Planos por faixa de faturamento (até R$ 80 mil/mês e acima), valores não exibidos; créditos de disparo com recarga mínima de R$ 99,90 [C] | https://repediu.com.br/funcionalidades/integracoes/zig/ ; https://repediu.com.br/planos-e-precos/ |
| REVO | Gestão para baladas: listas VIP, promoters, portaria digital, reservas, ingressos, chatbot com IA no WhatsApp/Instagram, CRM, app com "+40 mil jovens" | [NC] | Sim [C] | 7 dias grátis; valor combinado por WhatsApp [C] | https://revoapp.com.br/produtos |
| VIPOU | Listas, QR Code, ranking de promoters | [NC] | Sim | [NC] | citado em https://revoapp.com.br/blog/lista-vip-guia-definitivo-casa-noturna-crescer |
| Tagme | Reservas, fila de espera e relacionamento para restaurantes | [NC] | Sim | [NC] | https://tagme.com.br/ |

**[I]** REVO é o concorrente mais direto do GoDrinking no lado B2B (lista + reserva + app de público).

### 3.3 Concorrentes da Zig (cashless/PDV)

| Empresa | Perfil | API aberta? | Fonte |
|---|---|---|---|
| Meep (Belo Horizonte, desde 2015) | Ticketeira + PDV + cashless; "R$ 2,1 bilhões transacionados/ano", "10 mil clientes"; escritório no DF | [NC], nada público | https://meep.com.br/ ; https://startups.com.br/alem-da-faria-lima/alem-da-faria-lima-mineira-meep-se-prepara-para-1a-captacao-e-expansao-internacional/ |
| NoxMob | PDV com cashless, lista VIP, controle de entrada e saída; "+25 mil clientes" | [NC] (cita integração com iFood) | https://nox.com.br/sistema-para-baladas/ |
| Consumer | PDV com módulo para boates (camarote, consumação, lista VIP) | Sim, "API de parceiros" para pedidos | https://consumer.com.br/sistema-para-boates-casas-noturnas ; https://ajuda.programaconsumer.com.br/integracao-api-do-parceiro/ |
| Bar Fácil | Cashless para eventos e bares | [NC] | https://www.barfacil.com.br/ |
| Sympla (ingressos, não cashless) | **API pública** com token por organizador: eventos, pedidos, participantes (nome, e-mail), check-in | Sim [C] | https://developers.sympla.com.br/api-doc/index.html ; https://ajuda.produtor.sympla.com.br/hc/pt-br/articles/15422073696653-Como-configurar-API-p%C3%BAblica |

Não pesquisei em profundidade: Ingresse, Blueticket, Fluxo, Yuppie, Dr. Pay, Pagga, Arena Pay; nada encontrado sobre API pública deles nas buscas feitas [NC].

---

## 4. A Zig é concorrente do GoDrinking?

| Função do GoDrinking | A Zig tem? | Observação |
|---|---|---|
| Descoberta (feed de lugares e eventos) | **Parcial** [C] | O Zig.App divulga "bares, restaurantes, baladas e outros estabelecimentos parceiros" (abr/2023) e zig.tickets é uma vitrine de eventos. https://blog.zig.fun/p/saiba-como-fazer-o-seu-estabelecimento-bombar-com-zig-app ; https://zig.tickets/en-US |
| Reservas | **Sim, no backoffice** [C] | Cobrança antecipada e no-show. Se há reserva pelo app do consumidor: [NC]. https://zig.fun/produtos/gestao-de-reservas/ |
| Lista de convidados | **Sim** [C] | Fluxo de inscrição do convidado: [NC]. https://zig.fun/produtos/lista-de-convidados/ |
| Fidelidade/CRM | **Sim** [C] | Giftback, SMS, analítico de clientes, push no app |
| Ambição declarada | "Queremos ser o aplicativo da balada" [C] | https://braziljournal.com/zig-recebe-aporte-da-kazsek-para-crescer-como-a-fintech-das-baladas/ |

**[I] Conclusão:** a Zig é concorrente potencial e tem caixa para entrar em descoberta com força. A vantagem dela é estar no PDV (dado de consumo real). Uma vantagem possível do GoDrinking é ser **neutro entre PDVs** (Zig, Meep, NoxMob etc.) e focado no público de Goiânia, com curadoria e programação. Também por isso a Zig pode não querer abrir dados para um app de descoberta concorrente.

---

## 5. LGPD

| Ponto | Conteúdo | Fonte |
|---|---|---|
| Papéis | Controlador = "a quem competem as decisões referentes ao tratamento"; operador = quem trata "em nome do controlador" (art. 5º, VI e VII) | https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm |
| Posição da Zig | Organizadores "na condição de controladores" dos dados coletados em seu nome; Zig "na condição de operadora", com DPA próprio; Zig é controladora em casos como "recomendação de eventos na plataforma" | [C] https://ajuda.zig.fun/hc/pt-br/articles/40936276193947-POL%C3%8DTICA-DE-PRIVACIDADE (itens 1.6.2, 1.6.3, 1.8) |
| App Zig | "O Usuário expressamente autoriza a ZIG a compartilhar com os Estabelecimentos seus dados pessoais e informações sobre a utilização do Aplicativo" (termos de 20/08/2022) | [C] https://zigpay.com.br/termos |
| Operador segue instruções | Art. 39; operador responde solidariamente se descumprir instruções (art. 42) | Lei acima |
| Compartilhar com outro controlador | Se a base for consentimento, "deverá obter consentimento específico do titular para esse fim" (art. 7º, §5º) | Lei acima |
| Legítimo interesse | Só "dados estritamente necessários" e respeitando "legítimas expectativas" do titular (art. 10) | Lei acima |
| Guia ANPD | Guia orientativo de agentes de tratamento (v2.0, 2022) | https://www.gov.br/anpd/pt-br/assuntos/noticias/nova-versao-do-guia-dos-agentes-de-tratamento |

**[I] Leitura aplicada (não é parecer jurídico):**
- A **casa** é a controladora dos dados de consumo do PDV dela; a Zig não pode, como operadora, entregar esses dados ao GoDrinking sem instrução da casa. Logo, qualquer integração exige **autorização por casa**.
- Se o GoDrinking só processar os dados **para a casa** (ex.: painel de clientes da casa), ele seria **operador**: precisa de contrato de operador com a casa e não pode reutilizar os dados para si (ex.: recomendar outros bares ao usuário).
- Se o GoDrinking quiser usar os dados **para si** (perfil unificado entre casas, recomendação), vira **controlador**. Aí precisa de base legal própria. O CPF foi informado no bar para fins operacionais, e usar isso para marketing de um app terceiro dificilmente cabe na "legítima expectativa" do art. 10. **Consentimento específico** do titular, colhido no próprio GoDrinking, é o caminho mais seguro.
- Cruzar por CPF/telefone uma base da casa com a base do GoDrinking também é tratamento. Só é seguro quando os dois lados têm base legal, e no lado GoDrinking isso significa o usuário ter consentido a vinculação.
- Consumo de álcool não é dado sensível pela lista do art. 5º, II, mas perfil de consumo + CPF é dado pessoal de alto valor. Exige minimização, segurança, encarregado (art. 41) e atendimento aos direitos do titular.

---

## 6. Caminhos de integração

| Opção | Prós | Contras | Esforço (julgamento, não medido) |
|---|---|---|---|
| (a) API oficial / parceria com a Zig | Dado em tempo real; precedente (Repediu); escala para todas as casas Zig | Sem portal público; acesso caso a caso; a Zig é concorrente potencial e pode negar ou cobrar; cada casa precisa autorizar; contrato e DPA; prazo comercial imprevisível | Alto: semanas a meses de negociação + 2 a 4 semanas de engenharia |
| (b) Casa exporta relatório do dashboard Zig e envia | Não depende da Zig; dá para validar o valor com 1 ou 2 casas | Manual e periódico; formato não documentado [NC]; precisa de contrato de operador com a casa; risco de planilha com CPF circulando por WhatsApp | Baixo a médio: importador de CSV + contrato modelo |
| (c) Casamento por CPF/telefone | Liga reserva/lista do GoDrinking ao consumo real (atribuição: "o app trouxe quem gastou X") | Exige (a) ou (b) como fonte; base legal dos dois lados; risco de reidentificação | Médio, depois de (a) ou (b) |
| (d) Não integrar no MVP | Zero dependência; foco no núcleo (descoberta + reserva + lista); o próprio GoDrinking coleta CPF/telefone com consentimento e check-in | Sem dado de consumo; a métrica de valor para a casa fica em "pessoas trazidas/check-ins", não em "R$ gastos" | Nenhum |

### Recomendação

1. **MVP: opção (d).** Capturar no GoDrinking nome, telefone e (opcionalmente) CPF na reserva e na lista, com consentimento explícito e granular para "compartilhar com a casa" e para "receber recomendações". Medir check-in na porta. Isso já cria a base própria, que é o ativo do GoDrinking.
2. **Fase 2: opção (b) + (c) com 1 ou 2 casas-piloto que usam Zig.** Contrato de operador com a casa; a casa envia exportação; o GoDrinking cruza com quem veio via app e devolve à casa um relatório de atribuição ("clientes do GoDrinking gastaram R$ X"). Prova o valor sem depender da Zig.
3. **Em paralelo: abrir conversa com a Zig** (comercial/parcerias), com a pergunta concreta: "existe API ou exportação automatizada de vendas por cliente para um parceiro autorizado pela casa? quais campos, custo e contrato?". Usar a página da Repediu como referência de que isso existe.
4. **Validar com o fundador** quem é o grupo de Brasília e como eles fazem (API x planilha). Isso economiza a descoberta.

### Perguntas em aberto [NC]
- O dashboard da Zig exporta vendas por cliente (CPF/telefone) em CSV/Excel? Quais colunas?
- A Zig cobra pelo acesso à API? Exige volume mínimo?
- Quais casas de Goiânia usam o cashless/PDV da Zig (além do Zig Tickets)?
- A reserva e a lista da Zig têm fluxo voltado ao consumidor (link público, app) ou são só backoffice?
