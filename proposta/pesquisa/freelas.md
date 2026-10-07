# Pesquisa: módulo Freelas do GoDrinking (staffing sob demanda para bares e casas noturnas)

> Pesquisa feita em 01/10/2026. Não sou advogado nem contador. Tudo que toca enquadramento trabalhista, previdenciário ou tributário precisa ser validado por um advogado trabalhista (vínculo, modelo de contrato, limites) e pela contabilidade do sócio (cálculo, guias, eSocial). Onde uma afirmação não foi confirmada em fonte, está marcado **não confirmado**. Fontes secundárias (blogs, reviews) estão sinalizadas como tal.

## Resumo executivo

1. **"Só MEI" não funciona como base do v1.** Garçom, barman/bartender, recepcionista/hostess, operador de caixa e auxiliar de cozinha **não constam** do Anexo XI da Resolução do Comitê Gestor do Simples Nacional (CGSN) 140/2018, a lista oficial de ocupações permitidas ao Microempreendedor Individual (MEI), conferida na versão oficial da Receita Federal de 16/10/2025, já com a alteração da Resolução CGSN 182/2025. O MEI só pode exercer as ocupações dessa lista, e a mesma norma proíbe o MEI de fazer cessão de mão de obra para serviços que se repetem periodicamente, "ainda que [...] de forma intermitente". Além disso, a lei diz que, havendo elementos de emprego, o rótulo MEI não protege a casa.
2. **O mercado brasileiro já tem vários players** (estaff, Closeer, Switch, Toopa, My Staff, Freela Certo, UmFreela, StaffUp, StaffPRO, TIO). A maioria se apresenta como intermediadora de autônomos; Closeer e TIO trabalham com o contrato intermitente da Consolidação das Leis do Trabalho (CLT). Cobrança típica: 10% a 16% (+ taxa fixa) por serviço, cobrada da casa.
3. **Lá fora, o modelo que sobreviveu ao escrutínio é o de "empregador de registro"** (a plataforma ou uma afiliada é a empregadora: Indeed Flex, Coople, Jobandtalent, Instawork W-2, Wonolo via Grow2). Os modelos de autônomo (1099 nos EUA, ZZP na Holanda) apanharam: a Qwick pagou US$ 2,1 milhões e converteu os trabalhadores da Califórnia em empregados, e em 16/06/2026 a Corte de Apelação de Amsterdã requalificou a Temper como agência de trabalho temporário. O markup típico fica entre 20% e 55%.
4. **No Brasil, a tese da pejotização (Tema 1389 do STF) e a da uberização (Tema 1291) seguem sem decisão de mérito** em 01/10/2026. A Convenção 193 da Organização Internacional do Trabalho (OIT), de 12/06/2026, manda classificar o trabalhador de plataforma pelos fatos, não pelo contrato.
5. **Recomendação para o v1:** o app como software da casa (a casa contrata; o app registra), com duas trilhas: **autônomo eventual com Recibo de Pagamento Autônomo (RPA)** para a noite avulsa e **intermitente (CLT art. 452-A)** para quem volta com frequência. MEI aceito só quando a ocupação do Cadastro Nacional da Pessoa Jurídica (CNPJ) do freela casar com a função, o que será raro. A trilha "plataforma/parceiro como empresa de trabalho temporário (Lei 6.019/74)" é a que mais reduz o risco para a casa, mas exige uma empresa registrada no Ministério do Trabalho com R$ 100 mil de capital: é fase 2, via parceria. Pagamento: Pix direto da casa ao freela, com o app só registrando.
6. **Maior risco:** reconhecimento de vínculo empregatício entre a casa e o freela recorrente. Os dados do próprio app (escala, check-in, avaliação, punições) viram prova, e a plataforma pode ser arrastada se exercer controle. Nenhuma lei dá um número seguro de turnos: houve vínculo reconhecido com 2 dias por semana.

---

## 1. Plataformas brasileiras de staffing para hospitalidade e eventos

### 1.1 O que existe (verificado)

