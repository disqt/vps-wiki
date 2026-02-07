# Xonotic Server

## Connection

Connect using the Xonotic multiplayer browser or console:

```
disqt.com:26420
```

## Overview

- **User**: `xonotic`
- **Management**: LinuxGSM (`/home/xonotic/xntserver`)
- **Console**: tmux (not screen) -- use the LinuxGSM console command
- **Port**: 26420 (UDP)

## Server Control

```bash
/home/xonotic/xntserver start      # Start the server
/home/xonotic/xntserver stop       # Stop the server
/home/xonotic/xntserver restart    # Restart the server
/home/xonotic/xntserver details    # Show server status and details
/home/xonotic/xntserver console    # Attach to tmux console
```

## Server Settings

| Setting | Value |
|---------|-------|
| Game type | Deathmatch |
| Max players | 8 |
| Bots | 4 (minplayers) |
| Bot skill | 6 |
| Bot prefix | `[DISQT]` |
| Grappling hook | Enabled |
| Maps | Stock maps only |

## Configuration

The server configuration file is located at:

```
/home/xonotic/serverfiles/xntserver/data/server.cfg
```

!!! warning
    No systemd service or crontab is configured for Xonotic. The server must be manually restarted after a VPS reboot.

## Known Issue: Invisible Walls

If players experience invisible walls, this is a **client-side version mismatch**, not a server issue.

**Fix**: Ensure the client Xonotic version matches the server version, and clear the download cache:

```
~/.xonotic/data/dlcache/
```

Delete the contents of this directory and reconnect.
