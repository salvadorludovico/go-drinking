# Escopo do MVP — GoDrinking

> Status: **proposta**. Cada item marcado `[DECISÃO #n]` depende da reunião da
> Etapa 1 (ver `04-processo-notas-para-prazo.md`). As estimativas assumem a
> escolha indicada como padrão; se a decisão for outra, a estimativa muda e está
> indicado quanto.

## 1. Princípio de corte

O MVP existe para responder **uma** pergunta: *a casa vende mais e opera melhor
quando a reserva/lista passa pelo app em vez do direct?* Tudo que não ajuda a
responder isso sai, por mais que seja bonito na apresentação.

Consequência direta e desconfortável: **Vibes (feed de vídeos) e Fidelidade não
são MVP.** Vibes é o melhor ativo de demo que você tem — mantenha no protótipo
para vender a visão aos sócios — mas ele não move o show-rate do piloto e é o
maior custo de infra (ver `06`). Fidelidade só faz sentido depois que existir
histórico de check-in; sem check-in, não há ponto para dar.

## 2. Contradição a resolver antes de tudo

A reunião decidiu **pagamento fora do escopo inicial** e, na mesma ata, definiu
**plano Ouro a R$15/mês**. Um exclui o outro. Recomendação: manter pagamento
fora, lançar fidelidade em versão gratuita (Prata/Ouro/Platina conquistados por
frequência, não comprados), e trazer cobrança só quando houver adquirente
definida. Isso preserva a decisão de risco e não mata a narrativa de fidelidade.

---

## 3. Personas e o que cada uma pode fazer

| Papel | No MVP |
|---|---|
| **Visitante** (sem conta) | Ver casas, programação, promoções, vídeos. Não reserva, não entra na lista. |
| **Cliente** (conta com nome, CPF, e-mail, nascimento) | Reservar, entrar em lista, gerar QR de entrada, ver histórico. |
| **Operador da casa** | Ver reservas do dia, validar QR na porta, marcar presença. |
| **Admin (nós)** | Cadastrar casas, publicar programação e promoções pelas casas. |

O papel "Gerente edita a própria programação" **fica fora do MVP** `[DECISÃO #3]`.
Com 1 casa piloto, é mais rápido e mais confiável nós publicarmos. Isso corta
~66h de painel e remove o maior risco não-técnico do projeto (casa que não
alimenta o sistema).

---

## 4. Features do MVP com critério de aceite

### F1 — Conta e identidade
- Cadastro com nome, CPF, e-mail, data de nascimento; login por telefone + OTP `[DECISÃO #6]`.
- Modo visitante disponível sem cadastro; ao tocar em "Reservar" ou "Entrar na lista", o app pede a conta antes de prosseguir e **retorna ao ponto exato** onde parou.
- **Aceite:** *Dado um visitante navegando na sexta do Môi, quando toca em Reservar, então completa cadastro e cai de volta no formulário de reserva daquela noite, sem perder o contexto.*
- **Aceite:** *CPF é validado (dígito verificador) e é único — o mesmo CPF não cria duas contas.*
- **LGPD:** CPF e data de nascimento exigem base legal e aviso de privacidade no cadastro. Não é opcional; é uma tela e um texto, mas precisa existir no dia 1.

### F2 — Descoberta: casas, programação e promoções
- Lista de casas com foto, setor, gênero musical e o que acontece **hoje**.
- Página da casa com a semana inteira: horário, nome da noite, DJs, promoções com validade ("2 taças R$30 até 22h"), status de entrada (free até X, depois R$Y).
- Navegação por swipe entre seções, como no protótipo atual.
- **Aceite:** *Dado que o Môi cadastrou "Girls&Wine, quinta 19h-2h, entrada free", quando o usuário abre o app numa quinta às 20h, então a noite aparece como "acontecendo agora" com a promoção ativa em destaque e a que já expirou apagada.*

### F3 — Reserva
- Escolher noite, número de pessoas, confirmar.
- Confirmação **automática** até a capacidade da noite `[DECISÃO #1 e #2]`; acima disso, lista de espera.
- Cancelamento pelo usuário até X horas antes (sugestão: 2h).
- Tela "Minhas reservas" com próximas e passadas.
- **Aceite:** *Dado que a sexta tem 120 lugares e 120 confirmados, quando o 121º reserva, então ele entra em lista de espera e não ocupa vaga.*
- **Aceite:** *Duas pessoas reservando a última vaga ao mesmo tempo: uma confirma, a outra vai para a espera. Nunca 121 confirmados.* (é isto que exige controle de concorrência no banco — não é detalhe)
- **Se a decisão #1 for "gerente aprova":** +24h e exige o painel do F5 no MVP.

### F4 — Lista / entrada free com QR
- Entrar na lista de uma noite gera um QR único.
- Na porta, o operador escaneia e o app mostra nome, foto do documento não, apenas nome + status + acompanhantes.
- QR só valida uma vez; segunda leitura mostra "já utilizado às 23h14".
- **Aceite:** *Dado um QR válido para a sexta, quando o operador escaneia às 22h, então marca presença e o mesmo QR falha na segunda leitura.*
- **Aceite:** *Com internet instável na portaria, a validação funciona com a lista carregada localmente e sincroniza depois.* — este requisito sozinho responde por boa parte da estimativa; se a casa aceitar exigir internet estável na porta, corta ~12h `[DECISÃO #5]`.

