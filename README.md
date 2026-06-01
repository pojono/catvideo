# Cat Video

Static placeholder for `catvideo.space`.

## Deploy

GitHub Actions deploys every push to `main` or `master` to `/opt/catvideo` on the server and restarts Caddy.

Required repository secrets:

- `DEPLOY_HOST`: `89.169.138.111`
- `DEPLOY_USER`: `ubuntu`
- `DEPLOY_SSH_KEY`: private SSH key with access to the server
