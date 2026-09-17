# Módulo Freelas — "Trabalhe na noite"

> Status: **ideia pós-MVP**, proposta por um sócio. Não entra no escopo de `05-escopo-mvp.md`. Este documento registra como o módulo funcionaria, onde está o risco e o que precisa ser respondido antes de estimar com seriedade. Tela de demonstração no protótipo: `index.html?aba=freelas`.

## 1. A proposta

A casa publica uma vaga (garçom, bartender, recepção, caixa), o freela vê os termos, aceita, assina o contrato no próprio app, trabalha o turno e recebe, com tributos e encargos resolvidos. O sócio já tem estrutura contábil para a parte fiscal; a ideia é acoplar essa estrutura ao app.

A dor é real e semanal: hoje a casa monta a equipe da noite por WhatsApp, com acerto em dinheiro ou Pix e recibo improvisado.

## 2. Divisão de responsabilidade

O app **não vira sistema contábil**. Ele faz a operação e entrega dados limpos; a contabilidade faz a parte fiscal.

| App | Contabilidade do sócio |
|---|---|
| Publicar vaga com termos estruturados | Definir o modelo de contrato por modalidade |
| Candidatura, aprovação e escala | Validar as regras de cálculo |
| Contrato gerado + assinatura eletrônica | Apurar tributos e emitir guias |
| Check-in e check-out do turno (mesmo QR code da portaria) | Enviar eSocial e EFD-Reinf quando aplicável |
| Cálculo do valor bruto e líquido | Conferir notas fiscais dos MEIs |
| Exportar o turno fechado para a contabilidade | Devolver status ("guia paga", "nota conferida") |

O "acoplamento" é a exportação. Enquanto não soubermos qual sistema contábil eles usam, a exportação é uma planilha por período; depois vira integração direta.

## 3. Fluxo

```
Casa publica vaga ─► Freela vê termos ─► Candidata-se ─► Casa aprova
                                                             │
                              Contrato gerado do modelo ◄────┘
                                        │
                          Assinatura eletrônica (freela e casa)
                                        │
                  Check-in / check-out do turno na portaria (QR code)
                                        │
                Turno fechado: horas, valor bruto, retenções, líquido
                     │                                    │
             Freela envia NFS-e                 Exportação para a contabilidade
                     │                                    │
            Casa paga via Pix                    Guias, eSocial, conferência
```

## 4. Modalidade de contratação — a decisão que define o produto

| Modalidade | Quem recolhe o quê | Complexidade | Risco trabalhista |
|---|---|---|---|
| **Microempreendedor Individual (MEI)** | Freela emite Nota Fiscal de Serviço eletrônica (NFS-e) e paga o próprio Documento de Arrecadação do Simples Nacional (DAS). Em regra a casa só paga a nota. | Baixa | Alto se for habitual |
| **Autônomo com Recibo de Pagamento Autônomo (RPA)** | Casa retém Instituto Nacional do Seguro Social (INSS) do freela, Imposto de Renda Retido na Fonte (IRRF) e, conforme o município, Imposto Sobre Serviços (ISS); paga contribuição patronal conforme o regime tributário; declara no eSocial. | Média | Alto se for habitual |
| **Intermitente (Consolidação das Leis do Trabalho, CLT, art. 452-A)** | Vínculo formal. A cada convocação: férias proporcionais + 1/3, 13º, descanso semanal remunerado, Fundo de Garantia do Tempo de Serviço (FGTS) e INSS. Convocação com no mínimo 3 dias corridos de antecedência. | Alta | Baixo |

**Recomendação para a primeira versão:** só MEI, com trava de habitualidade (ver 5.1). RPA entra na fase 2 com as regras de cálculo validadas pela contabilidade. Intermitente é o caminho para quem trabalha toda semana na mesma casa.

## 5. Riscos

