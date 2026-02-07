# systemd Services

Most long-running services on the VPS are managed as systemd units.

## Service Units

| Unit Name | User | Description |
|-----------|------|-------------|
| `disqt-bot.service` | cs | Discord bot |
| `lgsm-info-api.service` | dev | Game server status API |
| `miaro-scheduler-api.service` | dev | Work schedule API |
| `node-exporter.service` | root | System metrics exporter |
| `process-exporter.service` | root | Per-process metrics exporter |
| `prometheus.service` | dev | Metrics aggregation |
| `grafana.service` | dev | Metrics dashboards |

## Common Commands

```bash
sudo systemctl status <unit>      # Check service status
sudo systemctl restart <unit>     # Restart a service
sudo systemctl stop <unit>        # Stop a service
sudo systemctl start <unit>       # Start a service
sudo journalctl -u <unit> -f      # Follow live logs
sudo journalctl -u <unit> --since "1 hour ago"  # Recent logs
```

!!! note
    Minecraft and Xonotic use **LinuxGSM** (not systemd) for server management. CS2 uses manual start/stop scripts with **screen**. See their respective pages for control commands:

    - [CS2](../game-servers/cs2.md)
    - [Minecraft](../game-servers/minecraft.md)
    - [Xonotic](../game-servers/xonotic.md)
