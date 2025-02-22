---
connections: 
tags:
  - permanent_note
type: permanent_note
created: 2025-02-19 22:15
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

In the last year my personal infrastructure has changed a lot from reading lots of books and blogs about individual's productive life. With this post I want to start a bi-annual series to track changes in how my approach to productivity, technology, and knowledge management is shifting, and what’s working (or not), inspired by [Elliot Clowes](http://elliotclowes.com/)'s [I'm Left Handed](https://imlefthanded.com/2025/the-tech-that-powers-my-life-2025-edition/). 

---

My personal setup has two machines: a 2020 Macbook Air M1 and a custom build Windows from 2019. I hate Windows and I wouldn't want to spend any time on it. It's slow, bloated with legacy features, a mess to work with, now it's introducing AI features that nobody wants, BUT... it runs games. This PC is mainly used for gaming, it's equipped with an AMD Ryzen 2700, an Nvidia RTX 2060, 8 Gb of ram, too much hard disk space and too few ssd space. It's beginning to show its age with modern games, but Marvel Rivals and Minecraft (the two games I am playing now) still run so I'm not in a rush to upgrade it. 
On the other hand, I love my Macbook. It was my first purchase going into university and also my first ever Apple product. Even though it was a new architecture, the launch was not traumatic, some compatibility issue here and there, some memory leaks, but Rosetta was quite a spectacular piece of software. Some MacOs features are frustrating, but extensions feel some gaps, like [Rectangle](https://rectangleapp.com/), for moving, snapping and resizing windows, [battery](https://github.com/actuallymentor/battery#readme), because when I'm in dock mode I want to limit the battery charge to avoid heating my usb-c hub, [f.lux](https://justgetflux.com/news/pages/macquickstart/), [amphetamine](https://apps.apple.com/it/app/amphetamine/id937984704) and others. 

As peripherals I recently bought a Keychron K8 with Gateron Pro Red switches, which I'm loving, and a wired Logitech G502 mouse. The only downside of the mouse is the fact that being wired I had to buy a KVM switch to use it in both machines. 
I have two monitors, a 27 inch Samsung curved display and a repurposed 24 inch LG TV as a second screen. On top of the first monitor, I recently bought a lightbar, which seems a gimmick, but actually improved my eye fatigue during night and plus lights up the workspace really well. 
Some other miscellaneous stuff include:
- [A beautiful deksmat](https://keygem.com/products/gestalt-keycap-pre-order?variant=45402118881548)
- [Charging station](https://amzn.eu/d/3CMIYia) for all my mobile devices
- An old android phone reused as a digital clock plus elgato stream deck alternative with [WebDeck ](https://github.com/Lenochxd/WebDeck). Unfortunately it only supports Windows. I also set up an automation to open the webdeck local ip whenever the PC boots up.
- a 1996 stereo system from Technics

As a browser in MacOs I mainly use [Arc](https://arc.net/gift/3dfaa55), a Chromium-based browser developed by the Browser company. It has many cool features, but the main selling points to me are the vertical bar with easier to see spaces and PIP view when switching tabs. Also hovering on the gmail shortcut to see a sneak peek of the inbox is cool. On windows I feel like it is not stable enough yet, so I tend to use Chrome a lot more. There's also a mobile app that has an AI-augmented search called Search for Me. I don't use this feature often, but the mobile app is stable and works well, minus the lack of extensions due to Apple policy. Speaking about extensions on PC there are all Chrome extensions, since Arc is based on Chromium. My go-to are:
- [Obsidian Web Clipper](https://chromewebstore.google.com/detail/obsidian-web-clipper/cnjifjpddelmedmihgijeibhnjfabmlf), to save websites in Obsidian. I don't use it very often.
- [Keepa](https://chromewebstore.google.com/detail/keepa-amazon-price-tracke/neebplgakaahbhdphmkckjjcegoiijjo), to see amazon price history charts
- [Privacy Badger](https://chromewebstore.google.com/detail/privacy-badger/pkehgijcmpdhfbdbbnkijodmdjhbjlgp), which blocks invisible trackers
- [SponsorBlock for Youtube](https://chromewebstore.google.com/detail/sponsorblock-per-youtube/mnjggcdmjocbbbhaepdhchncahnbgone), crowdsourced extension to skip promotions and sponsored segments
- [Zotero Connector](https://chromewebstore.google.com/detail/zotero-connector/ekhagklcjbdpajgpjgmbionohlpdbjgc), saves references to Zotero
- [uBlock Origin](https://chromewebstore.google.com/detail/ublock/epcnnfbjfcgphgdmggkamkmgojdagdnn), Ad block
- [Shut Up](https://chromewebstore.google.com/detail/shut-up-comment-blocker/oklfoejikkmejobodofaimigojomlfim), removes comments to all websites

For my productive life, I tend to follow the teachings of [[How to Take Smart Notes - Sönke Ahrens]] for when I don't have any too specific tasks. With this mindset, I keep every note in [Obsidian](https://obsidian.md/), that helps me follow the Zettelkasten principles. I settled to Obsidian after switching different note taking apps, from pure Latex, where I was spending more time to fix things rather than actual writing, to Notion, the last note taking app I used before Obsidian. I switched from Notion for two main reasons:
- I don't like the cloud approach of Notion, keeping every note with their proprietary format. This was not future-proof enough for me and I didn't actually own my notes. Instead Obsidian takes a local-first approach, with its cloud servers being a monthly 5$ add-on, and uses markdown, so even if I decide to change app or Obsidian shuts down I can still read all my notes without problems. 
- the second reason is the high customizability, with endless community plugins. I am not ashamed to admit I spent countless hours trying different plugins, setups and approaches. I finally settled for this [PARA+Zettelkasten vault template](https://github.com/DuskWasHere/dusk-obsidian-vault) which is amazing.
For tasks, I use the classic [Todoist](https://www.todoist.com/it) synced with Google calendar. I don't have any special configurations for todo lists organization, I'm still experimenting with it. 

At home I also keep an old PC tower repurposed as a server. I mounted Ubuntu server and I host some basic services like [Jellyfin](https://jellyfin.org/), [Home Assistant](https://www.home-assistant.io/) and [NextCloud](https://nextcloud.com/). To access the server remotely instead of opening ports to the internet, I use [Tailscale](https://tailscale.com/), which allows to create private networking with stupidly easy setup. I even hosted a Minecraft server to play with my friends and Tailscale made it easy to share the machine. 

--- 

That's about it. It’s not as impressive as some other setups I’ve seen, but it works for me—for now. I’ve left out many smaller tools that aren’t as essential to mention. Inspired by Elliot, I’d encourage others to document their own digital lives as well.