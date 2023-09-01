---
title: Investigating “Recommended Extensions” in Firefox - Part 2
date: 2023-09-01 12:00:00 +0800
categories: [Browser]
tags: [firefox, privacy, extensions]     # TAG names should always be lowercase
toc: true
math: true
---

#  PocketTube: Youtube Subscription Manager [Version 15.6.4] - 17,000 users
PocketTube is an extension used to manage group subscriptions on youtube. As stated in its privacy policy, it that it uses Mixpixel for analytics tracking, however, the policy makes no mention of Sentry, which it also uses. [^footnote`] There are also many analytics, but they seem less geared to data collection and more towards premium feature payment. Moreover, there may be more analytics, but with more then 8 MB of javascript code, finding such code is difficult.

```
var be = "https://api.mixpanel.com";
var ke = {};

function we(e, t, n, i) {
  ke.token = e;
  ke.distinct_id = t;
  ke.lang = n;
```

```
  } else if (e.menuItemId === "1115") {
    chrome.tabs.create({
      url: "https://www.youtube.com/channel/UCTVgSQTwWpHWIXC6EOh8vWw?sub_confirmation=1"
    }, function() {});

```

However, with Sentry, more infomation could be collected, although there is no evidence to suggest this is ongoing.

```
lC({
  Vue: o["default"],
  dsn: "https://0038060f1bc6428da18206617e79945a@o416359.ingest.sentry.io/5310804",
  integrations: [
    new a.BrowserTracing({

```

```
{
  "sdk": {
    "name": "sentry.javascript.vue",
    "packages": [
      {
        "name": "npm:@sentry/vue",
        "version": "wS"
      }
    ]
  }
}
```

[^footnote1]: https://addons.mozilla.org/en-US/firefox/addon/youtube-subscription-groups/privacy/
