---
tags: commandline, json, jq
date: 2022-06-23
title: Using JQ to sort a json structure
---

# [[2022-06-23 - Using JQ to sort a json structure]]

```
jq '.links | sort_by(.href)' test_links.json
```

This will sort the links array by the href key