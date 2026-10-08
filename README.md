# Reddit-CFMod

Extensão do Chrome (Manifest V3) para editar custom feeds do Reddit em massa.

Na página de um custom feed (`reddit.com/user/<você>/m/<feed>`), o botão **Adição Customizada** abre um modal central com:

- **No feed:** as comunidades que já estão no feed, cada uma com botão de remover.
- **Comunidades que você segue:** as que ainda não estão no feed, com busca, checkbox, "todas visíveis" e o botão **Adicionar selecionadas**.

O botão **Adição Customizada** da extensão fica logo à direita do botão nativo "Add Communities" (feed vazio) ou do botão de editar o feed. Se nenhum dos dois aparecer na tela, ele flutua no canto inferior direito.

## Instalação

1. Abra `chrome://extensions`.
2. Ative o **Modo do desenvolvedor**.
3. Clique em **Carregar sem compactação** e escolha esta pasta.
4. Entre em um custom feed seu no www.reddit.com.

## Privacidade

- A extensão nunca chama API de IA nem servidor de terceiros. A única origem acessada é `https://www.reddit.com`, com a sua sessão já logada.
- A permissão de host cobre só `www.reddit.com`.
- O cache da lista de comunidades seguidas (dura 10 min) fica em `chrome.storage.local`, só neste dispositivo. Não usa `storage.sync`.

- O rodapé tem um link para a bee6. Ele é um link comum: só abre algo se você clicar.
- As fontes da marca (Archivo, Staatliches) não são baixadas. Se não estiverem instaladas no sistema, o painel usa Arial.

## Idioma

A extensão lê a língua do navegador (`navigator.languages`). Português e espanhol têm tradução própria; qualquer outra língua cai no inglês. O nome e a descrição em `chrome://extensions` seguem o mesmo padrão via `_locales/`.

| Língua | Link do rodapé |
|---|---|
| Português | https://bee6.com.br/ |
| Inglês e demais | https://bee6.com.br/en |
| Espanhol | https://bee6.com.br/es |

## Ícone

`icons/` tem o ícone em 16, 32, 48 e 128 px. Desenho: favo laranja da bee6 sobre vidro escuro, com as camadas do feed dentro e um "+".

## Como funciona

| Ação | Endpoint |
|---|---|
| Comunidades seguidas | `GET /subreddits/mine/subscriber.json` (paginado) |
| Ler o feed | `GET /api/multi/user/<u>/m/<feed>` |
| Adicionar | `PUT /api/multi/user/<u>/m/<feed>/r/<sub>` com `X-Modhash` |
| Remover | `DELETE /api/multi/user/<u>/m/<feed>/r/<sub>` com `X-Modhash` |

As adições saem uma de cada vez, com 350 ms de intervalo, para não bater no rate limit.

## Limitações conhecidas

- Depois de adicionar, recarregue a página para o feed nativo mostrar as mudanças.
- Feeds de outros usuários abrem só para leitura.

## Licença

MIT. Veja [LICENSE](LICENSE).
