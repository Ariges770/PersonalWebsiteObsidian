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
 -v "/mnt/c/Users/My Name/Documents/Obsidian:/home/node/obsidian" \
 docker.n8n.io/n8nio/n8n
```  


```yaml
services:
  db:
    image: postgres:16-alpine
    container_name: n8n-db
    restart: always
    environment:
      - POSTGRES_USER=n8n
      - POSTGRES_PASSWORD=n8n_password
      - POSTGRES_DB=n8n
    volumes:
      - n8n_db_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U n8n"]
      interval: 5s
      timeout: 5s
      retries: 5

  n8n:
    image: n8nio/n8n:latest
    container_name: n8n-main
    restart: always
    environment:
      - DB_TYPE=postgresdb
      - DB_POSTGRESDB_HOST=db
      - DB_POSTGRESDB_PORT=5432
      - DB_POSTGRESDB_DATABASE=n8n
      - DB_POSTGRESDB_USER=n8n
      - DB_POSTGRESDB_PASSWORD=n8n_password
      - N8N_RUNNERS_ENABLED=true
      - N8N_RUNNERS_MODE=external
      - N8N_RUNNERS_BROKER_LISTEN_ADDRESS=0.0.0.0
      - N8N_RUNNERS_AUTH_TOKEN=your-secret-here
      - GENERIC_TIMEZONE=Asia/Jerusalem
      - TZ=Asia/Jerusalem
      - N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
    ports:
      - "5678:5678"
      - "5679:5679"
    volumes:
      - n8n_data:/home/node/.n8n
      - "/mnt/c/Users/Ari Gestetner/Documents/Obsidian:/home/node/.n8n-files/obsidian"
    depends_on:
      db:
        condition: service_healthy

  task-runners:
    image: n8nio/runners:latest
    container_name: n8n-runners
    restart: always
    environment:
      - N8N_RUNNERS_TASK_BROKER_URI=http://n8n-main:5679
      - N8N_RUNNERS_AUTH_TOKEN=your-secret-here
    depends_on:
      - n8n

volumes:
  n8n_data:
  n8n_db_data:
```