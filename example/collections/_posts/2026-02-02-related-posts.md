---
layout: post
title: "Categories, tags, and related posts"
date: 2026-02-02
categories: [Technology]
tags: [jekyll, nord]
description: "How the taxonomy in _data/taxonomy.yml powers the categories page and related posts."
---

Categories are grouped into themes in `_data/taxonomy.yml`. The
[Categories]({{ '/categories/' | relative_url }}) page renders those groups, and the
post layout uses the same taxonomy to suggest related posts.

This post shares the **Technology** category with "Welcome to Nord Newsletter", so each should
appear in the other's related-posts list.
