---
title: Investigating “Recommended Extensions” - Part 2
date: 2023-09-03 12:00:00 +0800
categories: [Technology, Browser]
tags: [firefox, privacy, extensions]     # TAG names should always be lowercase
toc: true
math: true
---

#  PocketTube: Youtube Subscription Manager [Version 15.6.4] - 17,000 users
## Introduction

![Image](https://raw.githubusercontent.com/ColoursofOSINT/ColoursofOSINT.github.io/master/assets/img/images/firefox/Screenshot%202023-09-08%20at%2010.21.40%20AM.png)

PocketTube is an extension used to manage group subscriptions on youtube. As stated in its privacy policy, it that it uses Mixpixel for analytics tracking, however, the policy makes no mention of Sentry, which it also uses.[^footnote1] However, with more then 8 MB of seemingly obfuscated javascript code finding such analytics code was difficult.

## Privacy Policy
The extension author claims that any data collected will "not sold to third parties". Furthermore, the policy claims to use Mixpanel and that the author may "gather and log data on how our users access and use".[^footnote1]

## Part 1 - Disclosed Code
There are many analytics, but they seem less geared to data collection and more towards premium feature payment.

```
var be = "https://api.mixpanel.com";
var ke = {};

function we(e, t, n, i) {
  ke.token = e;
  ke.distinct_id = t;
  ke.lang = n;
```

However, with the Sentry SDK, more infomation could be collected, although there is no evidence to suggest this is ongoing. The extension author claims that this data is only used for preformance upgrades.

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
## Part 2 - Suspicious Code
Continuing my search, I began to find some code that appeared suspicious.

```
 {
 key: 'setupAnalytics',
 value: function(e, t) {
     var n = new URL(location.href).searchParams,
    i = n.get('lang')
      je.init(
      '94714e302802e9b5b7216b239f268116',
     e,
    null === i ? 'en' : i.substring(0, 2),
 t
 )
n.get('view-version')
 }
 },
```

This code appear to "setupAnalytics", but upon further examination, I couldn't find anything that appeared blatantly suspect.

## Part 3 - Undiscolsed Analytics and Javascript Injection
After a significant amount of searching, the following code was found.

```
return c = document.createElement("script");
c.type = "text/javascript";
c.async = !0;
c.id = "profitwell-js";
c.dataset.pwAuth = "d9e7cc8d6ed29daf6d6bf94d3fbfa915";
d = document.querySelector("html").getAttribute("ysm-email");
c.text = "(function(i, s, o, g, r, a, m) {
  i[o] = i[o] || function() {
    (i[o].q = i[o].q || []).push(arguments);
  };
  a = s.createElement(g);
  m = s.getElementsByTagName(g)[0];
  a.async = 1;
  a.src = r + '?auth=' + s.getElementById(o + '-js').getAttribute('data-pw-auth');
  m.parentNode.insertBefore(a, m);
})(window, document, 'profitwell', 'script', 'https://public.profitwell.com/js/profitwell.js');
profitwell('start', { 'user_email': '" + d + "' });
(document.head || document.documentElement).appendChild(c);
m["return"]();
if (!...

```
This fetches the user's email address from a HTML document (with the auth token of 'd9e7cc8d6ed29daf6d6bf94d3fbfa915'), then creates, injects and continuously runs the profitwell analytics javascript which initiates with the email of the user. There appears to be no way to opt-out of this injection and data collection.

All in all, with such a massive size this extension was quite hard to analyze, and it appears to load a sentry SDK which can be used for error tracking. However, the Sentry Vue documentation also states that it may be used to "capture the user and gain critical pieces of information that construct a unique identity".[^footnote2] With profitwell, remote javascript is loaded and injected for user analytics tied to a registered email. At the very least, it pulls remote javascript and does not allow the user to opt-out of non-necessary data collection, which is a clear violation of the recommended extensions policy.  


[^footnote1]: [https://addons.mozilla.org/en-US/firefox/addon/youtube-subscription-groups/privacy/](https://addons.mozilla.org/en-US/firefox/addon/youtube-subscription-groups/privacy/)
[^footnote2]: [https://docs.sentry.io/platforms/javascript/guides/vue/](https://docs.sentry.io/platforms/javascript/guides/vue/)
