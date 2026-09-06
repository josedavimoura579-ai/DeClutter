# DeClutter

Um painel de mídia unificado e estritamente cronológico — sem algoritmo, sem anúncio, sem recomendação.

Eu criei o DeClutter pra juntar Reddit, Mastodon e YouTube num único feed, ordenado só por data/hora, exatamente como as redes sociais eram antes dos algoritmos de engajamento decidirem o que a gente vê. Roda 100% no navegador, sem backend, sem conta, sem coleta de dados.

**🔗 Acesse aqui: [josedavimoura579-ai.github.io/DeClutter](https://josedavimoura579-ai.github.io/DeClutter/)**

## Por quê

Cansei de feeds "inteligentes" que otimizam pra prender minha atenção em vez de me manter informado. Fiz o DeClutter pra devolver o controle: você escolhe as fontes, e elas aparecem na ordem em que aconteceram. Só isso.

## Usando o site

Não precisa instalar nada nem criar conta. É só abrir o link acima e:

1. Toque em **"Fontes"** no topo
2. Adicione o que você quer acompanhar:
   - **Reddit** — nome do subreddit, ex: `technology`
   - **Mastodon** — usuário completo, ex: `@usuario@mastodon.social`
   - **YouTube** — o Channel ID do canal (encontrado na página do canal em *Sobre → Compartilhar canal → Copiar ID do canal*)
3. Toque em **"Atualizar"** — as notícias aparecem todas juntas, mais recente primeiro

Outras coisas que dá pra fazer:
- Ligar/desligar cada fonte na tela usando os botões **Reddit / Mastodon / YouTube** no topo, sem precisar remover nada
- Buscar por palavra dentro do feed
- Ativar atualização automática (5, 15 ou 30 min)
- Trocar pro modo escuro
- Se uma fonte falhar momentaneamente, o site mostra os últimos itens salvos com um aviso, em vez de sumir tudo

Tudo que você configura fica salvo só no seu próprio navegador — nada é enviado pra nenhum servidor meu ou de terceiros.

## Funcionalidades

- Feed único combinando **Reddit**, **Mastodon** e **YouTube**, em ordem estritamente cronológica
- Zero anúncios, zero rastreador, zero coleta de dados
- Cache local: se uma fonte cair, mostra os últimos dados salvos em vez de ficar em branco
- Filtro por fonte e busca por texto dentro do feed
- Atualização automática configurável e modo escuro
- Não precisa de build, framework ou backend: é um único arquivo HTML

## Rodando localmente / contribuindo

### Testar local

1. Baixe `index.html` deste repositório
2. Sirva com um servidor local (evita bloqueios de `file://`):
   ```bash
   python -m http.server 8080
   ```
3. Acesse `http://127.0.0.1:8080`

### Publicar sua própria versão

1. Faça um fork ou suba `index.html` pra raiz do seu repositório
2. Vá em **Settings → Pages → Source**, selecione a branch `main` e pasta `/ (root)`
3. Seu painel fica disponível em `https://SEU-USUARIO.github.io/SEU-REPOSITORIO/`

### Como funciona por baixo dos panos

| Fonte | API usada | Precisa de proxy CORS? |
|---|---|---|
| Reddit | `reddit.com/r/{sub}/new.json` (pública) | Sim |
| Mastodon | API pública do Mastodon (`/api/v1/`) | Não |
| YouTube | RSS por canal (`youtube.com/feeds/videos.xml`) | Sim |

Reddit e YouTube não liberam CORS para chamadas de navegador, então essas duas passam por proxies CORS públicos, com fallback automático entre três serviços diferentes caso algum esteja fora do ar. Mastodon já libera CORS nativamente em praticamente todas as instâncias.

### Limitações conhecidas

- Depende de proxies CORS de terceiros para Reddit/YouTube, que podem cair ocasionalmente
- Sem paginação/scroll infinito — mostro só os itens mais recentes de cada fonte a cada atualização
- Sem notificações push

### Contribuindo

Pull requests são bem-vindos. Algumas ideias que tenho em mente pro futuro:
- Proxy CORS auto-hospedado (Cloudflare Worker) em vez de depender de serviços públicos
- Suporte a mais fontes (RSS genérico, Bluesky, Lemmy)
- Modo "somente texto" para conexões lentas

## Licença

MIT — use, modifique e redistribua livremente.
