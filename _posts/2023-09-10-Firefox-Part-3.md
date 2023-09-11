---
title: Investigating “Recommended Extensions” - Part 3 
date: 2023-09-10 12:00:00 +0800
categories: [Technology, Browser]
tags: [firefox, privacy, security]     # TAG names should always be lowercase
toc: true
math: true
---

# Thoughts on Recommended Extensions
My findings about the Recommended Extensions in Firefox is that the program is good in theory, but has serious flaws in execution and policy. The program appears to have lax examination procedures and ineffective policies which provide a false sense of security for Firefox users. 

## Policy Problems: No requirement to allow examination of code
   Extensions can use a custom licence or end user agreement which has consumer limiting terms that prevent the examination of source code. It's very hard to find malicious code if the user is prevented from searching for such code.  Furthermore, for Firefox to claim that recommended extensions have the “highest standards of security” is dubious, since exposing or even investigating malicious code can come with risks of financial and legal repercussions.
  For example, Enhancer for YouTube has a licence that states "nobody has the right to review the Source Code" and that "nobody has the right to reverse-engineer" while promising legal action should the terms be violated. If malicious code was found in an investigation, I wouldn't feel comfortable reporting it for fear of legal issues.
  This is very concerning considering the various complaints about ads:

+ "This extension ... includ[es] advertisements." - hmm 
+ "Adware in a Recommended extension is absolutely UNACCEPTABLE, especially since you can't adblock elements in a settings page. This is malware-like behavior." - Psythik 
+ "When the add-on is automatically updated it presents a popup on every single youtube tab until they're refreshed. This popup does not go away, and cannot be closed easily." - Firefox user 15163168
+ "Abuses user trust by inserting ads in the settings and opening the ad-on settings page *without user interaction*. Unacceptable. Recommended label needs to be removed."  - Firefox user 17092397
+ "Instantly removing due to inclusion of pop up ads. How in the hell are you going to have an app that removes YT ads then hits you with its own popup ads?" - Scott347
+ "Whenever you open Firefox, Enhancer for YouTube™ sets a youtube.com cookie." - Firefox user 16930958,

The developers asseration that if there was "do not collect data of any sort, and they do not inject ads" and that if they did the extension would "be rejected" is worthless, as the review team misses the most basic of code injection and analytics. 

Recommended extensions should be held to the highest standards. Users should be allowed to search for malware, adware and spyware without worrying about legal consequences.

## Extension Examination Failures
- Search for common terms
  + 
## Communication Failures 

# Afterword
Overall, I'm disappointed in Mozilla. Not so much for the failures to catch remote code and hidden analytics, but rather the willing misrepresentation of the security the certification process provides. It's certainly not as bad as the 'Featured' extensions on Chrome, but I expected better. While the vast majority of the Recommended Extensions are privacy and security respecting, this is more likely to be a result of the open source community keeping extensions honest. The abject failure to catch even the most obvious of violations does not inspire confidence.

https://addons.mozilla.org/en-US/firefox/addon/enhancer-for-youtube/reviews/?score=1
https://www.mrfdev.com/privacy
