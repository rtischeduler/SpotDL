# SpotDL

Workspace for `https://spotsaver.net/`.

## Pulling the site

Run the `pull-spotsaver` workflow (Actions tab, Run workflow). Inputs: start page (default `https://spotsaver.net/`), output folder (default `Site`), extra hosts to follow (cdn or api hosts). It saves every text file it can reach into `Site/files/<host>/...` and writes `Site/index.tsv` (status per URL), `Site/urls.txt` and `Site/endpoints.tsv` (API-looking strings found in scripts), then commits the result.

## index.html

A standalone page (reverse-engineered client, not a page proxy) that talks to SpotSaver's own API through Singuloxy, using the same proxy layer as `rtischeduler/DeepAI` (wisp list sync, probing, verification, automatic switching and retry).

- Search a song name or paste an `open.spotify.com` track, album or playlist link: `GET /api/spotify/?q=...` or `?url=...`.
- Play: `POST /api/get-id/` (finds the video when the result has none), then `POST /api/download/` with `format: "mp3"`. The returned audio is fetched through the proxy into memory and played in the page with a Play/Pause button per track. Nothing is saved to disk.
- Albums and playlists get a "Play all" button that plays the tracks in order.
- Every request goes through Singuloxy with a cookie jar kept in `localStorage`. If the proxy drops, a "Switch proxy" button appears.
