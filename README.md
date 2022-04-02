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

Create a `config.js` and add the following settings:

```js
module.exports = {
  hostRules: [
    {
      // required for private packages
      hostType: "npm",
      matchHost: "https://gitlab.com/api/v4/packages/npm/",
      token: process.env.RENOVATE_TOKEN,
    },
  ],
};
```

Let RenovateBot run:

```bash
docker run \
  --rm \
  -v ${PWD}/config.js:/usr/src/app/config.js \
  -e RENOVATE_ENDPOINT="https://gitlab.com/api/v4/" \
  -e RENOVATE_PLATFORM="gitlab" \
  -e RENOVATE_AUTODISCOVER="true" \
  -e RENOVATE_AUTODISCOVER_FILTER="4s1/**" \
  -e RENOVATE_TOKEN="<BOT_GITLAB_TOKEN>" \
  -e GITHUB_COM_TOKEN="<BOT_GITHUB_TOKEN>" \
  -e LOG_LEVEL=debug \
  renovate/renovate \
  > "$(date +"%Y-%m-%d_%H-%M-%S").log"
```

`BOT_GITLAB_TOKEN` with the following settings:

- api
- read_user
- write_repository

`BOT_GITHUB_TOKEN` with no special settings, just an API key to increase the rate limit against github.com for fetching the changelogs.
