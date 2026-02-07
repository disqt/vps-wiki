# Kernel Tuning

## Network Optimizations

Network buffer sizes and queue depths are tuned for game server traffic in `/etc/sysctl.d/99-gameserver.conf`:

```ini
net.core.rmem_max = 4194304
net.core.wmem_max = 4194304
net.core.rmem_default = 1048576
net.core.wmem_default = 1048576
net.core.netdev_max_backlog = 5000
```

### What These Do

- **rmem_max / wmem_max**: Raises the maximum UDP receive/send buffer to **4MB** (default was 208KB). This prevents packet drops under high game server load.
- **rmem_default / wmem_default**: Sets the default buffer to **1MB** so new sockets start with a reasonable size.
- **netdev_max_backlog**: Increases the network backlog queue to **5000** packets, preventing drops during traffic spikes.

These settings benefit all game servers (CS2, Minecraft, Xonotic) running on the VPS.

### Applying Changes

```bash
sudo sysctl --system
```

This reloads all sysctl configuration files, including the game server tuning.

## CS2-Specific CVars

These CVars are set in `server.cfg` to complement the kernel tuning:

```
sv_maxrate 0                    # Unlimited bandwidth per client
sv_minrate 128000               # Minimum 128KB/s per client
sv_parallel_sendsnapshot 1      # Multi-threaded snapshot sending
sv_clockcorrection_msecs 15     # Tighter clock sync (competitive standard)
```

!!! warning "Invalid CSGO-era CVars"
    These CVars do **not** exist in CS2 (Source 2 engine). Using them produces "Unknown command" errors in the server console:

    - `net_splitpacket_maxrate`
    - `net_splitrate`
    - `net_maxcleartime`
    - `sv_pure`

## Tick Rate

CS2 runs at **64 tick** with sub-tick input timestamping. This is hardcoded by Valve and cannot be changed through server configuration.
