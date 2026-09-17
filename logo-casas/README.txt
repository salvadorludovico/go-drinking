Como Adicionar os Logos Reais das Casas Noturnas:

Para que os logos reais das baladas apareçam automaticamente no aplicativo LUAN, basta seguir este passo a passo simples (sem precisar mexer em nenhuma linha de código):

1. Acesse o Instagram de cada casa e salve a imagem de perfil dela (ou qualquer logo que preferir).
2. Salve as imagens dentro desta pasta "logo-casas" exatamente com os seguintes nomes e formatos:
   - subcult.png
   - moi.png
   - fluxo.png
   - cajuina.png
   - mosaic.png
   - vernissage.png
   - beatproibido.png

Formatos suportados: .png, .jpg ou .jpeg.
O aplicativo possui um sistema inteligente de fallback: se você não colocar a imagem de alguma casa, ele não mostrará o círculo ou as iniciais, deixando a interface limpa e minimalista de forma automática!

Capas (imagem grande dos cartões e da página da casa):
- Salve como "<id>-capa.jpg" nesta pasta (ex.: moi-capa.jpg), de preferência na vertical (720x1280).
- As capas atuais são frames dos vídeos do Vibes (ffmpeg -ss 4 -i moi.mp4 -frames:v 1 -vf scale=720:-2 moi-capa.jpg).
- Sem capa, o app mostra o logo sobre um fundo com a cor da casa.
