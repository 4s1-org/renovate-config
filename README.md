# Renovate Config

## How to use

Create a `.renovaterc.json` file in the root folder of your project and add:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["gitlab>YellowGarbageGroup/renovate-config"]
}
```

Add the project to you underlying `config.js` where the renovate bot is running.

## config.js

```js
module.exports = {
  endpoint: "https://gitlab.com/api/v4/",
  token: "<GITLAB-TOKEN>",
  platform: "gitlab",
  onboardingConfig: {
    extends: ["config:base"],
  },
  hostRules: [
    {
      hostType: "npm",
      matchHost: "https://gitlab.com/api/v4/packages/npm/",
      token: "<GITLAB-TOKEN>",
    },
  ],
  repositories: ["<PROJECT-1>", "<PROJECT-2>", "<PROJECT-n>"],
};
```

## Docker Container

```bash
docker run \
  --rm \
  -v ${PWD}/config.js:/usr/src/app/config.js \
  -e GITHUB_COM_TOKEN=<GITHUB-TOKEN> \
  -e LOG_LEVEL=info \
  renovate/renovate
```
