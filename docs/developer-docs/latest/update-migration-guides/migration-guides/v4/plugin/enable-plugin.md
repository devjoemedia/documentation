---
title: v4 plugin migration - Enable a plugin - Strapi Developer Docs
description:
canonicalUrl:
prev: /developer-docs/latest/update-migration-guides/migration-guides/v4/plugin-migration.md
---

<!-- TODO: update SEO -->

# v4 plugin migration: Enable a plugin

!!!include(developer-docs/latest/update-migration-guides/migration-guides/v4/snippets/plugin-migration-intro.md)!!!

<br/>

::: callout
A Strapi v3 plugin was enabled if it was manually installed or found in the `plugins` directory.

In Strapi v4:

- Installed plugins following the [automatic plugins discovery](/developer-docs/latest/plugins/plugins-intro.md#automatic-plugins-discovery) pattern will automatically be enabled.
- While developing a local plugin, the plugin must explicitly be enabled in [the `./config/plugins.js` file](/developer-docs/latest/setup-deployment-guides/configurations/optional/plugins.md) of the Strapi application.
:::

Enabling a local plugin in v4 and defining an optional configuration should be done manually with the following procedure:

1. Create the `./config/plugins.js` file if it does not already exist. This JavaScript file should export a function that returns an object and can take the `{ env }` object as a parameter (see [Environment configuration](/developer-docs/latest/setup-deployment-guides/configurations/optional/environment.md) documentation).
2. Within the object exported by `./config/plugins.js`, create a key with the name of the plugin (e.g. `"my-plugin"`). The value of this key is also an object.
3. Within the `"my-plugin"` object, set the `enabled` key value to `true` (boolean).
4. _(optional)_ Add a `resolve` key, whose value is the path of the plugin folder (as a string), and a `config` key (as an object) that can include additional configuration for the plugin (see [plugins configuration](/developer-docs/latest/setup-deployment-guides/configurations/optional/plugins.md) documentation).

::: details Example: Enabling and configuring a "my-plugin" plugin

```js
// path: ./config/plugins.js

module.exports = ({ env }) => ({
  "my-plugin": {
    enabled: true,
    resolve: "./path-to-my-plugin",
    config: {
      // additional configuration goes here
    },
  },
});
```

:::

:::note Plugins published on npm
If the plugin will be published on npm, the `package.json` file should include a `strapi.kind` key with a value set to `"plugin"` (i.e. `{ "strapi": { "kind": "plugin" } }`).
:::
