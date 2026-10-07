# Proposta de estrutura do repositório

> Status: **proposta, nada foi movido nem apagado.** Se aprovar, a migração é a seção 4. Até lá, `base/`, `tasks/` e o `index.html` continuam valendo como histórico.

## 1. O problema da estrutura atual

| Sintoma | Exemplo | Efeito |
|---|---|---|
| Documentos empilhados por data, não por assunto | `01` e `03` (julho) dizem "MVP em 4–6 semanas, React + Node + Redis"; `05` e `06` (agosto/setembro) dizem "16 semanas, Supabase" | Ninguém sabe qual vale. Nenhum documento diz "este substitui aquele". |
| Decisão, pergunta e desejo misturados | `02` tem cerca de 60 checkboxes; `04` diz que só 13 importam; nenhuma foi fechada | Dois meses depois, zero decisões registradas |
| `tasks/todo.md` virou diário de bordo | 240 linhas de changelog de sessões de agente | Não serve como lista de tarefas, e fica na raiz |
| Protótipo, mídia e PWA misturados na raiz | `index.html`, `manifest.json`, `favicon.jpg`, `logo-casas/` | Parece que o protótipo é o produto |
| Nome do produto inconsistente | `LUAN` no manifest e no título, `GoDrinking` nos docs, "Sistema de Reservas" no `01` | Ninguém de fora sabe como chamar a coisa |
| Sem `README.md` nem regras para agentes | Cada sessão de agente escreve no estilo que quer | Texto longo, retórico, com números inventados apresentados como fato |

## 2. Estrutura proposta

```
README.md                  O que é, estado atual em 10 linhas, como abrir o protótipo, onde está cada coisa
CLAUDE.md                  Regras para agentes (ver CLAUDE.proposto.md nesta pasta)
CONTEXT.md                 Glossário do domínio: Casa, Noite, Lista, Mesa, Camarote... (ver CONTEXT.md nesta pasta)

docs/
  visao.md                 Uma página: problema, para quem, proposta de valor, o que o MVP prova
  estado-atual.md          O que existe de verdade hoje (protótipo, código, contratos, casas que toparam)
  decisoes/                Uma decisão por arquivo, numerada, com status: proposta | aceita | substituída
    0001-nome-do-produto.md
    0002-reserva-de-mesa-exige-sinal.md
    ...
  produto/
    escopo-mvp.md          Features com critério de aceite (herda o melhor do 05)
    jornadas.md            Herda o 08, enxugado
    modulos/
      planos.md            Assinatura com tiers (pós-MVP)
      freelas.md           Contratação de freelas (pós-MVP)
  pesquisa/                Pesquisa externa, sempre com data e fontes. Não é decisão.
    2026-10-concorrentes.md
    2026-10-zig.md
    ...
  tecnico/
    arquitetura.md         Só depois que a decisão de stack existir
    infra-e-custos.md      Herda o 06
  perguntas-abertas.md     O que ainda não sabemos, com dono de cada pergunta

prototipo/                 Tudo que é demonstração, separado do produto
  index.html
  manifest.json
  favicon.jpg
  midia/                   Antigo logo-casas/

.agent/                    Planos de sessões de agente: .agent/2026-10-02-<slug>/plano.md
                           (substitui tasks/todo.md; o histórico antigo vai para cá)

app/  ou  apps/            Código real, quando começar (não existe ainda)
```

## 3. Regras que fazem a estrutura funcionar

1. **Decisão só existe em `docs/decisoes/`.** Se está em outro lugar, é opinião. Cada arquivo tem: contexto em 3 linhas, opções, escolha, data, quem decidiu, e o que muda se mudarmos de ideia.
2. **Pesquisa tem data e fonte em toda afirmação.** Concorrente muda de preço, API muda de versão. Pesquisa sem data envelhece em silêncio.
3. **Número sem base não entra.** Toda estimativa ou métrica diz de onde veio: medição, comparação, ou "julgamento, não medido".
4. **Um documento substituído ganha uma linha no topo** apontando para o que o substitui. Não se apaga, não se deixa competir.
5. **`estado-atual.md` é atualizado no fim de cada sessão de trabalho.** É o primeiro arquivo que você ou um agente lê ao voltar ao projeto. Este pedido de hoje ("faz tempo que não mexo, me situa") vira 2 minutos de leitura em vez de uma auditoria.

## 4. Migração (só depois de aprovar)

| Hoje | Vai para | Como |
|---|---|---|
| `base/01-base-informacional.md` | `docs/visao.md` + `CONTEXT.md` + `docs/pesquisa/2026-07-casas-mapeadas.md` | Reescrever; o original vai para `docs/arquivo/` |
| `base/02-definicoes-pendentes.md` | `docs/perguntas-abertas.md` | Cortar de ~60 para as que ainda importam, com dono |
| `base/03-roadmap-arquitetura.md` | `docs/arquivo/` | Superado pelo `05` e `06`; stack ainda não decidida |
| `base/04-processo-notas-para-prazo.md` | `docs/arquivo/` + método resumido no `CLAUDE.md` | O método (PERT, fatias verticais) é bom; o resto é carta ao CTO |
| `base/05-escopo-mvp.md` | `docs/produto/escopo-mvp.md` | Revisar com o escopo novo (mesa, camarote, Zig) |
| `base/06-infra-e-custos.md` | `docs/tecnico/infra-e-custos.md` | Manter; marcar premissas como não validadas |
| `base/07-modulo-freelas.md` | `docs/produto/modulos/freelas.md` | Incorporar a pesquisa de `pesquisa/freelas.md` |
| `base/08-jornadas.md` | `docs/produto/jornadas.md` | Enxugar; adicionar jornada de mesa/camarote |
| `tasks/todo.md` | `.agent/2026-07-a-09-historico.md` | Mover inteiro, sem editar |
| `index.html`, `manifest.json`, `favicon.jpg`, `logo-casas/` | `prototipo/` | `git mv`; corrigir caminhos de mídia no HTML |
| `proposta/LEIA-PRIMEIRO.md` | `docs/visao.md` + `docs/estado-atual.md` | Dividir |
| `proposta/pesquisa/*` | `docs/pesquisa/2026-10-*.md` | Mover |
| `proposta/decisoes.md` | `docs/decisoes/000N-*.md` | Um arquivo por decisão, à medida que forem fechadas |

Esforço da migração: uma sessão de trabalho com agente, cerca de 1 a 2 horas (julgamento, não medido). O risco é só quebrar caminhos de mídia do protótipo ao mover para `prototipo/`, e isso se verifica abrindo a página.
