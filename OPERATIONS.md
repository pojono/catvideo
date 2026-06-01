# Catvideo Operations

## Timeweb media storage

- Main media bucket: `catvideo-media-hot`, bucket id `511863`, storage class `hot`.
- Main CDN resource for `media.catvideo.space`: id `12499`, CDN domain `lhb1nb752z.cdn.twcstorage.ru`.
- Public media domain: `https://media.catvideo.space`.
- Timeweb API token is stored locally in `~/.twcrc`. Never print or commit it.

## S3 credentials

Do not use the default local AWS profile for this bucket. It is not the bucket user and returns `403`.

For object uploads, read the Object Storage user credentials from Timeweb API and pass them only through environment variables:

```sh
TOKEN=$(/usr/bin/awk -F'"' '/token/{print $2; exit}' "$HOME/.twcrc")
USERS=$(/usr/bin/curl -sS -H "Authorization: Bearer $TOKEN" \
  https://api.timeweb.cloud/api/v1/storages/users)
AWS_ACCESS_KEY_ID=$(/opt/homebrew/bin/jq -r '.users[0].access_key' <<<"$USERS")
AWS_SECRET_ACCESS_KEY=$(/opt/homebrew/bin/jq -r '.users[0].secret_key' <<<"$USERS")
AWS_DEFAULT_REGION=ru-1
AWS_CONFIG_FILE=/dev/null
AWS_SHARED_CREDENTIALS_FILE=/dev/null
```

Do not echo these values. Use `aws --endpoint-url https://s3.twcstorage.ru ...`.

The CDN resource configuration also contains `origin.aws`, but those credentials are for CDN origin reads. Do not use them for uploads.

## Object URL style

Prefer clean root-level public URLs:

```text
https://media.catvideo.space/bakery-assistant.mp4
https://media.catvideo.space/bakery-assistant.jpg
```

Avoid exposing source/tool folder names like `kling` in public site URLs. Keep old objects in place unless explicitly asked to delete them.
