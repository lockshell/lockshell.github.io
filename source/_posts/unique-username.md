---
title: "找到独一无二的用户名"
description: "find unique Username,python,spider,网名"
date: "2019-08-12T11:37:28+08:00"
thumbnail: ""
categories:
  - "开发工具"
tags:
  - "Python"
---

很多朋友想要申请一个独一无二的个性用户名/网名，但是自己想好的名称总容易跟别人的冲突；要么是A网站不冲突，在B网站冲突了。

那么有没有方法一次性找出某个用户名，在所有常见社交网站、论坛的注册情况呢？

万能的Github已经有人为我们提供了方便的工具，那就是[sherlock](https://github.com/sherlock-project/sherlock)。

sherlock是一个用Python编写的爬虫工具，通过社交网络上的用户名搜索社交媒体帐户。

## 安装

```bash
# clone the repo
$ git clone https://github.com/sherlock-project/sherlock.git

# change the working directory to sherlock
$ cd sherlock

# install python3 and python3-pip if they are not installed

# install the requirements
$ python3 -m pip install -r requirements.txt
```

## 查找示例

查找单个用户:
```
python3 sherlock.py user123
```

查询多个用户:
```
python3 sherlock.py user1 user2 user3
```

<p align="center">
<img src="https://raw.githubusercontent.com/sherlock-project/sherlock/master/images/sherlock_preview.gif"/>
</p>


## 结果示例

比如运行`python sherlock.py  python` 来查找`python`这个用户名的注册结果。

```
[*] Checking username python on:
[-] ResearchGate: Illegal Username Format For This Site!
[+] 500px: https://500px.com/python
[+] 9GAG: https://9gag.com/u/python
[+] About.me: https://about.me/python
[-] Academia.edu: Not Found!
[-] AngelList: Not Found!
[+] Anobii: https://www.anobii.com/python/profile
[+] Aptoide: https://python.en.aptoide.com/
[+] Archive.org: https://archive.org/details/@python
[+] AskFM: https://ask.fm/python
[+] BLIP.fm: https://blip.fm/python
[+] Badoo: https://badoo.com/profile/python
[+] Bandcamp: https://www.bandcamp.com/python
[+] Basecamp: https://python.basecamphq.com
[+] Behance: https://www.behance.net/python
[+] BitBucket: https://bitbucket.org/python/
[-] BitCoinForum: Not Found!
[+] Blogger: https://python.blogspot.com
[-] Brew: Not Found!
[-] BuyMeACoffee: Not Found!
[-] BuzzFeed: Not Found!
[+] Canva: https://www.canva.com/python
[+] Carbonmade: https://python.carbonmade.com
[+] CashMe: https://cash.me/python
[-] Cent: Not Found!
[+] Cloob: https://www.cloob.com/name/python
[+] Codecademy: https://www.codecademy.com/python
[+] Codechef: https://www.codechef.com/users/python
[-] Codementor: Not Found!
[-] Codepen: Not Found!
[-] Coderwall: Not Found!
[+] Codewars: https://www.codewars.com/users/python
[+] ColourLovers: https://www.colourlovers.com/lover/python
[-] Contently: Not Found!
[-] Coroflot: Not Found!
[+] CreativeMarket: https://creativemarket.com/python
[-] Crevado: Not Found!
[+] Crunchyroll: https://www.crunchyroll.com/user/python
[-] DEV Community: Not Found!
[+] DailyMotion: https://www.dailymotion.com/python
[-] Designspiration: Not Found!
[-] DeviantART: Not Found!
[+] Discogs: https://www.discogs.com/user/python
[+] Disqus: https://disqus.com/python
[+] Docker Hub: https://hub.docker.com/u/python/
[+] Dribbble: https://dribbble.com/python
[+] EVE Online: https://evewho.com/pilot/python/
[+] Ebay: https://www.ebay.com/usr/python
[+] Ello: https://ello.co/python
[-] Etsy: Not Found!
[+] EyeEm: https://www.eyeem.com/u/python
[-] Facebook: Not Found!
[-] Fandom: Not Found!
[-] Filmogs: Not Found!
[+] Flickr: https://www.flickr.com/people/python
[-] Flightradar24: Not Found!
[+] Flipboard: https://flipboard.com/@python
[-] Foursquare: Not Found!
[+] Giphy: https://giphy.com/python
[+] GitHub: https://www.github.com/python
[-] GitLab: Not Found!
[+] Gitee: https://gitee.com/python
[+] GoodReads: https://www.goodreads.com/python
[+] Gravatar: http://en.gravatar.com/python
[-] Gumroad: Not Found!
[-] HackerNews: Not Found!
[+] HackerOne: https://hackerone.com/python
[+] HackerRank: https://hackerrank.com/python
[+] House-Mixes.com: https://www.house-mixes.com/profile/python
[+] Houzz: https://houzz.com/user/python
[+] HubPages: https://hubpages.com/@python
[+] IFTTT: https://www.ifttt.com/p/python
[+] ImageShack: https://imageshack.us/user/python
[+] Imgur: https://imgur.com/user/python
[+] Instagram: https://www.instagram.com/python
[+] Instructables: https://www.instructables.com/member/python
[-] Investing.com: Not Found!
[+] Issuu: https://issuu.com/python
[+] Itch.io: https://python.itch.io/
[-] Jimdo: Not Found!
[-] Kaggle: Not Found!
[+] KanoWorld: https://api.kano.me/progress/user/python
[-] Keybase: Not Found!
[+] Kik: https://ws2.kik.com/user/python
[+] Kongregate: https://www.kongregate.com/accounts/python
[+] Launchpad: https://launchpad.net/~python
[+] LeetCode: https://leetcode.com/python
[-] Letterboxd: Not Found!
[+] LiveJournal: https://python.livejournal.com
[-] Mastodon: Not Found!
[+] Medium: https://medium.com/@python
[+] MeetMe: https://www.meetme.com/python
[+] MixCloud: https://www.mixcloud.com/python/
[+] MyAnimeList: https://myanimelist.net/profile/python
[+] Myspace: https://myspace.com/python
[+] NPM: https://www.npmjs.com/~python
[+] NPM-Package: https://www.npmjs.com/package/python
[+] NameMC (Minecraft.net skins): https://namemc.com/profile/python
[-] NationStates Nation: Not Found!
[-] NationStates Region: Not Found!
[+] Newgrounds: https://python.newgrounds.com
[-] OK: Not Found!
[-] OpenCollective: Not Found!
[-] Packagist: Not Found!
[+] Pastebin: https://pastebin.com/u/python
[+] Patreon: https://www.patreon.com/python
[+] PayPal: https://www.paypal.me/python
[-] Pexels: Not Found!
[+] Photobucket: https://photobucket.com/user/python/library
[+] Pinterest: https://www.pinterest.com/python/
[+] Pixabay: https://pixabay.com/en/users/python
[-] PlayStore: Not Found!
[-] Plug.DJ: Not Found!
[+] Pokemon Showdown: https://pokemonshowdown.com/users/python
[-] ProductHunt: Not Found!
[-] Quora: Not Found!
[+] Rajce.net: https://python.rajce.idnes.cz/
[+] Rate Your Music: https://rateyourmusic.com/~python
[+] Reddit: https://www.reddit.com/user/python
[+] Repl.it: https://repl.it/@python
[-] ReverbNation: Not Found!
[-] Roblox: Not Found!
[+] Scratch: https://scratch.mit.edu/users/python
[+] Scribd: https://www.scribd.com/python
[-] Signal: Not Found!
[+] Slack: https://python.slack.com
[+] SlideShare: https://slideshare.net/python
[-] Smashcast: Not Found!
[+] SoundCloud: https://soundcloud.com/python
[+] SourceForge: https://sourceforge.net/u/python
[+] Speedrun.com: https://speedrun.com/user/python
[-] Splits.io: Not Found!
[+] Spotify: https://open.spotify.com/user/python
[+] Star Citizen: https://robertsspaceindustries.com/citizens/python
[+] Steam: https://steamcommunity.com/id/python
[+] SteamGroup: https://steamcommunity.com/groups/python
[+] Taringa: https://www.taringa.net/python
[+] Telegram: https://t.me/python
[+] TikTok: https://www.tiktok.com/@python
[+] Tinder: https://www.gotinder.com/@python
[-] TradingView: Not Found!
[+] Trakt: https://www.trakt.tv/users/python
[-] Trello: Not Found!
[-] Trip: Not Found!
[+] TripAdvisor: https://tripadvisor.com/members/python
[+] Twitch: https://m.twitch.tv/python
[+] Twitter: https://www.twitter.com/python
[+] Unsplash: https://unsplash.com/@python
[+] VK: https://vk.com/python
[+] VSCO: https://vsco.co/python
[+] Venmo: https://venmo.com/python
[+] Vimeo: https://vimeo.com/python
[+] Virgool: https://virgool.io/@python
[-] VirusTotal: Not Found!
[+] Wattpad: https://www.wattpad.com/user/python
[+] We Heart It: https://weheartit.com/python
[+] WebNode: https://python.webnode.cz/
[-] Wikipedia: Not Found!
[-] Wix: Not Found!
[+] WordPress: https://python.wordpress.com/
[+] WordPressOrg: https://profiles.wordpress.org/python/
[+] YouNow: https://www.younow.com/python/
[-] YouPic: Not Found!
[-] YouTube: Not Found!
[+] Zhihu: https://www.zhihu.com/people/python
[+] authorSTREAM: http://www.authorstream.com/python/
[-] boingboing.net: Not Found!
[+] devRant: https://devrant.com/users/python
[+] gfycat: https://gfycat.com/@python
[+] iMGSRC.RU: https://imgsrc.ru/main/user.php?user=python
[+] last.fm: https://last.fm/user/python
[+] mixer.com: https://mixer.com/python
[+] osu!: https://osu.ppy.sh/users/python

```
