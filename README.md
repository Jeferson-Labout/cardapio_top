# Top Espetinho — Cardápio Digital

Cardápio digital de página única para o Top Espetinho. Sem back-end, sem build: um `index.html` que lê os preços de uma planilha do Google Sheets publicada como CSV e atualiza a página sozinho.

## Como funciona

- Os preços ficam numa Google Planilha, publicada em **Arquivo › Compartilhar › Publicar na Web** no formato **CSV**.
- O site busca esse CSV a cada carregamento de página e monta as categorias e itens automaticamente.
- Se a planilha estiver fora do ar ou o link não estiver configurado, o site usa uma cópia de preços embutida no próprio `index.html` (bloco `<script id="precos-reserva">`), então o cardápio nunca fica em branco.
- Colunas do CSV: `categoria, item, descricao, preco, preco2, disponivel`. Deixe `disponivel` como `não` para esconder um item sem apagar a linha.

## Configuração

1. Abra o `index.html` num editor de texto.
2. Publique a aba de preços da planilha como CSV (Arquivo › Compartilhar › Publicar na Web) e copie o link gerado (formato `.../pub?...&output=csv`).
3. Cole o link na constante `PLANILHA_CSV_URL`, perto do topo do bloco `<script>`.
4. Para adicionar uma categoria nova, basta criar linhas com esse nome de categoria na planilha — ela aparece sozinha no site. Para configurar colunas de preço (ex: "Simples"/"Completo") ou uma observação fixa da categoria, edite o objeto `CATEGORIAS` no `index.html`.

## Testar localmente

Como o site busca dados de outra origem (`fetch`), abrir o arquivo direto (`file://`) pode falhar por causa de CORS. Sirva a pasta por um servidor local:

```bash
npx serve .
```

Depois abra a URL indicada (ex.: `http://localhost:3000`) no navegador.

## Publicar

Qualquer host de arquivos estáticos serve: arraste a pasta em [app.netlify.com/drop](https://app.netlify.com/drop), ou publique via GitHub Pages / Cloudflare Pages. Não precisa de servidor, banco de dados ou processo de build.

## Licença

MIT — veja [LICENSE](LICENSE).
