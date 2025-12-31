---
author: Ari Gestetner
aliases: 
tags: 
draft: true
img:
desc:
title: Setting Up N8N For Local Use
dateCreated: 31-12-2025
lastModified: 31-12-2025
---

# Setting Up N8N For Local Use

In order to setup N8N for local use (i.e. on pc or homeserver on lan), follow the following commands.  

```bash
docker rm -f n8n-runners

docker run -d \
  --name n8n-runners \
  --network host \
  -e N8N_RUNNERS_AUTH_TOKEN="my-secret-token" \
  -e N8N_RUNNERS_TASK_BROKER_URI=http://127.0.0.1:5679 \
  n8nio/runners:latest

``` 