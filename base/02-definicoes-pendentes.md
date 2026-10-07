# Definições Pendentes & Perguntas Críticas

## 🎯 Questões para a Conversa com Luan

### 📊 SOBRE O NEGÓCIO

#### MVP & Prioridade
- [ ] **Qual é a casa prioritária para começar?** (Môi, Point, Mosaic, Vernissage, Fluxo, Cajuína?)
  - Por que essa casa? (volume, disponibilidade, comprometimento?)
  - As outras virão depois?

- [ ] **Qual é o problema mais urgente que o app precisa resolver?**
  - Pessoas não sabem que eventos/promoções existem?
  - Dificuldade em fazer/gerenciar reservas (fila, desistência)?
  - Falta de controle sobre lotação/ocupação?
  - Perda de clientes por falta de comunicação?

- [ ] **Timeline realista?** Quanto vocês conseguem investir em desenvolvimento?
  - 4-6 semanas é factível ou precisa ser mais rápido?
  - Qual é o deadline ideal?

#### Modelo de Receita
- [ ] **Como vocês pretendem ganhar com isso?**
  - Comissão por reserva confirmada? (quantos %?)
  - Taxa mensal por casa? (quanto?)
  - Porcentagem do ingresso vendido?
  - Premium features para gerentes?
  - Publicidade/anúncios no app?
  - Ou simplesmente aumentar ocupação nas casas?

- [ ] **As casas pagariam por usar?** Ou seria valor zero enquanto testa?

#### Audiência & Escala
- [ ] **Quantas pessoas acompanham essas casas hoje?**
  - Total de seguidores no Instagram (soma de todas)?
  - Conversão esperada para o app?
  - Qual é a meta de usuários no primeiro mês/trimestre?

---

### 🔄 SOBRE RESERVAS (Core Feature)

#### Fluxo Atual
- [ ] **Como funciona a reserva hoje?** 
  - Telefonema? WhatsApp? Instagram DM?
  - Quanto tempo leva pra confirmar?
  - Qual é a taxa de desistência?

#### Requisitos Técnicos
- [ ] **Como funciona a confirmação de reserva?**
  - A casa confirma automaticamente (até lotação máxima)?
  - Ou precisa de aprovação manual do gerente?
  - Confirmação imediata ou recebe mensagem depois?

- [ ] **Quanto tempo antes do evento as pessoas reservam?**
  - No dia? 1-2 dias antes? 1 semana?
  - Afeta o design da notificação?

- [ ] **Limite de lugares por noite?**
  - Varia por dia (sexta é lotado, quarta tem espaço)?
  - Como determinar capacidade?
  - Precisa avisar quando está lotado?

- [ ] **Cancelamento de reserva**
  - Usuário pode cancelar até quando?
  - Casa pode desabilitar reservas em eventos específicos?

- [ ] **Identificação do usuário**
  - Email + Senha? Social login (Google/Instagram)?
  - Precisa de foto/ID para validar presença?
  - Telefone é obrigatório?

#### Integração com Pagamento
- [ ] **Haverá cobrança de entrada no app?**
  - Sim: quanto, como pagar (débito, crédito, Pix)?
  - Não: por enquanto é só confirmação?

- [ ] **Se houver pagamento, quem recebe?**
  - App fica com taxa? Quanto?
  - Casa recebe via transferência? Pix?

---

### 📢 SOBRE NOTIFICAÇÕES

#### Estratégia
- [ ] **Quando notificar?**
  - Quando novo evento é publicado?
  - Virada de lote (ingresso fica mais caro)?
  - Último horário (ainda tem lugar pra hoje)?
  - Lembretes (você tem reserva amanhã)?

- [ ] **Como não incomodar?**
  - Usuário escolhe quais casas quer notificações?
  - Pode ligar/desligar por tipo de notificação?
  - Frequência máxima de notificações por dia?

- [ ] **Qual é o poder esperado das notificações?**
  - Aumentar ocupação em dias vazios?
  - Converter "interessado" em "confirmado"?
  - Trazer pessoas que desistiram?

