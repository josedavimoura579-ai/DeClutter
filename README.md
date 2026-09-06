# DeClutter

Um painel de mídia unificado e estritamente cronológico — sem algoritmo, sem anúncio, sem recomendação.

Eu criei o DeClutter pra juntar Reddit, Mastodon e YouTube num único feed, ordenado só por data/hora, exatamente como as redes sociais eram antes dos algoritmos de engajamento decidirem o que a gente vê. Roda 100% no navegador, sem backend, sem conta, sem coleta de dados.

## Por quê

Cansei de feeds "inteligentes" que otimizam pra prender minha atenção em vez de me manter informado. Fiz o DeClutter pra devolver o controle: você escolhe as fontes, e elas aparecem na ordem em que aconteceram. Só isso.

## Funcionalidades

- Feed único combinando **Reddit** (subreddits), **Mastodon** (contas públicas) e **YouTube** (canais)
- Ordem estritamente cronológica — sem curadoria, sem "conteúdo recomendado"
- Zero anúncios, zero rastreador, zero coleta de dados
- Configuração das fontes fica salva só no seu navegador (`localStorage`) — não envio nada pra nenhum servidor
- Não precisa de build, framework ou backend: é um único arquivo HTML

## Como usar

### Direto no navegador

1. Baixe `index.html` deste repositório
2. Abra num servidor local (recomendo, evita bloqueios de `file://`):
   ```bash
   python -m http.server 8080
   ```
   e acesse `http://127.0.0.1:8080`
3. Clique em **Configurar fontes** e adicione:
   - Subreddits (ex: `technology`)
   - Contas Mastodon (ex: `@usuario@mastodon.social`)
   - Channel ID do YouTube (encontrado em *Sobre → Compartilhar canal → Copiar ID do canal*)
4. Clique em **Atualizar feed**

### Publicando no GitHub Pages (grátis)

1. Suba `index.html` para a raiz deste repositório
2. Vá em **Settings → Pages → Source**, selecione a branch `main` e pasta `/ (root)`
3. Seu painel fica disponível em `https://SEU-USUARIO.github.io/DeClutter/`

## Como funciona por baixo dos panos

| Fonte | API usada | Precisa de proxy CORS? |
|---|---|---|
| Reddit | `reddit.com/r/{sub}/new.json` (pública) | Sim |
| Mastodon | API pública do Mastodon (`/api/v1/`) | Não |
| YouTube | RSS por canal (`youtube.com/feeds/videos.xml`) | Sim |

Reddit e YouTube não liberam CORS para chamadas de navegador, então essas duas passam por um proxy CORS público (com um segundo proxy como plano B, caso o primeiro esteja fora do ar). Mastodon já libera CORS nativamente em praticamente todas as instâncias.

## Limitações conhecidas

- Depende de proxies CORS de terceiros para Reddit/YouTube, que podem cair ocasionalmente
- Sem paginação/scroll infinito — mostro só os itens mais recentes de cada fonte a cada atualização
- Sem notificações push nem atualização automática em segundo plano

## Contribuindo

Pull requests são bem-vindos. Algumas ideias que tenho em mente pro futuro:
- Proxy CORS auto-hospedado (Cloudflare Worker) em vez de depender de serviços públicos
- Suporte a mais fontes (RSS genérico, Bluesky, Lemmy)
- Modo "somente texto" para conexões lentas

## Licença

MIT — use, modifique e redistribua livremente.
