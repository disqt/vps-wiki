# Infrastructure

The disqt.com VPS is a **Debian server hosted on OVH**. This section covers the underlying infrastructure that supports all services.

## Key Principles

- **User isolation**: Each service runs under its own Linux user for security and separation of concerns.
- **systemd services**: Most long-running processes are managed as systemd units.
- **nginx reverse proxy**: All HTTP traffic enters through nginx, which routes requests to the appropriate backend.
- **SSH on port 24420**: SSH access uses a non-standard port for basic security hardening.

## Infrastructure Pages

- [nginx](nginx.md) -- Reverse proxy configuration and routing
- [Metrics Monitoring](metrics.md) -- Prometheus, Grafana, and exporters
- [systemd Services](systemd.md) -- Service units and management commands
- [Users & Access](users-and-access.md) -- Linux users and SSH configuration
- [Kernel Tuning](kernel-tuning.md) -- Network optimizations for game servers