| Plataforma | O que faz | Modelo de receita | Modalidade de contratação | Tração declarada | Fontes |
|---|---|---|---|---|---|
| **estaff** (SP, atuação nacional) | Freelas para bares, restaurantes, buffets, hotéis e eventos. Também faz recrutamento fixo e monta equipes de evento. Check-in e check-out com validação, avaliação de gestores, frequência e pontualidade | Taxa por contratação concluída "conforme o plano", mais planos mensais com seleção assistida (fonte secundária). Percentual **não confirmado** | **Não confirmado** (o site não diz) | "1,5 milhão de profissionais cadastrados", "+1.515 bares, restaurantes, hotéis e eventos", "998 mil jobs" | [estaff para empresas](https://estaff.com.br/para-empresas), [estaff home](https://estaff.com.br/), [Google Play](https://play.google.com/store/apps/details?id=com.estaff.appfreela&gl=br) |
| **Closeer** (fundada em fev/2019) | Gestão e pagamento de mão de obra operacional (food service, hotelaria, varejo). Check-in e check-out por QR code, carteira digital, avaliação de 1 a 5 estrelas | Só a empresa paga: percentual de taxa de serviço por job (2021). Em 2018 falava em 10% do trabalhador após 6 meses grátis e mensalidade da casa | Em 2018: contrato **intermitente** gerado eletronicamente pelo app. Hoje o site não especifica (**não confirmado**) | Hoje: "+1,1 milhão de jobs", "+670 mil profissionais", "+6.000 unidades de negócio", "+R$ 150 milhões" pagos. Investimento-anjo de R$ 725 mil | [closeer.com.br](https://www.closeer.com.br/), [Projeto Draft 2021](https://www.projetodraft.com/a-closeer-conecta-freelancers-da-area-operacional-a-empresas-dos-setores-de-food-service-hotelaria-e-varejo/), [Abrasel 2018](https://abrasel.com.br/noticias/noticias/aplicativos-conectam-bares-e-restaurantes-a-trabalhadores-intermitentes/), [Gazeta do Povo](https://www.gazetadopovo.com.br/economia/aplicativos-conectam-bares-e-restaurantes-a-trabalhadores-intermitentes-f2oaed3lryqk6bb9tqunka2fi/) |
| **Switch** (ES; Grande Vitória, SP, BH, RJ) | Freelas por hora para bares, restaurantes, hotéis e supermercados. Treinamento obrigatório do profissional | Sem mensalidade. A casa recebe nota fiscal de intermediação mais nota de débito do repasse. Percentual **não confirmado** | **Autônomo**. Os termos dizem que a relação "não possui nenhuma das características [...] de vínculo", com serviço "eventual, não exclusivo, sem subordinação". Não exige MEI | "+30.000 profissionais", "+1.200 empresas", "+50 mil serviços", "+R$ 4 mi" pagos aos profissionais | [switchapp.com.br](https://switchapp.com.br/), [termos dos profissionais](https://switchapp.com.br/termos-profissionais/), [blog Switch](https://switchapp.com.br/blog/contratar-garcom/) |
| **Toopa** (RJ/SP, fundada em jun/2020) | Recepcionistas, garçons, cumins, barmen, caixas e limpeza para bares, restaurantes, hotéis e eventos | Sem mensalidade: "o contratante repassa cerca de 10% do valor total do serviço". O app retém o pagamento da casa e garante o repasse ao trabalhador em até 3 dias úteis | **Não confirmado** | Ago/2021: 500 estabelecimentos e 2.000 candidatos. Situação atual **não confirmada** | [Forbes Brasil 2021](https://forbes.com.br/forbes-tech/2021/08/exclusiva-aplicativo-conecta-bares-e-restaurantes-a-funcionarios-freelancers-para-apoiar-a-retomada-do-setor/) |
| **My Staff** | Garçons, bartenders, limpeza e atendentes para restaurantes, bares e eventos, por geolocalização | "Taxa de 16% mais R$ 2 em cima do valor contratado" (2018). A Abrasel de 2019 fala em 16% | Autônomo | 2018: 2 mil cadastros, metade em SP. Situação atual **não confirmada** | [Abrasel 2018](https://abrasel.com.br/noticias/noticias/aplicativos-conectam-bares-e-restaurantes-a-trabalhadores-intermitentes/), [Abrasel 2019](https://abrasel.com.br/noticias/noticias/aplicativos-para-bares-e-restaurantes-facilitam-contratacoes-confira/), [Projeto Draft](https://www.projetodraft.com/o-my-staff-conecta-prestadores-de-servico-a-bares-restaurantes-e-eventos/) |
| **TIO – Trabalho Intermitente Online** | Software de gestão do **intermitente**: convocação com fila de substituição, ponto com reconhecimento facial e geolocalização, recibos | Assinatura em planos (**valores não confirmados**) | **Intermitente CLT**. A casa é a empregadora | **Não confirmado** | [tio.digital](https://tio.digital/), [Abrasel 2019](https://abrasel.com.br/noticias/noticias/aplicativos-para-bares-e-restaurantes-facilitam-contratacoes-confira/) |
| **Freela Certo** | Freelas de gastronomia e eventos | **Não confirmado** | Não especifica. O pagamento é direto da casa ao freela, "imediatamente ao término do trabalho" | **Não confirmado** | [FAQ Freela Certo](https://freelacerto.com.br/faq/) |
| **UmFreela** | Freelas de gastronomia, hotelaria e eventos | Freela não paga. "A primeira vaga é sempre grátis" para a empresa (as seguintes são pagas, valor **não confirmado**) | Não especifica | Pequena (5,0 no Google com 14 avaliações) | [umfreela.com.br](https://umfreela.com.br/) |
| **Freela Serviços** | Cozinheiros, garçons, bartenders e recepcionistas para eventos, bares e restaurantes | Diz não cobrar taxa adicional do cliente (como monetiza: **não confirmado**) | Não especifica | **Não confirmado** | [freelaservicos.com.br](https://www.freelaservicos.com.br/) |
| **StaffUp** (RS/SC) | Staffing de freelas para eventos, bares e restaurantes | **Não confirmado** | **Não confirmado** | **Não confirmado** | [staffup.com.br](https://staffup.com.br/site-staffup) |
| **StaffPRO** | Freelas para eventos: escala, check-in, pagamentos | **Não confirmado** | **Não confirmado** | **Não confirmado** | [staffpro.com.br](https://staffpro.com.br/) |
| **Staff BR**, **Easy Freela**, **e-Bico**, **Central Freela SP** | Apps menores de diária ou freela | **Não confirmado** | **Não confirmado** | **Não confirmado** | [Staff BR](https://play.google.com/store/apps/details?id=br.com.futebolcard.staffbr.app&hl=en), [Easy Freela](https://easyfreela.com/), [e-Bico](https://ebicoapp.com/), [Central Freela SP](https://www.centralfreelasp.com/) |

**Nomes da lista pedida que não encontrei como plataforma de staffing de hospitalidade (não confirmados):** "Jobbol", "Temporário Já", "FreelaJá", "Popjobs", "Dia de Bico", "Staffy", "Chef Freela", "Eventos Staff", "Contrata Garçom", "Shiftmarket". "Bico" só apareceu como termo genérico e como o app de serviços domésticos "Bicos Online" ([Catraca Livre](https://catracalivre.com.br/carreira/bicos-on-line-conheca-a-primeira-plataforma-focada-em-servicos-domesticos/)). Trampos, Gupy, Sólides, Workana e Avec atuam em vagas fixas, recrutamento, RH ou gestão de salão, não em turno sob demanda (julgamento meu, não verificado um a um nesta pesquisa).

### 1.2 Padrões observados no Brasil

- **Quem paga é a casa.** O freela usa de graça em todos os casos documentados ([Closeer](https://www.projetodraft.com/a-closeer-conecta-freelancers-da-area-operacional-a-empresas-dos-setores-de-food-service-hotelaria-e-varejo/), [UmFreela](https://umfreela.com.br/), [Toopa](https://forbes.com.br/forbes-tech/2021/08/exclusiva-aplicativo-conecta-bares-e-restaurantes-a-funcionarios-freelancers-para-apoiar-a-retomada-do-setor/)).
- **A taxa documentada fica em 10% a 16%** do valor do serviço ([Toopa ~10%](https://forbes.com.br/forbes-tech/2021/08/exclusiva-aplicativo-conecta-bares-e-restaurantes-a-funcionarios-freelancers-para-apoiar-a-retomada-do-setor/), [My Staff 16% + R$ 2](https://abrasel.com.br/noticias/noticias/aplicativos-conectam-bares-e-restaurantes-a-trabalhadores-intermitentes/)). É bem abaixo dos 20% a 55% dos modelos estrangeiros em que a plataforma é a empregadora (seção 2).
- **Dois fluxos de dinheiro:** (a) a plataforma recebe da casa e repassa (Switch paga semanalmente às quintas e pode reter valores; Toopa repassa em até 3 dias úteis), ou (b) a casa paga direto (Freela Certo) ([termos Switch](https://switchapp.com.br/termos-profissionais/), [Freela Certo](https://freelacerto.com.br/faq/)).
- **No-show e cancelamento** são tratados com nota e reputação: o Freela Certo marca "1 cancelamento" (aviso de 6 h ou mais) ou "1 não comparecimento" (menos de 6 h) e prioriza bem avaliados. A Switch prevê desconto de até 10% das horas por descumprimento ([Freela Certo](https://freelacerto.com.br/faq/), [Switch cl. 10.9](https://switchapp.com.br/termos-profissionais/)). Atenção: punição disciplinar aplicada pela plataforma é indício de subordinação (ver 3.6).
- **Preço de referência:** um garçom freela ganha em média R$ 100 a R$ 250 por diária (fonte secundária, [EPOC](https://epoc.com.br/blog/garcom-freelancer/)). Reviews citam R$ 9 a R$ 13 por hora na Switch (fonte secundária, via busca, **não confirmado**).
- **Ninguém que pesquisei exige MEI.** Os termos da Switch tratam o profissional como autônomo pessoa física ([termos Switch](https://switchapp.com.br/termos-profissionais/)).

**Leitura para o GoDrinking:** o mercado já existe e tem escala (estaff, Closeer, Switch). O diferencial do GoDrinking não é o marketplace de freelas em si. É estar dentro da operação da noite (programação, portaria por QR code, a casa já cadastrada) em Goiânia, onde nenhum desses players mostrou presença local (**não confirmado**: não verifiquei cobertura por cidade).

---

## 2. Referências internacionais

| Plataforma | Modelo de receita | Classificação do trabalhador | Confiabilidade e UX | Fontes |
|---|---|---|---|---|
| **Instawork** (EUA) | Valor-hora "tudo incluso" com markup que "varia por tipo de turno, volume, cargo e local". Análises externas falam em 20% a 40%, com um caso citado de 35%. Taxa de conversão para contratação fixa de US$ 2,5 mil, que cai para US$ 1 mil se o profissional já fez 320 h com a casa | Híbrido: 1099 (contratado da própria Instawork) ou W-2 como empregado da **Advantage Workforce Services**, afiliada que atua como empregadora | Cancelamento grátis com 24 h. No-show: 1 em 30 dias dá 7 dias de suspensão, 2 em 30 dias dão 30 dias, depois desativação. Score de confiabilidade em janela móvel de 3 meses | [preços](https://help.instawork.com/en/articles/5854747-instawork-business-pricing), [classificação](https://help.instawork.com/en/articles/12691234-worker-classification-basics), [Contrary Research](https://research.contrary.com/company/instawork), [cancelamento/suspensão](https://help.instawork.com/en/articles/6122001-cancellation-policy-suspensions), [score](https://help.instawork.com/en/articles/6449818-understand-your-performance-score) |
| **Qwick** (EUA, hospitalidade) | ~40% sobre o valor-hora, pago pela empresa (fonte secundária). Instant pay em ~30 min com taxa de 3% | Era 1099. **Acordo de US$ 2,1 milhões com San Francisco (set/2024)**: os ~10 mil trabalhadores da Califórnia viraram W-2 | Diz ter 98% de comparecimento (fonte secundária) | [Bloomberg Law](https://news.bloomberglaw.com/litigation/qwick-will-pay-2-1-million-to-settle-misclassification-suit), [BMCC Law](https://bmcclaw.com/2024/09/san-franciscos-2-1-million-settlement-with-qwick-puts-spotlight-on-worker-misclassification/), [SideHustles (secundária)](https://sidehustles.com/qwick-app-review/) |
| **Indeed Flex** (ex-Syft, Reino Unido, comprada pela Indeed em 2019) | Markup percentual sobre o pagamento do "Flexer", incluindo encargos e taxa da plataforma | **W-2, empregador de registro**: a Indeed Flex cuida de folha e compliance; a casa é o local de trabalho | — | [licença do cliente](https://indeedflex.com/legal/flex-client-user-license/), [Recruit Holdings](https://recruit-holdings.com/en/blog/post_20221017_0001/) |
| **Wonolo** (EUA) | Markup padrão de **45% (1099) e 55% (W-2)** sobre a remuneração. Cobra do trabalhador US$ 0,65 a US$ 0,70/h de "Trust and Safety Fee" | Maioria 1099. W-2 via parceira **Grow2** (empregadora de registro) | — | [Customer Agreement](https://info.wonolo.com/customer-agreement), [comparativo (secundária)](https://indeedflex.com/career-hub/guides/indeed-flex-vs-wonolo) |
| **Shiftsmart** (EUA) | Markup **não confirmado** | 1099 | Instant pay por US$ 3 (cai em ~30 min após aprovação). Revisão do turno em 24 a 72 h. Diz atingir mais de 95% de preenchimento (secundária) | [ajuda Shiftsmart](https://help.shiftsmart.com/hc/en-us/articles/28868841034772-When-you-ll-get-paid), [Indeed FAQ](https://www.indeed.com/cmp/Shiftsmart/faq/is-shiftsmart-1099-or-w-2?quid=1ee36j0gbp1hq800) |
| **Coople** (Suíça e Reino Unido) | Sem setup e sem assinatura. Preço por hora com encargos | **A Coople é a empregadora legal** (staff leasing e payrolling), sob a convenção coletiva "Staff Leasing" da swissstaffing | 1 milhão de trabalhadores registrados (UK + CH) | [temp staffing](https://www.coople.com/ch/en/business/temp-staffing), [payrolling](https://www.coople.com/ch/en/business/payrolling), [preços](https://www.coople.com/ch/en/business/pricing), [Retail Times](https://retailtimes.co.uk/digital-staffing-platform-coople-hits-milestone-of-1-million-registered-workers-across-uk-and-switzerland/) |
| **Jobandtalent** (Espanha) | Agência de trabalho temporário digital ("workforce as a service") | **Empresa de Trabalho Temporário (ETT) licenciada**: os trabalhadores são empregados dela | Comprou duas agências na Colômbia. Captou US$ 108 mi (2021) e US$ 115 mi da Kinnevik | [TechCrunch](https://techcrunch.com/2021/01/08/jobandtalent-tops-up-with-108m-for-its-workforce-as-a-service-platform/), [Kinnevik](https://www.globenewswire.com/en/news-release/2021/12/01/2343768/0/en/Kinnevik-Invests-USD-115-Million-in-Jobandtalent-the-World-s-Leading-Digital-Temp-Staffing-Agency.html), [SIA](https://www.staffingindustry.com/news/global-daily-news/spain-jobandtalent-acquires-two-colombian-temporary-staffing-firms) |
| **Brigad** (França; o análogo mais próximo do "só MEI") | Comissão de 25% (fontes antigas); o CEO falou em "~20% de custos operacionais" em 2023. Série B de € 33 mi (Balderton) | Freelas **auto-entrepreneur** (o equivalente francês do MEI) ou sociedades. A plataforma se diz mera intermediária | 12 mil estabelecimentos, 23 mil profissionais, 300 mil missões. **O risco de requalificação pela URSSAF fica com o restaurante, não com a Brigad** | [Hello My Business](https://www.hellomybusiness.fr/comment-devenir-micro-entrepreneur-en-ligne/avis-brigad/), [RH Matin](https://www.rhmatin.com/recrutement-talents/site-emploi-specialise/plateforme-de-mises-en-relation-pour-le-travail-brigad-decroche-33-millions-d-euros.html), [Brigad](https://www.brigad.co/), [Extencia](https://www.extencia.fr/urssaf-extras-independants-restauration) |
| **Temper** (Holanda) | Plataforma de autônomos (ZZP) para hospitalidade | **Em 16/06/2026 a Corte de Apelação de Amsterdã decidiu que os trabalhadores são temporários de agência (uitzendovereenkomst)**: a Temper não é "plataforma neutra", fornecia contratos-modelo e **limitava as horas por cliente**, o trabalho integrava a rotina do cliente e não havia risco empresarial real. Consequências: convenção coletiva das agências (ABU-CLA), lei Waadi e passivo de imposto sobre salário de 2016 a 2019 | — | [Mondaq](https://www.mondaq.com/employee-rights-labour-relations/1807606/amsterdam-court-of-appeal-temper-workers-qualify-as-temporary-agency-workers), [Remote Work Europe](https://remoteworkeurope.eu/news/2026/netherlands-temper-platform-uitzendbureau-court-appeal/), [Recht.nl](https://www.recht.nl/nieuws/arbeidsrecht/6a315d06c947df262795/hof-ziet-deelnemers-aan-platform-temper-niet-als-als-zzpers-maar-als-uitzendkrachten/) |
| **Catapult** (Reino Unido) | **Não confirmado** | Promete "sem contrato zero-hora", pagamento semanal e férias acumuladas por turno, o que sugere vínculo de agência (**não confirmado**) | Candidatura a vários turnos de uma vez, timesheet, avaliação do empregador, "instant claim" | [joincatapult.com](https://www.joincatapult.com/looking-for-work) |
| **StaffMate** | **Não pesquisado** (não confirmado) | — | — | — |

### 2.1 O que tirar dos estrangeiros

- **Markup:** de 20% a 40% (Instawork), passando por ~40% (Qwick), até 45% ou 55% (Wonolo, 1099 ou W-2). O W-2 custa uns 10 pontos a mais porque embute os encargos ([Wonolo](https://info.wonolo.com/customer-agreement), [Contrary](https://research.contrary.com/company/instawork)). No Brasil, os 10% a 16% observados correspondem a modelos em que a plataforma **não** é empregadora.
- **Classificação:** a tendência de 2024 a 2026 é migrar para "empregador de registro" ou agência temporária, por acordo (Qwick) ou por decisão judicial (Temper). A Brigad sobrevive como intermediária pura justamente porque **o risco fica com o restaurante** ([Extencia](https://www.extencia.fr/urssaf-extras-independants-restauration)). Isso equivale ao desenho "só MEI": tira o risco da plataforma e o põe no cliente, que é a casa.
- **A ironia da trava:** no caso Temper, a **limitação de horas por cliente imposta pela plataforma foi citada como prova de controle** ([Mondaq](https://www.mondaq.com/employee-rights-labour-relations/1807606/amsterdam-court-of-appeal-temper-workers-qualify-as-temporary-agency-workers)). A trava de habitualidade proposta no rascunho precisa ser desenhada com advogado: um alerta para a casa ("considere intermitente") é diferente de uma regra disciplinar da plataforma.
- **Padrões de UX que valem copiar:**
  - Preço "tudo incluso" mostrado à casa antes de publicar ([Instawork](https://help.instawork.com/en/articles/5854747-instawork-business-pricing)).
  - Cancelamento grátis até 24 h ([Instawork](https://help.instawork.com/en/articles/5854747-instawork-business-pricing)).
  - Score de confiabilidade em janela móvel com peso maior para no-show do que para cancelamento tardio ([Instawork](https://help.instawork.com/en/articles/6449818-understand-your-performance-score)).
  - Instant pay como upsell pago pelo trabalhador: 3% na Qwick, US$ 3 na Shiftsmart ([SideHustles](https://sidehustles.com/qwick-app-review/), [Shiftsmart](https://help.shiftsmart.com/hc/en-us/articles/28868841034772-When-you-ll-get-paid)).
  - "Try before you hire", com taxa de conversão decrescente pelas horas já trabalhadas ([Qwick jobs](https://www.qwick.com/jobs/), [Contrary](https://research.contrary.com/company/instawork)).
  - Check-in e check-out geolocalizado ou por QR code ([Closeer](https://www.projetodraft.com/a-closeer-conecta-freelancers-da-area-operacional-a-empresas-dos-setores-de-food-service-hotelaria-e-varejo/), [estaff](https://estaff.com.br/)).
  - Avaliação mútua ([Switch](https://switchapp.com.br/termos-profissionais/)).
  - Fila de substituição automática ([TIO](https://tio.digital/)).
  - "Backup worker" ou standby pago: não encontrei documentação oficial (**não confirmado**).

---

## 3. Panorama legal brasileiro (resumo, sem substituir advogado)

### 3.1 MEI: as funções pedidas são ocupações permitidas?

**Não.** Conferi o PDF oficial do Anexo XI da Resolução CGSN 140/2018 na Receita Federal ([anexo_xi.pdf](https://www8.receita.fazenda.gov.br/simplesnacional/arquivos/manual/anexo_xi.pdf); metadados do arquivo: gerado em 16/10/2025). Ele já inclui a ocupação "MOTORISTA (POR APLICATIVO OU NÃO) INDEPENDENTE", trazida pela Resolução CGSN 182/2025, publicada no Diário Oficial da União (DOU) em 01/10/2025 ([LegisWeb](https://www.legisweb.com.br/legislacao/?id=484221)). Busquei no texto integral:

| Função do GoDrinking | Ocupação no Anexo XI? | Ocupações "vizinhas" que existem (não equivalem à função) |
|---|---|---|
| Garçom | **Não** | — |
| Bartender / barman | **Não** | "Comerciante de bebidas" e "Proprietário de bar e congêneres" (dono do próprio bar, não quem trabalha no bar alheio) |
| Recepção / hostess | **Não** | "Promotor(a) de eventos independente" (CNAE 8230-0/01, organização de feiras e eventos) |
| Caixa | **Não** | — |
| Cozinha (auxiliar, cozinheiro) | **Não** como prestação no estabelecimento alheio | "Cozinheiro(a) que fornece refeições prontas e embaladas", "Salgadeiro(a)", "Churrasqueiro(a) em domicílio", "Pizzaiolo(a) em domicílio" |
| DJ (fora do escopo, só referência) | Sim: "Disc jockey (DJ) ou video jockey (VJ) independente" | — |

O art. 100 da Resolução CGSN 140/2018 define o MEI como quem "exerça, de forma independente e exclusiva, **apenas** as ocupações constantes do Anexo XI" ([texto compilado da Res. CGSN 140](https://guiatributario.net/wp-content/uploads/2025/10/resolucao-140-cgsn.pdf)). Fontes contábeis secundárias confirmam: "não existe a ocupação garçom" no Portal do Empreendedor ([Contábeis, fórum](https://www.contabeis.com.br/forum/legalizacao-de-empresas/412716/mei-garcom-qual-atividade-mais-adequada-ou-correspondente/)).

Há notícia de uma Resolução CGSN 183/2025 que também alteraria a lista; o conteúdo **não foi confirmado** ([busca: Mais MEI](https://www.maismei.com.br/blog/o-que-mudou-nas-atividades-que-podem-ser-mei-em-2026)). Mudanças em 2026 também **não foram confirmadas**: antes de qualquer decisão, a contabilidade deve reconferir a lista vigente no [Portal do Empreendedor](https://www.gov.br/empresas-e-negocios/pt-br/empreendedor/quero-ser-mei/o-que-e-ser-um-mei/verifique-se-voce-atende-as-condicoes-para-ser-mei-1).

**Mais duas travas do MEI:**
- **Proibição de cessão de mão de obra.** O art. 112 da Res. CGSN 140/2018 diz: "O MEI não poderá realizar cessão ou locação de mão de obra, sob pena de exclusão do Simples Nacional". O §3º define serviços contínuos como "os que constituem necessidade permanente da contratante, que se repetem periódica ou sistematicamente [...] **ainda que sua execução seja realizada de forma intermitente**". O garçom que a casa chama toda sexta parece se encaixar aí (minha leitura; **validar com o contador**) ([Res. CGSN 140, art. 112](https://guiatributario.net/wp-content/uploads/2025/10/resolucao-140-cgsn.pdf)).
- **O rótulo MEI não protege a casa.** A Lei Complementar 123/2006, art. 18-B, §2º, diz que o regime "não se aplica quando presentes os elementos da relação de emprego, ficando a contratante sujeita a todas as obrigações dela decorrentes, inclusive trabalhistas, tributárias e previdenciárias" ([LC 123/2006, Planalto](https://www.planalto.gov.br/ccivil_03/leis/lcp/lcp123.htm)).
- **Limite de faturamento:** continua R$ 81 mil por ano. O Projeto de Lei Complementar (PLP) 108/2021, que sobe para R$ 130 mil, teve urgência aprovada em 17/03/2026, mas não foi sancionado até a fonte consultada ([Agência Sebrae](https://agenciasebrae.com.br/economia-e-politica/camara-aprova-urgencia-para-projeto-que-amplia-teto-de-faturamento-anual-dos-mei-para-r-130-mil/), [Jettax](https://www.jettax.com.br/blog/aumento-do-limite-do-mei-em-2026-valor-atual-projeto-de-lei-e-o-que-pode-mudar/)).

**Consequência para o produto:** se o v1 validar o CNPJ do MEI por API, como prevê o rascunho, a API vai mostrar a ocupação cadastrada. Garçom com MEI de "promotor de eventos" será a regra, e o app estaria registrando, com prova documental, um enquadramento indevido.

### 3.2 Requisitos do vínculo (CLT arts. 2º e 3º)

- Art. 2º: empregador é quem, "assumindo os riscos da atividade econômica, admite, assalaria e **dirige** a prestação pessoal de serviço".
- Art. 3º: empregado é "toda pessoa física que prestar serviços de natureza **não eventual** a empregador, sob a **dependência** deste e mediante salário".
- Os requisitos clássicos são pessoa física, pessoalidade, não eventualidade, subordinação e onerosidade ([CLT, Planalto](https://www.planalto.gov.br/ccivil_03/decreto-lei/del5452.htm)).
- Art. 442-B (reforma de 2017): a contratação do autônomo "cumpridas por este todas as formalidades legais, com ou sem exclusividade, de forma contínua ou não, afasta a qualidade de empregado" ([CLT](https://www.planalto.gov.br/ccivil_03/decreto-lei/del5452.htm)). Na prática, os tribunais aplicam a primazia da realidade (abaixo).

**Jurisprudência que interessa a uma casa de Goiânia:**
- **Sem vínculo:** em 09/10/2024, o Tribunal Regional do Trabalho da 18ª Região (TRT-18, Goiás) negou vínculo de um garçom com um bar de Goiânia. Ele escolhia os dias por WhatsApp sem punição, podia se afastar por longos períodos e trabalhava para concorrentes (processo 0011505-44.2023.5.18.0005) ([TRT-18](https://www.trt18.jus.br/portal/garcom-nao-consegue-provar-vinculo-empregaticio-com-bar-de-goiania/)). **Esse é o perfil que o produto deve preservar: liberdade real de aceitar ou recusar, sem punição.**
- **Com vínculo:** em mar/2026, o TRT-4 reconheceu vínculo de uma atendente de açaiteria com turnos fixos às quintas e sextas por cerca de 4 meses. Citou o Tribunal Superior do Trabalho (TST): o vínculo pode existir "mesmo em jornadas reduzidas ou intermitentes" ([Contadores.cnt](https://www.contadores.cnt.br/noticias/tecnicas/2026/03/03/jornada-de-dois-dias-por-semana-gera-vinculo-empregaticio-entende-trt-4.html)). O TRT-4 também reconheceu vínculo de garçom pago por diárias (2023), com o ônus da prova da autonomia passando à casa depois de admitida a prestação de serviço ([TRT-4](https://www.trt4.jus.br/portais/trt4/modulos/noticias/558333)). Há também barman de casa noturna em fins de semana e eventos mensais com vínculo reconhecido ([JusBrasil](https://www.jusbrasil.com.br/noticias/barman-que-trabalhava-em-casa-noturna-nos-finais-de-semana-e-em-eventos-mensais-tem-reconhecido-vinculo-de-emprego/430633050)) e TST com vínculo para trabalho 2 vezes por semana por mais de 2 anos ([JusBrasil](https://www.jusbrasil.com.br/noticias/trabalhar-duas-vezes-por-semana-com-habitualidade-garante-vinculo-segundo-tst/449247967)).
- **Conclusão (julgamento, não parecer):** não existe número de turnos seguro em lei. O que decide é subordinação mais habitualidade. Um teto do tipo "no máximo N turnos por mês na mesma casa" ajuda, mas um teto como 8 por mês (todas as sextas e sábados) já seria habitualidade. **O limite precisa vir de advogado trabalhista.**

### 3.3 Trabalho intermitente (CLT art. 443, §3º, e art. 452-A)

- **Definição:** "a prestação de serviços, com subordinação, não é contínua, ocorrendo com alternância de períodos de prestação de serviços e de inatividade, determinados em horas, dias ou meses, independentemente do tipo de atividade" (art. 443, §3º) ([CLT](https://www.planalto.gov.br/ccivil_03/decreto-lei/del5452.htm)).
- **Regras do art. 452-A** ([CLT](https://www.planalto.gov.br/ccivil_03/decreto-lei/del5452.htm)):
  - Contrato escrito, com valor-hora não inferior ao do salário mínimo ou ao dos demais empregados da mesma função.
  - Convocação "com, pelo menos, **três dias corridos** de antecedência".
  - Resposta em 1 dia útil; o silêncio é recusa. "A recusa da oferta não descaracteriza a subordinação".
  - Quem aceita e falta sem justo motivo paga multa de 50% da remuneração devida.
  - A cada período, o trabalhador recebe remuneração, férias proporcionais + 1/3, 13º proporcional, descanso semanal remunerado (DSR) e adicionais. A casa recolhe Fundo de Garantia do Tempo de Serviço (FGTS) e contribuição ao Instituto Nacional do Seguro Social (INSS) (§§6º a 8º; conferir no texto).
- **Constitucionalidade:** o Supremo Tribunal Federal (STF) validou o intermitente por 7 a 4, em 13/12/2024, nas Ações Diretas de Inconstitucionalidade (ADIs) 5826, 5829 e 6154 ([Conexão Trabalho/CNI](https://conexaotrabalho.portaldaindustria.com.br/noticias/detalhe/trabalhista/-geral/stf-declara-constitucional-o-contrato-de-trabalho-intermitente/), [acórdão via TRT-3](https://portal.trt3.jus.br/internet/jurisprudencia/repercussao-geral-e-controle-concentrado-adi-adc-e-adpf-stf/downloads/adi-5826-acordao-publicado-improcedente.pdf)).
- **Atrito com o produto:** os 3 dias de antecedência não servem para "preciso de um bartender hoje à noite". Servem para a escala da semana, que é o caso da casa noturna com programação definida (o motor de datas do GoDrinking já sabe as noites).
- **Custo:** se a casa estiver no Simples Nacional, a contribuição patronal previdenciária (CPP) costuma estar dentro do Documento de Arrecadação do Simples Nacional (DAS) para as atividades de comércio e serviços dos Anexos I a III. Bar e restaurante normalmente ficam no Anexo I. Isso torna o intermitente e o RPA mais baratos do que parecem. **Não confirmado nesta pesquisa: validar com a contabilidade.**
- Já há quem defenda o "intermitente plataformizado" como enquadramento para trabalho por app ([ConJur, 18/12/2025](https://conjur.com.br/2025-dez-18/servico-por-aplicativo-e-novo-tipo-de-atividade-intermitente-diz-advogada/)).

### 3.4 Trabalho temporário via agência (Lei 6.019/74, alterada pela Lei 13.429/2017)

Base: [Lei 6.019/74, Planalto](https://www.planalto.gov.br/ccivil_03/leis/l6019.htm).

- **Definição:** trabalho "prestado por pessoa física contratada por uma empresa de trabalho temporário que a coloca à disposição de uma empresa tomadora de serviços, para atender à necessidade de substituição transitória de pessoal permanente ou à **demanda complementar de serviços**" (art. 2º). Demanda complementar é a "oriunda de fatores imprevisíveis ou, quando decorrente de fatores previsíveis, tenha natureza **intermitente, periódica ou sazonal**" (art. 2º, §2º). Noite de casa cheia, evento e reforço de fim de semana parecem caber; **validar com advogado**.
- **Empresa de Trabalho Temporário (ETT):** pessoa jurídica "devidamente registrada no Ministério do Trabalho" (art. 4º). Requisitos (art. 6º): CNPJ, registro na Junta Comercial e **capital social mínimo de R$ 100.000,00**.
- **Contrato** escrito entre ETT e tomadora, com o motivo justificador (art. 9º). Duração de até **180 dias**, consecutivos ou não, prorrogáveis por mais 90 (art. 10, §§1º e 2º). Recontratação para a mesma tomadora só depois de 90 dias; antes disso, "caracteriza vínculo empregatício com a tomadora" (art. 10, §§5º e 6º). A tomadora é **subsidiariamente responsável** pelas obrigações trabalhistas do período (art. 10, §7º).
- **Direitos do temporário** (art. 12): remuneração equivalente à dos empregados da mesma categoria da tomadora, adicional noturno, DSR, férias proporcionais etc.
- **Por que importa:** é o equivalente brasileiro do modelo Indeed Flex, Coople, Jobandtalent ou Instawork W-2. Quem emprega é a agência; a casa só toma o serviço e o risco de vínculo com a casa cai muito (fica a responsabilidade subsidiária). O preço é a agência cobrar markup e assumir folha. **O GoDrinking não deveria virar ETT no v1** (capital, registro, folha); o caminho é parceria com uma ETT de Goiânia, e a existência de candidatas locais **não foi verificada**.
- **Risco de fazer "agência sem ser agência":** se o app escala, precifica, pune e substitui trabalhadores para a casa sem ser ETT, pode ser visto como intermediação de mão de obra fora da Lei 6.019, com risco de corresponsabilidade. É o que aconteceu com a Temper na Holanda ([Mondaq](https://www.mondaq.com/employee-rights-labour-relations/1807606/amsterdam-court-of-appeal-temper-workers-qualify-as-temporary-agency-workers)). No Brasil, é minha leitura (**não confirmado** com jurisprudência específica; levar ao advogado).

### 3.5 Autônomo com RPA (contribuinte individual)

- A casa retém 11% de INSS do autônomo até o teto (em 2026, teto de R$ 8.475,55, logo no máximo R$ 932,31 por mês) e paga 20% de contribuição patronal, salvo regime em que a CPP vai no DAS. Retém Imposto de Renda Retido na Fonte (IRRF) pela tabela progressiva. O Imposto Sobre Serviços (ISS) depende do município. A casa informa o pagamento no eSocial ([Barbieri Advogados](https://www.barbieriadvogados.com/contribuicao-inss-autonomo/), [Trivium](https://triviumcontabil.com.br/recibo-de-pagamento-autonomo-rpa/), [Foco Tributário](https://focotributario.com.br/retencao-do-inss-na-contratacao-de-contribuinte-individual/)).
- **Vantagem sobre o MEI:** qualquer função cabe, porque não depende da lista de ocupações. O risco de vínculo é o mesmo se houver habitualidade e subordinação.
- **A ISS de Goiânia para esse serviço:** **não confirmado**.

### 3.6 Pejotização e plataformas: STF e Congresso em 2025-2026

- **Tema 1389 (pejotização, ARE 1532603, relator Gilmar Mendes).** Discute (i) a competência da Justiça do Trabalho para julgar fraude em contrato civil, (ii) a licitude de contratar autônomo ou pessoa jurídica e (iii) o ônus da prova.
  - A repercussão geral foi reconhecida em abr/2025, e em 14/04/2025 houve suspensão nacional dos processos ([Agência Brasil](https://agenciabrasil.ebc.com.br/justica/noticia/2025-04/stf-suspende-todas-acoes-do-pais-sobre-pejotizacao-de-trabalhadores), [STF – andamento](https://portal.stf.jus.br/jurisprudenciaRepercussao/verAndamentoProcesso.asp?incidente=7138684&numeroProcesso=1532603&classeProcesso=ARE&numeroTema=1389)).
  - O mérito começou no Plenário Virtual em nov/2025 e está parado por pedido de vista da ministra Cármen Lúcia desde dez/2025 ([Managefy, ago/2026](https://managefy.com.br/blog/pejotizacao-stf-tema-1389/)).
  - Em 17 ou 18/06/2026, o relator liberou a tramitação na 1ª e na 2ª instância, mas os processos não sobem ao TST nem ao STF até a tese ([TST](https://www.tst.jus.br/-/stf-retira-suspensao-de-processos-sobre-pejotizacao-na-primeira-instancia-e-nos-trts), [Felsberg](https://www.felsberg.com.br/tema-1389-pejotizacao-retomada-processos-stf/)).
  - **Sem decisão de mérito até a última fonte consultada (set/2026)** ([Contábeis](https://www.contabeis.com.br/noticias/79446/stf-tem-julgamentos-pendentes-sobre-pejotizacao-e-previdencia/)). O conteúdo do voto do relator **não foi confirmado** em fonte primária.
  - **Impacto:** uma tese pró-contratação civil reduziria o risco do modelo autônomo ou MEI; uma tese restritiva aumentaria. Não dá para construir o produto contando com o resultado.
- **Tema 1291 (uberização, RE 1446336, Uber).** Foi retirado de pauta em 24/06/2026 pelo presidente do STF, Edson Fachin, a pedido da Defensoria Pública da União (DPU) e do Ministério Público do Trabalho (MPT), para analisar a **Convenção 193 da OIT**, aprovada em 12/06/2026 na 114ª Conferência Internacional do Trabalho ([ConJur](https://www.conjur.com.br/2026-jun-24/stf-adia-julgamento-da-uberizacao-para-analisar-nova-convencao-da-oit/), [STF Notícias](https://noticias.stf.jus.br/postsnoticias/a-pedido-da-dpu-e-do-mpt-stf-retira-de-pauta-julgamento-sobre-relacoes-de-trabalho-em-plataformas-digitais/)). Voltou à pauta em 27/08/2026 e não foi julgado; não há nova data (fontes secundárias: [Garrastazu](https://www.garrastazu.adv.br/motoristas-de-app-tem-vinculo-empregaticio-o-que-o-stf-vai-decidir-em-junho-de-2026), [Advogado de Bolso](https://advdebolso.com/direito-trabalhista/motorista-de-aplicativo-vinculo-emprego-stf/)).
- **Convenção 193 da OIT:** o art. 9º manda classificar o trabalhador de plataforma "com base, principalmente, nos fatos relativos à execução do trabalho e à remuneração", não na forma contratual. Não cria presunção de emprego e cobre também o autônomo ([ConJur, 18/08/2026](https://conjur.com.br/2026-ago-18/convencao-193-da-oit-e-a-primazia-da-realidade-no-julgamento-do-trabalho-em-plataformas-digitais-no-stf/), [CSB](https://csb.org.br/noticias/convencao-193-oit-trabalho-decente-economia-plataformas)). A ratificação pelo Brasil **não foi confirmada**.
- **Projetos de lei:** o PLP 12/2024 (motoristas como "trabalhador autônomo por plataforma") não virou lei ([texto, Planalto](https://www.planalto.gov.br/CCIVIL_03/Projetos/Ato_2023_2026/2024/PLP/plp-012.htm)). O PLP 152/2025 (transporte e entrega por plataforma) recebeu parecer pela aprovação na forma de substitutivo em 07/04/2026, mas a votação na comissão especial foi cancelada e ficou sem data até jul/2026 ([Câmara, ficha](https://www.camara.leg.br/proposicoesWeb/fichadetramitacao?idProposicao=2537739), [Vida de Motorista (secundária)](https://vidademotorista.com.br/plp-152-2025-regulamentacao-uber-99/)). **Nenhum dos dois cobre staffing de hospitalidade.**

### 3.7 Segurança privada: fora do módulo

A Lei 14.967/2024 (Estatuto da Segurança Privada) revogou a Lei 7.102/1983. Os serviços "serão prestados por pessoas jurídicas especializadas", e o parágrafo único do art. 2º diz: "**É vedada a prestação de serviços de segurança privada de forma cooperada ou autônoma**". A autorização e a fiscalização são da Polícia Federal ([Lei 14.967/2024, Câmara](https://www2.camara.leg.br/legin/fed/lei/2024/lei-14967-9-setembro-2024-796214-publicacaooriginal-172963-pl.html), [SindRio](https://www.sindrio.com.br/2024/11/nova-lei-de-seguranca-para-eventos-o-que-muda-para-a-organizacao-de-festas-e-shows-no-brasil/)). O rascunho está certo em excluir a função. Vale bloquear também títulos de vaga como "segurança", "controlador de acesso" ou "porteiro" que escondam a função; a fronteira entre "controlador de acesso" e "vigilante" **precisa de advogado**.

### 3.8 O que precisa de advogado trabalhista (lista objetiva)

1. Desenho da trava de habitualidade: quantos turnos, em que janela e se é bloqueio ou alerta. Levar o caso Temper como contraexemplo.
2. Se a plataforma pode aplicar punições (suspensão por no-show, desconto) sem caracterizar subordinação a ela.
3. Se "demanda complementar" (Lei 6.019, art. 2º, §2º) cobre as noites de fim de semana de uma casa noturna e se há contrato temporário de um dia na prática.
4. Modelos de contrato: autônomo eventual, intermitente e tomadora-ETT.
5. A fronteira da função "controlador de acesso" ou "recepção" frente à Lei 14.967/2024.
6. Convenção coletiva de bares, restaurantes e hotelaria de Goiânia: piso, adicional noturno e cláusulas sobre "extra" ou diarista. **Não pesquisado nesta rodada** (o limite de buscas acabou); é item obrigatório.

---

## 4. Pagamento: split por Provedor de Serviços de Pagamento (PSP) e instant pay

### 4.1 Por que não deixar o dinheiro passar pela conta do GoDrinking

Se o app recebe da casa e repassa ao freela, ele se aproxima da figura do subcredenciador ou facilitador, sujeita a regras do Banco Central (participação na liquidação centralizada etc.). O caminho usual é contratar um intermediador já homologado e usar o split dele ([iugu, regras do Bacen para marketplaces](https://www.iugu.com/blog/novas-regras-bacen-marketplaces), [Migalhas](https://www.migalhas.com.br/depeso/277839/banco-central-disciplina-a-figura-do-subcredenciador)). A Resolução BCB 80/2021 foi atualizada pela 494/2025 para reforçar a autorização prévia de instituição de pagamento ([Merc Group](https://www.mercgroup.com.br/insights/compliance-bcb-instituicoes-pagamento)). Em que ponto um app como o GoDrinking passaria a precisar de autorização **não foi confirmado: consultar advogado regulatório se o v2 for por esse caminho.**

### 4.2 Opções de PSP

| PSP | Como faz o split | Pix | Observações | Fontes |
|---|---|---|---|---|
| **Asaas** | Subcontas criadas por API, cada uma com `walletId`. Split fixo ou percentual sobre o **valor líquido**, executado após o recebimento. Webhook `PAYMENT_SPLIT_DONE`. O estorno também estorna os repasses | Sim | Cada freela precisaria de subconta Asaas (KYC). Pix anunciado a R$ 0,99 ou R$ 1,99 por transação (secundária, a confirmar) | [docs split](https://docs.asaas.com/docs/split-de-pagamentos), [subcontas](https://docs.asaas.com/docs/criacao-de-subcontas), [blog Asaas](https://blog.asaas.com/split-de-pagamento/) |
| **Pagar.me (Stone)** | "Recebedores" por transação, em percentual ou valor. Os recebedores **não precisam de conta Pagar.me**: a liquidação vai direto para a conta bancária deles | Sim, com chave aleatória | Bom encaixe para freela pessoa física | [overview marketplace](https://docs.pagar.me/docs/overview-marketplace), [recebedores](https://docs.pagar.me/docs/recebedores-2), [Pix](https://docs.pagar.me/docs/pix-1) |
| **iugu** | "Conta mestre e subcontas", com split fixo ou percentual definido também "se pago com Pix" | Sim | — | [dev iugu split](https://dev.iugu.com/docs/split-de-pagamentos) |
| **Stripe Connect (BR)** | Contas conectadas Custom ou Express a partir de plataforma brasileira | Pix para contas brasileiras é **só por convite**, exige 60 dias de processamento | Menos indicado para Pix-first no v1 | [Stripe Pix](https://support.stripe.com/questions/how-to-enable-pix-as-a-payment-method-in-brazil), [Connect Custom](https://docs.stripe.com/connect/custom-accounts) |

### 4.3 Instant pay

- **Pix direto da casa ao freela já é "instant pay"** do ponto de vista do trabalhador, sem custo de float para o GoDrinking. O Freela Certo segue esse modelo: pagamento "imediatamente ao término do trabalho" ([Freela Certo](https://freelacerto.com.br/faq/)).
- O instant pay dos estrangeiros (Qwick 3%, Shiftsmart US$ 3) é **pago pelo trabalhador** e existe porque a plataforma é quem paga ([SideHustles](https://sidehustles.com/qwick-app-review/), [Shiftsmart](https://help.shiftsmart.com/hc/en-us/articles/28868841034772-When-you-ll-get-paid)). Antecipar ao freela antes de a casa pagar é crédito, com risco financeiro e possivelmente regulatório (julgamento meu).
- **v1:** o app gera o valor bruto e o líquido do turno fechado e um QR Pix "copia e cola" com a chave do freela. A casa paga e marca "pago" (ou o freela confirma). **v2:** cobrança da casa via PSP com split automático (freela + taxa GoDrinking), com o dinheiro sem passar por conta nossa.

---

## 5. Recomendação

### 5.1 Modalidade para o v1 enxuto

**Trocar "só MEI" por "a casa contrata, o app registra", em duas trilhas:**

| Trilha | Quando | Modalidade | Quem faz o quê |
|---|---|---|---|
| **Avulso** | Primeira vez ou reforço pontual numa casa | **Autônomo eventual com RPA**. MEI aceito só se a ocupação do CNPJ casar com a função (raro para garçom, bartender, caixa e recepção) | O app gera o RPA (valor bruto, retenções, líquido) e exporta para a contabilidade do sócio, que cuida de guias, eSocial e da Escrituração Fiscal Digital de Retenções e Outras Informações Fiscais (EFD-Reinf) |
| **Recorrente** | O freela passa a aparecer com frequência na mesma casa (gatilho definido pelo advogado) | **Intermitente (CLT 452-A)**, com a casa como empregadora | O app emite a convocação com 3 ou mais dias de antecedência a partir da programação da casa, registra o aceite, o check-in e o check-out e exporta para a folha da contabilidade |

Por que esse desenho:
- Cobre todas as funções da noite, inclusive cozinha, sem depender da lista do MEI.
- Usa exatamente o que a contabilidade do sócio sabe fazer (RPA e folha).
- Transforma a "trava de habitualidade" de proibição em **migração para um regime legal** (alerta: "este freela já fez N turnos; converter em intermitente?"). Isso conversa melhor com o caso Temper do que um bloqueio imposto pela plataforma.
- Mantém o GoDrinking como fornecedor de software da casa, e não como intermediador de mão de obra: sem precificar o trabalho, sem punir o freela, sem escolher quem vai.

**Fase 2 (se a tração justificar):** parceria com uma ETT registrada (Lei 6.019) para vender "staff garantido" com markup, que é o modelo Indeed Flex ou Coople. É o que mais tira risco da casa e permite cobrar o markup de 20% a 40% visto lá fora. Não faz sentido o GoDrinking virar ETT (capital de R$ 100 mil, registro no Ministério do Trabalho e folha própria).

**O que mudar no `base/07-modulo-freelas.md`:**
- A seção 4 trata MEI como "baixa complexidade". A lista oficial não tem as funções, e há a vedação de cessão de mão de obra do art. 112.
- A estimativa da seção 7 tem uma tarefa de "validação do CNPJ do MEI por API" que vai reprovar quase todo mundo.
- A seção 5.2 já pedia "verificar se cada função é ocupação permitida ao MEI": a resposta é **não**, para as cinco funções.

### 5.2 Maior risco

**Vínculo empregatício reconhecido entre a casa e o freela recorrente, com o histórico do app como prova.** Isso independe do rótulo (MEI, RPA ou "freela"), por força da LC 123, art. 18-B, §2º, e da primazia da realidade (CLT arts. 2º e 3º; Convenção 193 da OIT, art. 9º). Os precedentes mostram que 2 dias por semana bastam (TRT-4, 2026) e que a liberdade real de recusar é o que salva (TRT-18, 2024).

Riscos secundários:
- A plataforma ser vista como empregadora ou intermediadora de fato se punir, precificar ou escalar (caso Temper).
- Tributário e previdenciário: MEI fora da ocupação permitida, cessão de mão de obra por MEI, falta de retenção no RPA.
- O resultado do Tema 1389 do STF, que pode mexer no risco para cima ou para baixo, ainda sem data.

### 5.3 Próximos passos sugeridos

1. Levar ao advogado trabalhista a lista da seção 3.8, com a CCT de Goiânia.
2. Pedir à contabilidade a confirmação do custo real de RPA e intermitente para uma casa no Simples Anexo I, com uma simulação de 1 noite de garçom.
3. Entrevistar 3 a 5 casas: como pagam hoje, quantos freelas recorrentes têm, se algum é MEI e com qual ocupação.
4. Checar se estaff, Closeer ou Switch atendem Goiânia hoje (**não confirmado**).
5. Reescrever a seção 4 e a seção 7 do `07-modulo-freelas.md` com as duas trilhas.
