# Infraestrutura e Custo — 7 casas

> Premissa da reunião: **pagamos a infra do próprio bolso no começo**, sem
> depender de créditos de startup. O objetivo aqui é mostrar que isso é
> confortável — e onde está o custo que realmente machuca (não é o servidor).

## 1. Correção de duas premissas da ata

**"Plataforma com 1.000 usuários custa ~R$700/mês de infra."**
Esse número só aparece quando há vídeo mal servido, banco superdimensionado ou
serviço gerenciado caro. Para o perfil do GoDrinking, 1.000 usuários custam
**menos de R$150/mês**. O custo escala com *tráfego de vídeo* e *SMS*, não com
número de cadastros.

**"Capacidade atual de ~500 acessos simultâneos é insuficiente para produção."**
Ao contrário: 500 simultâneos é **3 a 6x** o pico projetado para as 7 casas.
Uma sexta-feira inteira de todas as casas não chega perto disso. O gargalo do
projeto não vai ser capacidade; vai ser conteúdo atualizado e adoção.

## 2. Modelo de carga (mostre esta tabela aos sócios)

Premissas — **valide a primeira linha com o Luan, tudo depende dela**:

| Parâmetro | Valor assumido |
|---|---|
| Seguidores somados das 7 casas | ~200.000 (a confirmar) |
| Conversão para cadastro em 6 meses | 4% |
| **Cadastros ao fim do semestre** | **~8.000** |
| Ativos no mês (MAU) | ~2.500 |
| Ativos na semana (WAU) | ~1.200 |
| Concentração de acesso | sexta e sábado, 19h-23h |

Disso sai o pico real:

```
1.200 ativos/semana x 40% concentrados numa janela de 4h  =  ~480 sessoes
480 sessoes / 4h, sessao media de 5 min                   =  ~100 usuarios simultaneos
100 simultaneos x ~0,1 requisicao/s                       =  ~10 requisicoes/s de pico
```

**10 req/s.** Um único servidor pequeno com cache atende isso com folga de uma
ordem de magnitude. E a maior parte do tráfego é leitura de programação — o
conteúdo mais cacheável que existe, porque muda uma vez por semana.

O que realmente pesa é diferente:
- **Vídeo (Vibes):** 2.500 pessoas x 20 vídeos x 5 MB = **~250 GB/mês** de saída.
- **SMS de OTP:** cada cadastro e cada login custa dinheiro por unidade.

## 3. Arquitetura recomendada e custo mensal

**Opção A — Gerenciado (recomendada).** Menos tempo seu em infra, e o seu tempo
é o recurso mais caro do projeto.

| Componente | Serviço | Custo/mês (BRL, aprox.) |
|---|---|---|
| Auth + Postgres + Storage + backup | Supabase Pro | ~R$ 140 |
| API backend | Fly.io / Render (instância pequena) | ~R$ 60 |
| PWA (frontend estático) | Cloudflare Pages | R$ 0 |
| Mídia e vídeo | Cloudflare R2 (**egress grátis**) | ~R$ 15 |
| E-mail transacional | Resend (até 3k/mês grátis) | R$ 0 - 110 |
| Push | Firebase Cloud Messaging | R$ 0 |
| Erros e uptime | Sentry free + UptimeRobot | R$ 0 |
| Domínio | .com.br | ~R$ 4 |
| **Total operacional** | | **~R$ 220 - 330 / mês** |

**Opção B — VPS único.** Hetzner CPX21 ou similar, Postgres e API na mesma
máquina: **~R$ 120/mês**. Economiza ~R$150, custa algumas horas suas por mês em
backup, atualização e madrugada de incidente. Não recomendo no começo.

### Por que Cloudflare R2 e não S3 para os vídeos

250 GB/mês de saída: no S3 isso é ~US$ 22 (~R$ 120) **só de transferência**, e
cresce linear com o sucesso do app. No R2 a saída é gratuita — paga-se só o
armazenamento, ~R$ 15. É a decisão de infra com melhor retorno do projeto, e é o
motivo pelo qual "vídeo é caro" não precisa ser verdade aqui.

## 4. O custo escondido: SMS

Se o login for por telefone + código SMS:

```
8.000 cadastros + ~7.000 logins/reenvios = ~15.000 SMS
15.000 x R$ 0,10 (media Brasil)          = ~R$ 1.500 no semestre
```

Isso é **5x a conta de servidor**. Três saídas, em ordem de preferência:

1. **OTP por e-mail** — custo próximo de zero, e o e-mail já é obrigatório no cadastro.
2. **OTP por WhatsApp** (API oficial) — mais barato que SMS e melhor conversão no Brasil, mas exige verificação de negócio e aprovação de template: comece o processo cedo, ele não depende de nós.
3. **SMS só como fallback**, para quem não recebeu por e-mail.

Decidir isso é a `[DECISÃO #6]` do doc `04` — e agora ela tem preço.

## 5. Como o custo escala

| Cenário | Cadastros | Infra/mês |
|---|---|---|
| Piloto (1 casa) | ~1.000 | ~R$ 150 |
| **7 casas** | ~8.000 | **~R$ 300** |
| 13 casas (meta 2027) | ~25.000 | ~R$ 700 - 1.000 |
| Sucesso inesperado | 100.000 | ~R$ 3.000 - 5.000 |

Compare com a receita: **7 casas x R$ 500/mês de assinatura = R$ 3.500/mês.**
A infra consome ~9% da receita no cenário das 7 casas. É saudável e não é o que
define a viabilidade do negócio — o que define é as casas pagarem a assinatura.

## 6. Sobre créditos de nuvem (mesmo tendo decidido pagar)

Concordo com pagar no início: R$300/mês não justifica travar a arquitetura em
AWS ou GCP para caber num programa de créditos. Mas registre isto para depois: o
**Google for Startups** e o **AWS Activate** costumam exigir apenas CNPJ e um
site — e o valor liberado tipicamente cobre o cenário de 13 casas por um ano
inteiro. Vale acionar quando o CNPJ existir, sem reescrever nada; a Opção A é
portável.

## 7. Checklist de fundação (entra na estimativa da fatia 8 do doc `05`)

- [ ] Backup diário do Postgres com **restauração testada** — backup não testado não é backup
- [ ] Ambiente de staging separado do de produção
- [ ] Deploy automatizado e rollback em um comando
- [ ] Alerta de erro (Sentry) e de queda (UptimeRobot) chegando no seu celular
- [ ] Rate limit nos endpoints de reserva e de OTP
- [ ] Aviso de privacidade e base legal para CPF/data de nascimento (LGPD)
- [ ] Painel simples de métricas do piloto: cadastros, reservas, check-ins, show-rate

> Valores em BRL convertidos a ~R$5,50/USD, para referência de ordem de grandeza.
> Confirme os preços vigentes antes de fechar contrato.
