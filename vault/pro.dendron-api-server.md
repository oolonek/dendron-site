---
id: 554d3c62-29da-4c86-9d16-f910e36ad7b1
title: Dendron API Server
desc: ''
updated: 1618956831962
created: 1606628243560
---

### Initialize a workspace

- NOTE: specific to kevin's vault, modify for your own

```bash
curl --location --request POST 'http://localhost:3005/api/workspace/initialize' \
--header 'Content-Type: application/json' \
--data-raw '{
    "uri": "/Users/kevinlin/Dendron",
    "config": {
        "vaults": ["/Users/kevinlin/Dendron/vault"]
    }
}'
```

# APIs

## Workspaces

### all

```
curl -XGET localhost:3005/api/workspace/all
```
