---
tags: commandline, json, jq
---

```
jq '.links | sort_by(.href)' test_links.json
```

This will sort the links array by the href key