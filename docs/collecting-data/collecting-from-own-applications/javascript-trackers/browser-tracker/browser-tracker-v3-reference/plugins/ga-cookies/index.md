---
title: "GA Cookies"
date: "2021-04-07"
sidebar_position: 10000
---

```mdx-code-block
import Block5966 from "@site/docs/reusable/javascript-tracker-release-badge-v3/_index.md"

<Block5966/>
```

With the GA Cookies plugin enabled the tracker will, by default, look for Google Analytics cookies (specifically the `__utma`, `__utmb`, `__utmc`, `__utmv`, `__utmz`, and `_ga` cookies) and combine their values into an event context which gets sent with every event.

The plugin can also be configured to collect Google Analytics 4 session and user identifiers.

:::tip
Google Analytics 4 cookies context and plugin options are available from v3.15
:::

## Installation

- `npm install @snowplow/browser-plugin-ga-cookies`
- `yarn add @snowplow/browser-plugin-ga-cookies`
- `pnpm add @snowplow/browser-plugin-ga-cookies`

## Initialization

```javascript
import { newTracker, trackPageView } from '@snowplow/browser-tracker';
import { GaCookiesPlugin } from '@snowplow/browser-plugin-ga-cookies';

newTracker('sp1', '{{collector_url}}', { 
   appId: 'my-app-id', 
   plugins: [ GaCookiesPlugin() ],
});
```

## Plugin options

The GA cookies plugin can be initialized with a couple of options allowing for customizing its behaviour:

| Option | Type | Description | Default value |
| :--------------:| :------: | :----------------------------------------------------------------------------------------------------------------: | :------: |
| ua | `boolean` | Should the plugin collect available Universal Analytics cookies. | `true` |
| ga4 | `boolean` | Should the plugin collect available Google Analytics 4 cookies. | `false` |
| ga4MeasurementId | `boolean` | The Google Analytics 4 measurement IDs the plugin should collect session cookie values. If not provided, the plugin will only collect Google Analytics 4 user identifier cookies (_\_ga_).  | `''` |
| cookiePrefix | `boolean` | Cookie prefix set on the Google Analytics 4 cookies using the [cookie_prefix](https://developers.google.com/tag-platform/devguides/cookies#rename_cookies) option of the gtag.js tracker. For each prefix, a new Google Analytics 4 cookies context is attached. _The tracker will by default try to collect any non-prefixed user and session cookies automatically_. | `[]` |

### Context

Adding this plugin will automatically capture the following context:

| Context                                                                                                                                                          | Example                                           |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|
| [iglu:com.google.analytics/cookies/jsonschema/1-0-0](https://github.com/snowplow/iglu-central/blob/master/schemas/com.google.analytics/cookies/jsonschema/1-0-0) | ![](images/Screenshot-2021-03-30-at-22.12.03.png) |

By adding the `{ ga: true }` option, the plugin will capture the following context:

| Context  |
| ---  |
| [iglu:com.google.ga4/cookies/jsonschema/1-0-0](https://github.com/snowplow/iglu-central/blob/master/schemas/com.google.ga4/cookies/jsonschema/1-0-0) |
