# Renovate Config

## How to use

Create a `.renovaterc.json` file in root folder and add:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["gitlab>YellowGarbageGroup/renovate-config"]
}
```

Add the project to you underlying `config.js` where the renovate bot is running.
