# Architecture

The disqt.com infrastructure runs on a **Debian VPS hosted on OVH**. It hosts game servers, web APIs, a Discord bot, and a full metrics monitoring stack.

## Service Overview

| Service | Port | User | Protocol | Public Path |
|---------|------|------|----------|-------------|
| CS2 Server | 27015 | cs | UDP | Direct connect |
| Minecraft PaperMC | 25565 | minecraft | TCP | Direct connect |
| Xonotic | 26420 | xonotic | UDP | Direct connect |
| Discord Bot | - | cs | - | - |
| lgsm-info-api | 8080 | dev | HTTP | `/servers` |
| miaro-scheduler-api | 8081 | dev | HTTP | `/miaro` |
| Website | - | - | HTTP | `/` |
| Node Exporter | 9100 | root | HTTP | localhost only |
| Process Exporter | 9256 | root | HTTP | localhost only |
| Prometheus | 9090 | dev | HTTP | localhost only |
| Grafana | 3000 | dev | HTTP | `/metrics` |
| nginx | 80/443 | root | HTTP/S | Reverse proxy |

## Network Diagram

```
Internet
   |
   v
nginx (80/443)
   |
   |-- /            --> Static files (website)
   |-- /servers     --> lgsm-info-api (8080)
   |-- /miaro       --> miaro-scheduler-api (8081)
   |-- /metrics/    --> Grafana (3000)
   |-- /map/        --> BlueMap (Minecraft)
   |
   |  (Direct UDP/TCP connections)
   |
   |-- :27015  --> CS2 Server
   |-- :25565  --> Minecraft Server
   |-- :26420  --> Xonotic Server
```

## Key Design Decisions

- **SSH access** is on port **24420** (not the default 22).
- **User isolation**: Each service runs under its own Linux user (`cs`, `minecraft`, `xonotic`, `dev`). See [Users & Access](infrastructure/users-and-access.md) for details.
- **No Docker**: All services run natively as systemd units, or via screen/tmux for game servers.
- **nginx** serves as the single entry point for all HTTP traffic, handling SSL termination and reverse proxying to backends.
