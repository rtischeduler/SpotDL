# SpotDL

Workspace for `https://spotsaver.net/`.

## Pulling the site

Run the `pull-spotsaver` workflow (Actions tab, Run workflow). Inputs: start page (default `https://spotsaver.net/`), output folder (default `Site`), extra hosts to follow (cdn or api hosts). It saves every text file it can reach into `Site/files/<host>/...` and writes `Site/index.tsv` (status per URL), `Site/urls.txt` and `Site/endpoints.tsv` (API-looking strings found in scripts), then commits the result.
