# Basketball · C.D.P. · Época 2026/27

Livro de jogadas animadas. Site estático, pronto para GitHub Pages.

## Estrutura

```
index.html          Homepage (logotipo, época, lista de jogadas)
jogada-3.html       Uma página por jogada (só dados)
assets/estilo.css   Estilo partilhado
assets/motor.js     Motor de animação partilhado
assets/cdp.png      Emblema do clube
robots.txt          Bloqueia indexação
.nojekyll           Evita processamento Jekyll no GitHub Pages
```

## Publicar no GitHub Pages

1. Criar repositório e enviar todos os ficheiros para a raiz.
2. Settings > Pages > Source: branch `main`, pasta `/ (root)`.
3. O site fica em `https://<utilizador>.github.io/<repositório>/`.

Atenção: num repositório público, o código e as jogadas ficam visíveis para qualquer pessoa. O `noindex` só afasta os motores de pesquisa.

## Formato de uma jogada (padrão a manter)

Cada página de jogada é uma cópia de `jogada-3.html` com o bloco `window.JOGADA` alterado.

- `titulo`, `intro`: título e descrição curta.
- `inicio.pos`: posição inicial de cada jogador `{n:[x,y]}`.
- `inicio.bola`: número do jogador com a bola. `inicio.c` é a legenda inicial.
- `fases`: lista ordenada. Cada fase tem `h` (nome), `c` (legenda) e `a` (acções).
- `alternativas`: finalizações à escolha (quem lança ou decide). Cada uma tem `rotulo` (botão), `h`, `c` e `a`. Pode ter quantas forem precisas, ou nenhuma.
- Uma alternativa pode ter vários passos: em vez de `h`, `c`, `a`, usa `passos:[{h,c,a},…]` (útil quando a decisão acontece antes do fim da jogada).
- `perguntaAlternativas`: texto acima dos botões de alternativa.
- `resumo`: lista de texto mostrada no fim da página.

### Acções (`a`)

- Deslocação: `{m:4, to:[x,y], t:[início,fim]}`
- Curva: acrescentar `c:[x,y]` (ponto de controlo).
- Drible: acrescentar `d:1` (linha ondulada).
- Bloqueio: acrescentar `s:1` (traço em T no final).
- Passe: `{p:1, t:[início,fim]}`, da bola actual para o jogador indicado.
- Lançamento: `{p:'B', t:[...]}`, com `c:[x,y]` para dar arco.

`t` vai de 0 a 1 dentro da fase e permite movimentos simultâneos ou desfasados.

### Coordenadas do campo (viewBox 400 × 345)

- Linha de fundo em cima (y = 20), cesto em (198, 67).
- Linhas laterais em x = 34 e x = 362; reposição fora do campo em x ≈ 379.
- Garrafão: x 158–237, até y = 158. Linha de 3: cantos em x = 55 e 340.

### Notação visual

Linha contínua = deslocação · ondulada = drible · tracejada = passe · T = bloqueio.

## Acrescentar uma jogada

1. Copiar `jogada-3.html` para `jogada-<nome>.html` e substituir o bloco `JOGADA`.
2. Em `index.html`, trocar a linha `<div class="jogada off">…</div>` por:
   `<a class="jogada" href="jogada-<nome>.html"><strong>…</strong><span>…</span></a>`