---

### 🎨 SOBRE CONTEÚDO & MÍDIAS

#### Instagram
- [ ] **Integração com Instagram é crítica no MVP?**
  - Posts do Instagram aparecem no app?
  - Só o evento ou a promoção também?
  - Link direto pra comprar ingresso no Sympla (alguns eventos)?

#### IA para Criar Posts
- [ ] **Vocês querem IA gerando texto dos eventos?**
  - Template/modelo que IA preenchere com detalhes?
  - Ou copiar manualmente do Instagram pro app?
  - Prioridade alta ou baixa pra MVP?

#### Mídias (Fotos/Vídeos)
- [ ] **Como a casa forneceria fotos/vídeos do evento?**
  - Upload manual no app?
  - Puxar do Instagram automaticamente?
  - Câmera ao vivo/stories?

---

### 👥 SOBRE PAPÉIS & GERENTES

#### Quem Usa o App?
- [ ] **Papéis no sistema:**
  - Usuário comum (reserva, vê programação, recebe notificações)
  - Gerente de casa (controla programação, vê reservas)
  - Admin da plataforma (suporte, relatórios)
  - Outros? (Marketing da casa? DJ?)

- [ ] **Como o gerente atualiza programação?**
  - Painel web simples?
  - App mobile também?
  - Form com todos os detalhes ou editor visual?

- [ ] **Quem cria as promoções?**
  - Gerente da casa? Marketing?
  - App auxilia com templates/sugestões?

---

### 🎮 SOBRE GAMIFICAÇÃO

#### Se Quiser Implementar
- [ ] **Qual é a gamificação ideal?**
  - Passport/passaporte (visita todas as casas)?
  - Pontos por reserva/check-in? Resgata em quê?
  - Badges/troféus por desafios?
  - Ranking (top visitantes)?

- [ ] **Quando implementar?**
  - MVP já tem? Ou é Fase 2?

- [ ] **Objetivo da gamificação:**
  - Pura diversão ou aumentar frequência?
  - Pode oferecer desconto no app (ex: 10 visitas = 50 off)?

---

### 📈 SOBRE ANALYTICS & DADOS

#### Para os Gerentes
- [ ] **Quais dados importam pro gerente?**
  - Quantas pessoas viram o evento?
  - Quantas fizeram reserva?
  - Quantas realmente foram? (via check-in)
  - Taxa de conversão (visualização → reserva → presença)?

- [ ] **Reports/Dashboard:**
  - Semanal? Mensal?
  - Visual ou exportar em Excel/PDF?

#### Para a Plataforma
- [ ] **Monitoramento (Audit Log):**
  - Crítico desde o start?
  - Rastrear edições de programação?
  - Rastrear cancelamentos de reserva?

---

### 🚀 SOBRE ROADMAP

#### Sequência de Lançamento
- [ ] **MVP mínimo (Semana 1):**
  - Apenas browse + programação + promoções (sem reserva ainda)?
  - Ou já com reserva no dia 1?

- [ ] **Quando expandir para mais casas?**
  - Depois que MVP tiver estável (2 semanas)?
  - Depois que atingir N usuários?
  - Assim que cada casa pedir?

- [ ] **Prioridade das features:**
  - Se tivesse que cortar 3 features, quais seriam?
  - Qual feature gera mais valor/impacto?

---

### 💻 SOBRE TÉCNICA

#### Plataforma
- [ ] **Web, Mobile ou ambos?**
  - MVP é web + mobile (React Native)?
  - Ou começa só web e mobile depois?

#### Infraestrutura
- [ ] **Hospedagem/Cloud:**
  - Prefere gerenciado (Firebase, Vercel)?
  - Ou VPS/self-hosted?
  - Budget para infraestrutura?

#### Integração
- [ ] **APIs necessárias:**
  - Instagram API (embed posts)?
  - Sympla API (se tiver ingresso lá)?
  - Pagamento (Stripe, PagSeguro, Pix)?

