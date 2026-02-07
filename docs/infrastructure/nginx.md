# nginx

nginx serves as the reverse proxy for all HTTP traffic on the VPS.

## Configuration

The main site configuration is located at:

```
/etc/nginx/sites-enabled/disqt.com
```

## Routing Table

| Path | Backend | Notes |
|------|---------|-------|
| `/` | Static files | disqt-info-website |
| `/servers` | `localhost:8080` | Cached 10min, stale-while-revalidate |
| `/miaro` | `localhost:8081` | miaro-scheduler-api |
| `/metrics/` | `localhost:3000` | Grafana dashboards |
| `/map/` | BlueMap | Minecraft 3D map |

## SSL/TLS

HTTPS is provided by **Let's Encrypt** certificates, managed by **certbot**. Certificates are automatically renewed.

## Common Commands

```bash
sudo nginx -t          # Test configuration for syntax errors
sudo nginx -s reload   # Reload configuration without downtime
```

Always run `nginx -t` before reloading to catch configuration errors.
