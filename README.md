# model-configs

Fallback mirror of the Taylor iOS app's on-device model configuration.

The app fetches its model configuration from these sources, in order:

1. `https://config.taylor-ai.info/models/production-config.json` (primary)
2. `https://backup-config.taylor-ai.info/models/production-config.json` (backup)
3. `https://raw.githubusercontent.com/Life-Altering-2/model-configs/main/models/production-config.json` (this repo)

The first two hosts sit behind the same CloudFront distribution, so this repo is
the independent fallback if that distribution is unreachable.

## Keep in sync

`models/production-config.json` here must stay **byte-identical** to
`https://config.taylor-ai.info/models/production-config.json`. Whenever you
publish a new config to the primary, commit the same bytes here on `main` in
the same change. Check with:

```bash
diff <(curl -sS https://config.taylor-ai.info/models/production-config.json) \
     <(curl -sS https://raw.githubusercontent.com/Life-Altering-2/model-configs/main/models/production-config.json)
```

This repo is public. Never commit secrets, tokens, internal URLs or personal
data. The config only names public Hugging Face model repos and revisions.
