---
title: Investigating “Recommended Extensions” - Part 2
date: 2023-09-02 12:00:00 +0800
categories: [Browser]
tags: [firefox, privacy, extensions]     # TAG names should always be lowercase
toc: true
math: true
---
> I am not an expert in browser extensions.
{: .prompt-warning }

#  PocketTube: Youtube Subscription Manager [Version 15.6.4] - 17,000 users
PocketTube is an extension used to manage group subscriptions on youtube. As stated in its privacy policy, it that it uses Mixpixel for analytics tracking, however, the policy makes no mention of Sentry, which it also uses. [^footnote1] There are also many analytics, but they seem less geared to data collection and more towards premium feature payment. However, with more then 8 MB of seemingly obfuscated javascript code finding such analytics code is difficult.

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

However, with Sentry, more infomation could be collected, although there is no evidence to suggest this is ongoing. The extension author claims that this data is only used for preformce upgrades.

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
All in all, with such a massive size this extenion was quite hard to analyze, and it appears to load a sentry SDK which can be used for error tracking. However, the Sentry Vue documentation also states that it may be used to "capture the user and gain critical pieces of information that construct a unique identity". [^footnote2] At the very least, it pulls remote javascript, which violates the recommended extensions policy. 

[^footnote1]: [https://addons.mozilla.org/en-US/firefox/addon/youtube-subscription-groups/privacy/](https://addons.mozilla.org/en-US/firefox/addon/youtube-subscription-groups/privacy/)
[^footnote2]: [https://docs.sentry.io/platforms/javascript/guides/vue/](https://docs.sentry.io/platforms/javascript/guides/vue/)
