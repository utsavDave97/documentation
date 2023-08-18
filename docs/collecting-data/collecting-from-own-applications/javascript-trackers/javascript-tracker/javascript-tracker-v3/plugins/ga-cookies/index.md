---
title: "GA Cookies"
date: "2021-03-30"
sidebar_position: 10000
---

```mdx-code-block
import Block5966 from "@site/docs/reusable/javascript-tracker-release-badge-v3/_index.md"

<Block5966/>
```

| Tracker Distribution | Included |
| --- | --- |
| `sp.js` | ✅ |
| `sp.lite.js` | ❌ |

With the GA Cookies plugin enabled the tracker will, by default, look for Google Analytics cookies (specifically the `__utma`, `__utmb`, `__utmc`, `__utmv`, `__utmz`, and `_ga` cookies) and combine their values into an event context which gets sent with every event.

The plugin can also be configured to collect Google Analytics 4 session and user identifiers.

:::tip
Google Analytics 4 cookies context and plugin options are available from v3.15
:::

## Download

<table class="has-fixed-layout"><tbody><tr><td>Download from GitHub Releases (Recommended)</td><td><a href="https://github.com/snowplow/snowplow-javascript-tracker/releases" target="_blank" rel="noreferrer noopener">Github Releases (plugins.umd.zip)</a></td></tr><tr><td>Available on jsDelivr</td><td><a href="https://cdn.jsdelivr.net/npm/@snowplow/browser-plugin-ga-cookies@latest/dist/index.umd.min.js" target="_blank" rel="noreferrer noopener">jsDelivr</a> (latest)</td></tr><tr><td>Available on unpkg</td><td><a href="https://unpkg.com/@snowplow/browser-plugin-ga-cookies@latest/dist/index.umd.min.js" target="_blank" rel="noreferrer noopener">unpkg</a> (latest)</td></tr></tbody></table>

**Note:** The links to the CDNs above point to the current latest version. You should pin to a specific version when integrating this plugin on your website if you are using a third party CDN in production.

## Initialization

```javascript
window.snowplow('addPlugin', 
  "https://cdn.jsdelivr.net/npm/@snowplow/browser-plugin-ga-cookies@latest/dist/index.umd.min.js",
  ["snowplowGaCookies", "GaCookiesPlugin"]
);
```

## Plugin options

The GA cookies plugin can be initialized with a couple of options allowing for customizing its behaviour:

| Option | Type | Description | Default value |
| :--------------:| :------: | :----------------------------------------------------------------------------------------------------------------: | :------: |
| ua | `boolean` | Should the plugin collect available Universal Analytics cookies. | `true` |
| ga4 | `boolean` | Should the plugin collect available Google Analytics 4 cookies. | `false` |
| ga4MeasurementId | `string | string[]` | The Google Analytics 4 measurement ID/s the plugin should collect session cookie values. If not provided, the plugin will only collect Google Analytics 4 user identifier cookies (_\_ga_).  | `''` |
| cookiePrefix | `string | string[]` | Cookie prefix/es set on the Google Analytics 4 cookies using the [cookie_prefix](https://developers.google.com/tag-platform/devguides/cookies#rename_cookies) option of the gtag.js tracker. For each prefix, a new Google Analytics 4 cookies context is attached. _The tracker will by default try to collect any non-prefixed user and session cookies automatically_. | `[]` |

### Context

Adding this plugin will automatically capture the following context:

| Context | Example |
| --- | --- |
| [iglu:com.google.analytics/cookies/jsonschema/1-0-0](https://github.com/snowplow/iglu-central/blob/master/schemas/com.google.analytics/cookies/jsonschema/1-0-0) | ![](images/Screenshot-2021-03-30-at-22.12.03.png) |

By adding the `{ ga: true }` option, the plugin will capture the following context:

| Context  |
| ---  |
| [iglu:com.google.ga4/cookies/jsonschema/1-0-0](https://github.com/snowplow/iglu-central/blob/master/schemas/com.google.ga4/cookies/jsonschema/1-0-0) |