---

## 📋 DECISÕES CRÍTICAS A TOMAR

| Decisão | Opção A | Opção B | Opção C | Status |
|---------|---------|---------|---------|--------|
| **Começar com quantas casas?** | 1 (piloto) | 2-3 | Todas 6 | ❓ |
| **Reserva é obrigatória?** | Sim | Não (só notificação) | Opcional | ❓ |
| **Cobrança de entrada** | Sim (via app) | Não (só reserva) | Depois | ❓ |
| **Gamificação no MVP?** | Sim | Não (Fase 2) | - | ❓ |
| **Instagram embed?** | Crítico | Nice-to-have | Fase 2 | ❓ |
| **Plataforma** | Web first | Mobile first | Ambas | ❓ |

---

## 🎯 FLUXOS AINDA NÃO DETALHADOS

### Fluxo de Reserva (Ponta a Ponta)
```
1. Usuário vê evento na timeline
2. Clica "Reservar"
3. Confirma quantidade de pessoas + telefone
4. Sistema valida (ainda tem espaço?)
5. Reserva é confirmada ou listada como "aguardando"?
6. Usuário recebe confirmação (notificação + email?)
7. Gerente vê a reserva no painel
8. Dia do evento: usuário faz check-in no app ou por QR code?
9. Gerente marca como "compareceu"
10. Unlock: pontos, badge, etc?
```

**O que falta definir:**
- Passo 4: Automático ou manual?
- Passo 6: Apenas notificação ou também email/SMS?
- Passo 8: QR code é obrigatório? Ou confiança?
- Passo 10: Gamificação já ativa?

---

### Fluxo de Notificação Inteligente
```
1. Usuário segue casa A, B, C
2. Casa A publica novo evento (sexta à noite)
3. Sistema identifica: sexta noite, gênero que usuário gosta?
4. Envia notificação: "House A tem nova festa sexta!"
5. Usuário clica notificação
6. Abre página do evento
7. Faz reserva ou só curte?
```

**O que falta definir:**
- Passo 3: Como saber o gênero/preferência do usuário?
  - Primeira vez que abre app, pede pra escolher?
  - Aprende com cliques/reservas?
- Frequência: 1 notificação/dia? 3? Sem limite?
- Hora da notificação: quando enviar? (manhã, tarde, noite?)

---

### 🎧 SOBRE ATRAÇÕES, FESTAS ITINERANTES E PARCEIROS (Ex: Beat Proibido, Cultura Subcult)

#### Fluxo de Divulgação
- [ ] **Como serão exibidos os eventos de artistas como o Beat Proibido?**
  - Aparecerão na timeline geral de eventos como "Beat Proibido no Môi" ou "Beat Proibido no Point"?
  - O perfil do artista terá uma página dedicada listando sua agenda de shows?
  - Haverá link direto para as reservas da casa onde eles vão tocar?

- [ ] **Como gerenciar festas itinerantes de nicho (Ex: Cultura Subcult)?**
  - Como exibir locais não convencionais/industriais (ex: Fábrica Inacabada Astúria) de forma clara no GPS/mapa?
  - Direcionamento para vendas externas de ingressos (ex: link do Sympla) em vez do sistema de reservas interna padrão do app.
  - Permitir links de redes sociais e canais oficiais de comunicação rápida (ex: linktree ou grupo oficial de WhatsApp no perfil da festa para liberação de lotes)?

- [ ] **Como diferenciar claramente uma atração/festa itinerante de uma casa física fixa?**
  - Badge visual explicativo ("Atração", "Festa Itinerante", "DJ Duo", etc.) para evitar que o usuário tente reservar um "Beat Proibido" ou "Cultura Subcult" como se fossem locais físicos fixos.
  - Mensagens informativas nas páginas desses perfis explicando sua natureza de evento temporário/itinerante.

