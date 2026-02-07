# CS2 Dedicated Server

## Connection

Connect via the CS2 console or Steam server browser:

```
connect disqt.com:27015
```

## Overview

- **User**: `cs`
- **Game files**: `/home/cs/cs2/`
- **Plugin framework**: CounterStrikeSharp (.NET 8.0), installed via Metamod
- **Console**: `screen -r cs2` (detach with Ctrl+A, D)

## Server Control

```bash
/home/cs/start-cs2.sh    # Start the server
/home/cs/stop-cs2.sh     # Stop the server
screen -r cs2             # Attach to the server console
```

## Plugins

| Plugin | Purpose |
|--------|---------|
| GameModeManager | Game modes, map voting, RTV |
| DisqtModes | Modifiers, bot management, workshop maps |
| CS2AnnouncementBroadcaster | Server announcements |
| SimpleAdmin | Admin commands |
| InventorySimulator | Skin system |

## DisqtModes Commands

### Modifiers

| Command | Description |
|---------|-------------|
| `!headshot` | Headshot-only mode |
| `!pistol` | Pistol-only mode |
| `!vampire` | Heal on kill |
| `!ammo` | Unlimited ammo |
| `!random` | Random modifier |

### Bot Management

| Command | Description |
|---------|-------------|
| `!bot add [n] [ct\|t]` | Add bots (optionally to a specific team) |
| `!bot kick [ct\|t]` | Kick bots (optionally from a specific team) |
| `!bot difficulty [0-3]` | Set bot difficulty |

### Workshop Maps

```
!workshop <URL or ID>
```

Loads a workshop map by its Steam Workshop URL or numeric ID.

## Configuration Files

| File | Purpose |
|------|---------|
| `/home/cs/cs2/game/csgo/cfg/server.cfg` | Base server settings |
| `/home/cs/cs2/game/csgo/cfg/bots.cfg` | Bot behavior and quotas |
| `/home/cs/cs2/game/csgo/cfg/ffa.cfg`, `comp.cfg`, etc. | Mode-specific overrides |

!!! warning
    Mode configs can override server.cfg settings. If a CVar change is not persisting, check the active mode's cfg file.

## Bot CVars Reference

```
bot_quota 0                    # Don't auto-fill bots
bot_quota_mode "normal"        # Don't auto-add to quota
bot_join_after_player 0        # Don't auto-join when human joins
mp_autoteambalance 0           # Allow unbalanced teams
mp_limitteams 0                # No team size limits
bot_difficulty 5               # 1=pacifist, 2=easy, 3=normal, 4=hard, 5=expert
```

## Building and Deploying DisqtModes

```bash
cd /home/cs/disqt-bot/DisqtModes && dotnet build -c Release
cp bin/Release/net8.0/DisqtModes.dll \
  /home/cs/cs2/game/csgo/addons/counterstrikesharp/plugins/DisqtModes/
cp -r lang \
  /home/cs/cs2/game/csgo/addons/counterstrikesharp/plugins/DisqtModes/
```

After deploying, restart the server for changes to take effect.

## Logs

CounterStrikeSharp logs are located at:

```
/home/cs/cs2/game/csgo/addons/counterstrikesharp/logs/
```

## Known Issues

### bot_add Sometimes Adds Extra Bots

Running `!bot add 1` occasionally adds 2 bots instead of 1. Investigated mitigations (all applied but the issue persists):

- `bot_join_after_player 0` in bots.cfg
- `bot_quota 0` with `bot_quota_mode "normal"`
- `mp_autoteambalance 0` and `mp_limitteams 0`

Possible remaining causes include game mode configs resetting bot CVars during mode transitions, or CS2 engine behavior with the `bot_add` command.

### Warmup Duration Overrides

`mp_warmuptime 10` is set in server.cfg, but some game modes override this value in their own cfg files.
