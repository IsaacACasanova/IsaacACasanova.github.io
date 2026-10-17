---
layout: post
title: For Myself, for Once
description: Two layoffs, twelve years of building other people's products, and why I'm building Compose.
date: 2026-10-02 09:00:00 -0400
tags: [personal, compose]
---

I haven't written here since September 2022. My last post was about dealing with uncertainty. I wrote it while Twitter's sale was still pending, and it's mostly a list of advice: log off, take care of yourself, control what you can. Reading it now, it sounds like someone trying to stay calm.

In 2023 I was laid off from Twitter. I went to Block and spent the next few years on Square's point of sale. This year I was laid off from Block too.

Two layoffs in three years taught me something I'd managed to avoid thinking about for most of my career. Both times, the decision had nothing to do with the work. And both times, the work stayed behind. For twelve years I'd built things that belonged to someone else, and they could decide at any point that I didn't belong to them anymore.

I'm proud of a lot of that work. But this time, I'm building something for myself.

# Compose

[Compose](https://composesocial.app) is an app for writing a post once and publishing it to Bluesky, Mastodon, Threads, and X. You connect your accounts, write in one composer, choose where it goes, and send. If one network needs different wording, you give it its own version. Before you post, Compose tells you which network your post won't fit and what to cut. Home shows everything you've published, with the engagement each network reports.

The people I follow are spread across four networks now. Posting to all of them meant pasting the same text into four apps, then fixing it four ways for four character limits. Compose is the app I wanted for that.

There's an iOS app, an Android app on the way, and a sync service so your history follows you between devices. Sync is end-to-end encrypted. The server stores data it can't read: no user table, no sign-up, no account ID. I've spent most of my career on apps that handle people's messages and money. This time I wanted to build one where I couldn't look at your data even if I wanted to.

# Doing it alone

This is the first time in twelve years nobody is handing me the work. Nobody sets the roadmap, nobody signs off on the design, and there's no team to catch what I miss. That's the part that scares me, and it's also the part I wanted. Every decision in Compose is mine, including the wrong ones.

I'm also building it differently than anything I've built before. Much of the code is written with AI tools, with me directing, reviewing, and deciding what ships. I'll write about what that's like, including where it falls short.

I don't know yet whether Compose becomes a business. I'd rather find out than keep wondering.

# What's next here

I'll write about building Compose as I go: what's working, what isn't, and what I'm learning doing this on my own. If you want to try it, or just want to talk, [email me](mailto:isaacacasanova@gmail.com).
