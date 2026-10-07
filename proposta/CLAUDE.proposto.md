# Regras para agentes neste repositório (proposta)

> Quando aprovado, este arquivo vira o `CLAUDE.md` da raiz. Está com outro nome para não ser carregado antes da hora.

## Antes de começar
- Leia `docs/estado-atual.md` e `CONTEXT.md`. Use os termos do glossário; se precisar de um termo novo, adicione-o lá.
- Decisões vigentes estão em `docs/decisoes/`. Não contradiga uma decisão aceita sem dizer isso explicitamente ao usuário.

## Onde escrever
- Plano de sessão: `.agent/<AAAA-MM-DD>-<slug>/plano.md`. Nunca `tasks/` nem arquivos soltos na raiz.
- Pesquisa externa: `docs/pesquisa/<AAAA-MM>-<tema>.md`, com fonte (URL) em cada afirmação e "não confirmado" quando for o caso.
- Decisão: só em `docs/decisoes/`, depois que o usuário decidir. Agente propõe; humano decide.
- Ao fim da sessão: atualize `docs/estado-atual.md` com o que mudou, em até 10 linhas.

## Como escrever
- Português do Brasil. Sigla por extenso na primeira ocorrência de cada documento.
- Um parágrafo é uma linha. Não quebre linha por limite de caracteres.
- Conciso. Tabela quando há comparação; prosa quando há argumento. Sem retórica ("momento da verdade", "desconfortável", "acabou").
- Todo número diz de onde veio: medido, comparado com algo citado, ou "julgamento, não medido". Premissa não validada fica marcada como premissa.
- Documento substituído ganha uma linha no topo apontando o substituto. Não apague.

## Protótipo
- `prototipo/index.html` é demonstração descartável. Não é a base do produto.
- Ferramentas de demonstração (relógio simulado, troca de papel) ficam atrás de `?demo=1`, nunca na interface principal.
