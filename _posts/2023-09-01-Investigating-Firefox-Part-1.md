---
title: Investigating “Recommended Extensions” -  Part 1
date: 2023-09-01 12:00:00 +0800
categories: [Browser]
tags: [firefox, privacy]     # TAG names should always be lowercase
toc: true
math: true
---
# Introduction
Recently, investigations of Google Chrome extensions have uncovered malware, spyware and adware in dozens of popular extensions used by millions of users.[^footnote] Although there was considerable criticism of Google’s review process for these extensions, I did not observe much curiosity directed towards the state of Firefox extensions. As a devout Firefox user, albeit one who only uses open-source extensions, I was inspired by a comment on YCombinator (Hacker News) by Krono to look into some popular extensions to compare Mozilla against Google.[^footnote2]
	
# Recommended Extensions
Mozilla’s “Recommended Extensions” program claims to certify that select extensions have the “highest standards of security, functionality, and user experience” which is done by “thoroughly evaluat[ing] each extension”.[^footnote3] Furthermore, they must abide by the extension standards, which you can read [here](https://extensionworkshop.com/documentation/publish/add-on-policies/), but in summary, extensions must:
1. Not have remote code;
2. Not use Google Analytics JavaScript, only the API;
3. Only collect relevant data to function;
4. Provide a privacy policy and ability to opt-out of data collection;
5. Must be actively maintained (recommended extensions only).

Seems fair, right? Well, a quick look into some of Mozilla’s “Recommended Extensions” finds that many extensions are not following these rules, and that Mozilla has failed to catch these violations. Lets take a look at some examples.

# Giphy [Version 3.1] – 7,000 users

This extension – produced by giphy.com – is used to load GIFs which can be sent in “emails, tweets and more”.[^footnote4] Users can search for a GIF and then drag and drop it into the message. Despite not being updated since 2021, it is still a recommended extension. Furthermore, although it has no privacy policy, which suggests that the extension author does not collect analytics, the extension includes an analytics.ts file, which when decompiled, yields: 

```
;(function(i, s, o, g, r, a, m) {
  i['GoogleAnalyticsObject'] = r;
  i[r] = i[r] || function() {
    (i[r].q = i[r].q || []).push(arguments);
  };
  i[r].l = 1 * new Date();
  a = s.createElement(o);
  m = s.getElementsByTagName(o)[0];
  a.async = 1;
  a.src = g;
  m.parentNode.insertBefore(a, m);
})(window, document, 'script', 'https://www.google-analytics.com/analytics.js', 'ga');
```

This loads an analytics javascript, which can collect the IP Addresses, user agents, page views, user engagement (time spent/website, interactions,) events (button clicks, video views) and referral sources of users. There is no option to opt-out of this, or even an indication that such information collection is ongoing. This extensions appears to violate most of the recommended extension rules.

[Read Part 2 here.](https://www.coloursofosint.com/posts/Investigating-Firefox-Part-2/)

[^footnote]: [https://palant.info/2023/05/31/more-malicious-extensions-in-chrome-web-store/](https://palant.info/2023/05/31/more-malicious-extensions-in-chrome-web-store/)
[^footnote2]: [https://news.ycombinator.com/item?id=37137552](https://news.ycombinator.com/item?id=37137552)
[^footnote3]: [https://extensionworkshop.com/documentation/publish/recommended-extensions/](https://extensionworkshop.com/documentation/publish/recommended-extensions/)
[^footnote4]: [https://addons.mozilla.org/en-US/firefox/addon/giphy-for-firefox/](https://addons.mozilla.org/en-US/firefox/addon/giphy-for-firefox/)
