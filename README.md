# Renovate Config

## How to use in a project

Create a `.renovaterc.json` file in the root folder of your project and add:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["local>4s1-org/renovate-config"]
}
```

## How to start service

Let RenovateBot run:

```bash
docker run \
  --rm \
  -v ${PWD}/config.js:/usr/src/app/config.js \
  -e RENOVATE_AUTODISCOVER="true" \
  -e RENOVATE_AUTODISCOVER_FILTER="4s1-org/**" \
  -e RENOVATE_TOKEN="<GITHUB_TOKEN>" \
  -e LOG_LEVEL=debug \
  renovate/renovate \
  > "$(date +"%Y-%m-%d_%H-%M-%S").log"
```

`GITHUB_TOKEN` with the following settings:

- api