### F5 — Operação da casa (versão mínima)
- Tela web (não app) com a lista do dia: quem reservou, quantas pessoas, quem chegou.
- Busca por nome na porta, como alternativa ao QR.
- Exportar a lista da noite.
- **Aceite:** *Às 23h de sexta, o operador vê em uma tela quantas pessoas confirmaram, quantas chegaram e encontra qualquer nome em menos de 5 segundos.*

### F6 — Comunicação
- E-mail de confirmação da reserva (barato, funciona em todo lugar).
- Lembrete no dia do evento.
- Push só se o usuário instalou o PWA `[DECISÃO #11]`. **No iOS, push em PWA exige que o usuário adicione o app à tela de início** — assuma que boa parte não fará isso e não prometa remarketing por push aos sócios.
- WhatsApp fica para a Fase 2: a API oficial exige aprovação de templates e verificação de negócio, o que leva semanas e não depende de nós.

### F7 — Fundações não-negociáveis
Não aparecem na demo, mas sem elas não há piloto: deploy automatizado, backup do
banco com restauração testada, monitoramento de erro, aviso de privacidade/LGPD,
e um painel simples de métricas do piloto (cadastros, reservas, check-ins,
show-rate).

---

## 5. Explicitamente fora do MVP

| Item | Por quê | Quando |
|---|---|---|
| Pagamento no app (cartão/Pix) | Decisão da reunião: risco e complexidade operacional | Fase 3, com adquirente definida |
| Integração Zig | Inviável hoje, sem contrato nem API definida `[DECISÃO #12]` | Reavaliar após piloto |
| Fidelidade paga (Ouro R$15) | Depende de pagamento | Fase 3 |
| Vibes em produção (upload, CDN, moderação) | Maior custo de infra, não move a métrica do piloto | Fase 2 |
| Painel self-service para gerentes | Nós publicamos no piloto | Fase 2, ao passar de 2 casas |
| Integração Sympla / Vernissage | Terceiro, variância alta `[DECISÃO #9]` | Fase 2 — no MVP, link externo |
| App nativo iOS/Android | PWA cobre o piloto | Após validação |
| Analytics para as casas | Sem volume não há insight | Fase 2 |

---

## 6. Estimativa (PERT, em horas de 1 dev)

| # | Fatia vertical | O | M | P | PERT |
|---|---|---|---|---|---|
| 1 | Conta, CPF, OTP, LGPD (F1) | 16 | 28 | 48 | **29** |
| 2 | Casas, programação, promoções (F2) | 20 | 32 | 50 | **33** |
| 3 | Promoções com validade por horário | 8 | 14 | 24 | **15** |
| 4 | Reserva ponta a ponta + concorrência (F3) | 30 | 48 | 80 | **50** |
| 5 | Lista + QR + validação na porta (F4) | 24 | 40 | 70 | **42** |
| 6 | Operação da casa, versão mínima (F5) | 14 | 22 | 36 | **23** |
| 7 | E-mail, lembrete, push PWA (F6) | 20 | 32 | 60 | **35** |
| 8 | Infra, deploy, backup, observabilidade, LGPD (F7) | 24 | 36 | 60 | **38** |
| | **Soma MVP-Piloto** | | | | **265h** |
| 9 | *(fora)* Painel self-service do gerente | 40 | 64 | 100 | 66 |
| 10 | *(fora)* Fidelidade v1 sem cobrança | 16 | 28 | 50 | 30 |
| 11 | *(fora)* Vibes em produção | 20 | 34 | 60 | 36 |

### Conversão em calendário (1 dev, 25h úteis/semana, +30% integração)

```
MVP-Piloto:  265h x 1.3 = 345h / 25 = 14 semanas + 2 de estabilizacao = 16 semanas
```

Com hoje = **19/08/2026**:

| Escopo | Faixa | Data |
|---|---|---|
| **Corte enxuto** (sem F4/QR, sem push — só reserva + e-mail) | 10-13 sem. | **28/out a 18/nov/2026** |
| **MVP-Piloto** (tabela acima, recomendado) | 15-18 sem. | **02/dez a 23/dez/2026** |
| **MVP + painel + fidelidade + Vibes** | 23-27 sem. | **fev a mar/2027** |

Recomendação para os sócios: **comprometer com o MVP-Piloto em dezembro/2026**,
apresentado como faixa, com recompromisso público em **30/09/2026** — quando as
fatias 1 a 3 estiverem prontas e a produtividade real já for medida em vez de
estimada.

### Como acelerar (as únicas alavancas reais)

1. **Um segundo dev** não corta pela metade — corta ~35% e só se as fatias forem independentes (1 e 2 são; 4 e 5 não).
2. **Cortar F4 (QR/lista)** economiza 42h e 2 semanas de calendário. É o corte mais barato se a casa piloto aceitar lista por nome.
3. **Backend gerenciado** (Supabase/Firebase para auth + banco + storage) corta boa parte da fatia 8 e parte da 1 — custa flexibilidade futura. Ver `06`.
4. **Não cortar F7.** Cortar fundação não acelera, só transfere o custo para dezembro, com juros.
