# SpotDL

Workspace for `https://spotify.downloaderize.com/en1/` (new pulls) and `https://spotsaver.net/` (in `Site`).

## Pulling the site

Run the `pull-site` workflow (Actions tab, Run workflow). Inputs: start page (default `https://spotify.downloaderize.com/en1/`), output folder (default `Downloaderize`), extra hosts to follow (cdn or api hosts). It saves every text file it can reach into `<folder>/files/<host>/...` and writes `<folder>/index.tsv` (status per URL), `<folder>/urls.txt` and `<folder>/endpoints.tsv` (API-looking strings found in scripts), then commits the result.

## index.html

A standalone page (reverse-engineered client, not a page proxy) that talks to SpotSaver's own API through Singuloxy, using the same proxy layer as `rtischeduler/DeepAI` (wisp list sync, probing, verification, automatic switching and retry).

- Search a song name or paste an `open.spotify.com` track, album or playlist link: `GET /api/spotify/?q=...` or `?url=...`.
- Play: `POST /api/get-id/` (finds the video when the result has none), then `POST /api/download/` with `format: "mp3"`. The returned audio is fetched through the proxy into memory and played in the page with a Play/Pause button per track. Nothing is saved to disk.
- Albums and playlists get a "Play all" button that plays the tracks in order.
- Every request goes through Singuloxy with a cookie jar kept in `localStorage`. If the proxy drops, a "Switch proxy" button appears.
