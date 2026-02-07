# lgsm-info-api

- **Repository**: [lgsm-info-api](https://github.com/disqt/lgsm-info-api)
- **Runtime**: Go (Gin framework)
- **Port**: 8080
- **User**: `dev`
- **systemd unit**: `lgsm-info-api.service`

## Overview

A lightweight HTTP API that queries all game servers and returns their status as JSON. It uses the external `gamedig` CLI tool to probe each server.

## Endpoint

```
GET /servers
```

Returns a JSON array with the status of each game server:

- Server name
- Running status
- Current player count
- Maximum players
- Connect URL

## Caching

nginx caches the `/servers` endpoint with a **10-minute TTL** and `stale-while-revalidate`. This means:

- Responses are served from cache for up to 10 minutes
- When the cache expires, nginx serves the stale response while fetching a fresh one in the background
- This reduces load on the game servers and ensures fast response times

## Consumer

The response is consumed by the [Disqt website](website.md) at `disqt.com/servers` to display live server status on the dashboard.

## Service Management

```bash
sudo systemctl restart lgsm-info-api    # Restart the API
sudo systemctl status lgsm-info-api     # Check status
sudo journalctl -u lgsm-info-api -f     # Follow logs
```
