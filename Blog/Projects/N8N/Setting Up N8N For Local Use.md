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
docker run -d \
  --name n8n-runners \
  --network host \
  -e N8N_RUNNERS_AUTH_TOKEN="my-secret-token" \
  -e N8N_RUNNERS_TASK_BROKER_URI=http://127.0.0.1:5679 \
  n8nio/runners:latest
```  

Then, after running the runners which allows for running Python and Javascript, start the n8n container.  

```bash
docker rm -f n8n

docker run -d \
 --name n8n \
 -p 5678:5678 \
 -p 5679:5679 \
 -e N8N_RUNNERS_ENABLED=true \
 -e N8N_RUNNERS_MODE=external \
 -e N8N_RUNNERS_AUTH_TOKEN="my-secret-token" \
 -e GENERIC_TIMEZONE="Australia/Melbourne" \
 -e TZ="Australia/Melbourne" \
 -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
 -v n8n_data:/home/node/.n8n \
 -v "/mnt/c/Users/My Name/Documents/Obsidian:/data/obsidian" \
 docker.n8n.io/n8nio/n8n
```  
