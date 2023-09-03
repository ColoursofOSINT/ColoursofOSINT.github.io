---
title: Atlas VPN 0Day
date: 2023-09-03 12:00:00 +0800
categories: [VPN]
tags: [atlas vpn, privacy, exploit]     # TAG names should always be lowercase
toc: true
math: true
---

# Atlas VPN 
VPNs have seen a massive increase in usage in the last few years[^footnote1], with a popular provider 'Atlas VPN' reportedly gaining more than six million users before being bought out by Nord Security, owners of NordVPN [^footnote2]. NordVPN has been extensive criticized for false advertising,[^footnote3] as well as its response to a data breach in 2019 - in which private keys and root access were compromised - that the company took more than 18 months to reveal.[^footnote4]

It appears their inability to secure their services has occurred again.  

# The 0-Day
Two days ago, a throwaway account named ‘Educational-Map-8145’ (I’ll call them ‘EM8’) posted on the Cybersecurity subreddit posted what the user claimed to be a 0-day javascript code that after execution could disconnect the “AtlasVPN linux client and leak the users IP address”. [^footnote5] 

According to EM8, the AtlasVPN runs both a client and a daemon, and the client connects via “API on localhost on port 8076”. As any program can access localhost, including websites which connect via browser, the malicious javascript could be run in any website to cause the VPN to disconnect, exposing the real IP of the user. Fortunately, the code is “not intended for illegal purposes.”

# Conformation 
In a post from Chris Partridge on Mastodon the “hilarious[ly]” bad security is “utter garbage”. He included a video which appears to demonstrate the PoE for the dropped connection. [^footnote7]

[![PoE](https://media.infosec.exchange/infosecmediaeu/cache/media_attachments/files/110/997/661/288/787/693/original/a209c146534a35a3.mp4)]

[![PoE](https://raw.githubusercontent.com/ColoursofOSINT/ColoursofOSINT.github.io/master/assets/img/Videos/a209c146534a35a3.mp4)]


# AtlasVPN Response (or Lack Thereof)
In the original reddit post, EM8 claims they tried to contact AtlasVPN about the issue but received “no answer” and saw “[no] signs of a bug bounty programme”. In fact, the response was so lacking and the fact that the security “suck[ed] so massively” that they found it “hard to believe this is a bug rather than a backdoor”. Yikes.

Hopefully Atlas will fix the exploit with the same speed as NordVPN. So only 18 months to go.

[^footnote1]: [https://www.thevpnexperts.com/research/why-vpn-usage-is-on-the-surge/](https://www.thevpnexperts.com/research/why-vpn-usage-is-on-the-surge/)
[^footnote2]: [https://www.comparitech.com/vpn/reviews/atlas-vpn-review/](https://www.comparitech.com/vpn/reviews/atlas-vpn-review/)
[^footnote3]: [https://www.pcmag.com/news/nordvpn-ad-banned-for-exaggerating-threat-of-public-wi-fi](https://www.pcmag.com/news/nordvpn-ad-banned-for-exaggerating-threat-of-public-wi-fi)
[^footnote4]: [https://arstechnica.com/information-technology/2019/10/hackers-steal-secret-crypto-keys-for-nordvpn-heres-what-we-know-so-far/](https://arstechnica.com/information-technology/2019/10/hackers-steal-secret-crypto-keys-for-nordvpn-heres-what-we-know-so-far/)
[^footnote5]: [https://www.reddit.com/r/cybersecurity/comments/167f16e/atlasvpn_linux_client_103_remote_disconnect/](https://www.reddit.com/r/cybersecurity/comments/167f16e/atlasvpn_linux_client_103_remote_disconnect/)
[^footnote7]: [https://cybersecurity.theater/@tweedge/110997661135498890](https://cybersecurity.theater/@tweedge/110997661135498890)