### 5.1 Vínculo empregatício (o maior)
Garçom que trabalha toda sexta na mesma casa, sob ordens do gerente, preenche os requisitos de vínculo (pessoalidade, habitualidade, subordinação, onerosidade), seja MEI ou RPA. Se o app facilitar isso em escala, o histórico do app vira a prova do vínculo contra a casa e, possivelmente, contra nós.

Mitigação no produto: limite de turnos por freela na mesma casa em uma janela de tempo, alerta para a casa, e sugestão de migrar para intermitente. **Os limites precisam de um advogado trabalhista; a contabilidade não cobre essa parte.**

### 5.2 Função não permitida
Segurança privada é atividade regulada e exige empresa autorizada pela Polícia Federal. **Segurança não entra como freela avulso.** Verificar também se cada função oferecida é ocupação permitida ao MEI.

### 5.3 Dinheiro passando por nós
Se a casa paga o app e o app repassa ao freela, ficamos perto de atividade regulada pelo Banco Central. Caminho seguro: *split* de um Provedor de Serviços de Pagamento (PSP), como Asaas ou Pagar.me, em que o dinheiro nunca fica em conta nossa. Na primeira versão, a casa paga o freela por Pix direto e o app só registra.

### 5.4 Assinatura
Assinatura eletrônica é válida em contrato privado (Lei 14.063/2020). Integrar um serviço (ZapSign, Clicksign ou D4Sign) por API e webhook; não construir assinatura própria.

## 6. Onde encaixa no GoDrinking

- **Mesmo backend, experiência separada.** O cliente procura onde beber hoje; o freela procura trabalho. No protótipo a entrada é um cartão no fim da aba Casas e o link `?aba=freelas`, e **não** um item da barra inferior.
- **Reaproveita:** conta da casa, painel da portaria, check-in por QR code, motor de datas das noites (a vaga herda a data da programação).
- **Receita:** é o lado B2B com dor clara. Opções: taxa por turno fechado, mensalidade por casa, ou participação na contabilidade do sócio. Já existem empresas de *staffing* sob demanda para bares e restaurantes no Brasil; mapear concorrentes antes de decidir preço.

## 7. Versão enxuta para validar

Escopo: só MEI, 1 casa, publicação de vaga feita por nós (como a programação no MVP), sem pagamento no app.

Estimativa por tarefa, para 1 pessoa (**julgamento, não medido**; referência: as partes análogas do `05-escopo-mvp.md`):

| Tarefa | Dias úteis |
|---|---|
| Cadastro do freela + validação do CNPJ do MEI por API pública | 3–4 |
| Publicação de vaga (admin) | 2 |
| Lista de vagas, termos, candidatura e aprovação | 3 |
| Contrato por modelo + integração de assinatura (webhook) | 3–4 |
| Check-in e check-out do turno reaproveitando o QR code | 2 |
| Painel da casa: escala da noite | 3 |
| Exportação para a contabilidade (planilha até definirmos o sistema) | 1–2 |
| Notificações (aprovação, lembrete do turno, nota pendente) | 2 |
| Testes, textos jurídicos no app, ajustes | 3 |
| **Total** | **22–25 (≈ 4,5 a 5 semanas)** |

Fica de fora: RPA, intermitente, pagamento no app, avaliação mútua, casa publicando a própria vaga.

## 8. Perguntas em aberto

Para o sócio e a contabilidade:
- [ ] Qual sistema contábil usam (Domínio, Alterdata, Questor, outro)? Define o formato da exportação.
- [ ] Eles aceitam receber os turnos por planilha na primeira fase?
- [ ] Qual modalidade as casas usam hoje com os freelas? Quantos são MEI?
- [ ] Quem redige e mantém o modelo de contrato?
- [ ] Qual o modelo de receita: taxa por turno, mensalidade, ou divisão com a contabilidade?

Para um advogado trabalhista:
- [ ] Qual limite de turnos por freela e casa reduz o risco de vínculo a um nível aceitável?
- [ ] Quais funções da noite podem ser contratadas como MEI?

Para nós:
- [ ] Confirmar que o módulo só começa depois do piloto do MVP.

*Criado: 17/09/2026.*
