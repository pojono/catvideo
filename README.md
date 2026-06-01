# Cat Video

Static placeholder for `catvideo.space`.

## Deploy

GitHub Actions deploys every push to `main` or `master` to `/opt/catvideo` on the server and restarts Caddy.

Required repository secrets:

- `DEPLOY_HOST`: `89.169.138.111`
- `DEPLOY_USER`: `ubuntu`
- `DEPLOY_SSH_KEY`: private deploy key generated only for this site

Current deploy key:

- private key on local machine: `~/.ssh/catvideo_deploy_ed25519`
- public key installed on server: `~/.ssh/authorized_keys`

Do not use the local administrative key `~/.ssh/tasks_deploy` as a GitHub secret.
