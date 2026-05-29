---
layout: post
title: "Search, the TOC, and math"
date: 2026-01-12
categories: [Software Engineering]
tags: [jekyll, search, katex]
toc: true
comments: true
description: "How client-side search, the table of contents, and KaTeX math render in the theme."
---

This post sets `toc: true` and `comments: true` in its front matter.

## Search

Search is fully client-side (elasticlunr). The index is built at load time from posts
and every output collection, so this post is searchable from the search overlay.

## Math

Inline math like $a^2 + b^2 = c^2$ and display math render via KaTeX:

$$\int_0^1 x^2 \, dx = \tfrac{1}{3}$$

## Comments

Because `comments: true` is set, a comments section appears below. Giscus only loads when
you configure `giscus.*` in `_config.yml`; otherwise the section is empty by design.
