# Renovate Config

## How to use in a project

Create a `.renovaterc.json` file in the root folder of your project and add:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["local>4s1/renovate-config"]
}
```

## How to configure service

I've created two files, `config.js` and `start.sh`. \
A cronjob starts the Renovate Bot service every 3 hours between 7 and 21 o'clock. \
`0 7-21/3 * * * cd ~/renovate-bot && ./start.sh`

### config.js

```js
module.exports = {
  onboardingConfig: {
    extends: ['config:base'],
  },
  autodiscoverFilter: '4s1/**',
  labels: ['renovate'],
}
```

### start.sh

`BOT_AUTHOR_INFO` like "Foo <foo@bar.de>". \
`BOT_GITLAB_TOKEN` with the following settings:

- api
- read_user
- write_repository

`BOT_GITLAB_TOKEN` with no special settings, just an API key to increase the rate limit against github.com for fetching the changelogs.

```bash
docker run \
  --rm \
  -v ${PWD}/config.js:/usr/src/app/config.js \
  -e RENOVATE_ENDPOINT="https://gitlab.com/api/v4/" \
  -e RENOVATE_AUTODISCOVER="true" \
  -e RENOVATE_TOKEN="<BOT_GITLAB_TOKEN>" \
  -e RENOVATE_PLATFORM="gitlab" \
  -e RENOVATE_GIT_AUTHOR="<BOT_AUTHOR_INFO>" \
  -e GITHUB_COM_TOKEN="<BOT_GITHUB_TOKEN>" \
  -e LOG_LEVEL=debug \
  renovate/renovate \
  > "$(date +"%Y-%m-%d_%H-%M-%S").log"
```