- [ ] **Gerenciamento dos perfis de marcas e artistas:**
  - O próprio Luan/Beat Proibido e os organizadores da Cultura Subcult terão acesso a um painel de "Gerente de Evento/Artista" para atualizarem suas datas e informações?
  - Ou essas agendas serão centralizadas pelos administradores do app ou vinculadas pelas casas físicas parceiras?

---

### 👤 SOBRE O PERFIL DO CO-CRIADOR (Luan S. Barbosa - @luan.sbarbosa)

- [ ] **Onde e como exibir os créditos do Luan no aplicativo?**
  - Terá uma seção "Sobre o App" ou "Idealizado por" no menu de configurações/perfil?
  - Link direto para o Instagram do Luan no rodapé/créditos?
  - Ele terá um perfil diferenciado na plataforma (ex: badge ou marcação de "Co-Criador/Admin")?

---

### 🔌 SOBRE O CRM ACOPLADO À ZIG (`[DECISÃO #13]`)

> **Origem:** mensagem do Luan em 17/09/2026 — conheceu um grupo de Brasília com um
> Customer Relationship Management (CRM) que acopla na Zig e puxa todos os leads.
> Ele ficou de passar a visão completa depois.

**O que é, em uma linha:** a Zig é o cashless/Ponto de Venda (PDV) das casas; um CRM
plugado nela lê a base de **consumo** — quem entrou, o que consumiu, quanto gastou.

**Por que importa para nós:** a Zig só enxerga quem **já entrou e gastou**. Nós ficamos
um passo antes — intenção: quem viu o evento, quem reservou, quem reservou e não
apareceu. É dado que não existe dentro da Zig. A chave de junção entre os dois lados é
o CPF/telefone, que o cadastro do MVP já coleta.

- Funil completo só existe juntando os dois: `viu → reservou → chegou → gastou R$X`.
- Consequência de posicionamento: **não vendemos "damos dados para a casa"** — se ela já
  tem esse CRM, esse pitch morre. Vendemos o lado da demanda (descoberta + reserva).

**Perguntas a fazer ao Luan quando ele passar a visão:**

- [ ] Eles vendem para a **casa** ou para a **marca de festa**? (define quem é o cliente comum)
- [ ] Já atendem alguma das nossas seis casas? (revela se é parceiro ou concorrente)
- [ ] O CRM deles **recebe** dado de fora ou só **puxa** da Zig? (se só puxa, não há ponte)
- [ ] Quem fica dono da base do cliente final numa integração — eles, a casa, ou nós?
- [ ] Eles têm ou pretendem ter reserva/descoberta no produto? (sobreposição direta)

**Riscos registrados:**

- CRM de casa noturna está a um passo de virar app de reserva — pode ser concorrente.
- Dependência de terceiro, mesma variância que jogou a Sympla para a Fase 2 `[DECISÃO #9]`.
- Não reabre a `[DECISÃO #12]`: continuamos sem precisar da API da Zig. **Fora do piloto.**

---

## 📝 Checklist Pré-Conversa com Luan

- [ ] Imprimir este documento ou compartilhar digital
- [ ] Trazer o documento `01-base-informacional.md`
- [ ] Pensar em 3 cenários possíveis (otimista, realista, pessimista) de timeline
- [ ] Ter pen e papel para anotar respostas
- [ ] Perguntar pelos problemas atuais (não só apresentar solução)
- [ ] Validar se as 6 casas estão 100% interessadas ou só algumas
- [ ] Deixar claro: MVP é rápido, depois evolui
- [ ] Discutir o fluxo de promoção de artistas/atrações (Beat Proibido), marcas de festas itinerantes (Cultura Subcult) no app e a integração dos créditos do co-criador (Luan).
- [ ] Levantar as 5 perguntas do CRM acoplado à Zig `[DECISÃO #13]` quando o Luan passar a visão completa.

---

**Data de criação:** 15/07/2026  
**Última atualização:** 17/09/2026 — inclusão da `[DECISÃO #13]` (CRM acoplado à Zig)  
**Status:** Aguardando respostas
