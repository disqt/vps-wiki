# Minecraft Server

## Connection

Connect using the default Minecraft port:

```
disqt.com
```

Port 25565 is the Minecraft default, so no port specification is needed.

## Overview

- **Server software**: PaperMC
- **Mode**: Offline mode with AuthMe for authentication
- **User**: `minecraft`
- **Management**: LinuxGSM (`/home/minecraft/pmcserver`)

## Server Control

```bash
/home/minecraft/pmcserver start      # Start the server
/home/minecraft/pmcserver stop       # Stop the server
/home/minecraft/pmcserver restart    # Restart the server
/home/minecraft/pmcserver console    # Attach to the console
/home/minecraft/pmcserver details    # Show server status and details
```

## Member Management

Player access is managed through a combination of:

- **Whitelist**: Controls who can join the server
- **AuthMe**: Handles player authentication (required since the server runs in offline mode)
- **LuckPerms**: Permission groups for role-based access control

## BlueMap

A 3D world viewer is available at [disqt.com/map](https://disqt.com/map). BlueMap renders the Minecraft world as an interactive 3D map accessible from any browser.

Use the `/bmdiscover` command in-game to trigger 3D model generation for newly explored areas.

## Plugins

| Plugin | Purpose |
|--------|---------|
| AuthMe | Player authentication (offline mode) |
| LuckPerms | Permission groups and roles |
| BlueMap | 3D world viewer at disqt.com/map |
| WorldEdit | In-game world editing |
| Multiverse-Core | Multi-world management |
| AxGraves | Player graves on death |
| SkinsRestorer | Custom skins (offline mode support) |
| Chunky | Pre-generation and world border |
| spark | Performance profiling and monitoring |

## Configuration Hierarchy

LinuxGSM uses a layered configuration system:

```
_default.cfg < common.cfg < pmcserver.cfg
```

Settings in `pmcserver.cfg` override `common.cfg`, which overrides `_default.cfg`. Only put custom settings in `pmcserver.cfg`.

## Automated Tasks (Crontab)

| Task | Schedule | Description |
|------|----------|-------------|
| Monitor | Every 5 minutes | Checks if the server is running, restarts if crashed |
| Update | Saturday 4:00 AM | Updates PaperMC to the latest build |
| LinuxGSM Update | Saturday 5:00 AM | Updates LinuxGSM itself |
| Backup | Daily 6:00 AM | Creates a backup of the world and config |

## Discord Alerts

Server events (crashes, restarts, updates) are sent to the `alert-minecraft` Discord channel.

## Map Management

- **MCASelector**: Used for selective world resets (delete specific region files)
- **BlueMap `/bmdiscover`**: Triggers 3D model generation for newly loaded chunks
