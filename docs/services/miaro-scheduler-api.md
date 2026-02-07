# miaro-scheduler-api

- **Repository**: [miaro-scheduler-api](https://github.com/disqt/miaro-scheduler-api)
- **Runtime**: Go (Gin framework)
- **Port**: 8081
- **User**: `dev`
- **systemd unit**: `miaro-scheduler-api.service`

## Overview

A 10-day rotating work schedule tracker. The API calculates the current shift based on a fixed cycle that started on August 31, 2024.

## Schedule Pattern

The 10-day cycle repeats continuously:

| Days | Shift | Hours |
|------|-------|-------|
| 0-1 | Morning | 06:00 - 14:00 |
| 2-3 | Afternoon | 14:00 - 22:00 |
| 4-5 | Night | 22:00 - 06:00 |
| 6-9 | Free | - |

## Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /health` | Health check |
| `GET /miaro` | HTML dashboard with current schedule |
| `GET /miaro/json` | JSON response with schedule data |

## Configuration

- **Timezone**: Europe/Paris
- **Cycle start**: August 31, 2024

## Access

The dashboard is accessible at [disqt.com/miaro](https://disqt.com/miaro).

## Service Management

```bash
sudo systemctl restart miaro-scheduler-api    # Restart the API
sudo systemctl status miaro-scheduler-api     # Check status
sudo journalctl -u miaro-scheduler-api -f     # Follow logs
```
