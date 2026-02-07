# Discord Bot

- **Repository**: [disqt-discord-bot](https://github.com/disqt/disqt-discord-bot)
- **Runtime**: Python (discord.py)
- **User**: `cs`
- **Location**: `/home/cs/disqt-bot/`
- **systemd unit**: `disqt-bot.service`

## Overview

The Discord bot provides remote control of the CS2 server through Discord slash commands. It communicates with the CS2 server using the Source RCON protocol.

## Commands

| Command | Description |
|---------|-------------|
| `/cs exec <cmd>` | Execute an RCON command |
| `/cs map <name>` | Change map (supports Workshop URLs) |
| `/cs maps` | List available maps |
| `/cs competitive` | Switch to Competitive mode |
| `/cs arena` | Arena mode |
| `/cs gungame` | Arms Race mode |
| `/cs retake` | Retake mode |
| `/cs ffa` | FFA Deathmatch |
| `/cs sandbox` | Practice mode |
| `/cs status` | Show server status and player list |
| `/cs bot add [n]` | Add bots |
| `/cs bot kick` | Kick all bots |
| `/cs bot difficulty <level>` | Set bot difficulty |

## Access Control

Commands are restricted to users with a configured Discord role. Only members with the appropriate role can interact with the bot.

## Bot Presence

The bot updates its Discord presence every 30 seconds, displaying the current map and player count on the CS2 server.

## Multi-Language Support

The bot supports French and English. Language files are stored as JSON in the `lang/` directory.

## DisqtModes Plugin

The bot repository also bundles the **DisqtModes** CounterStrikeSharp plugin (C#), which adds in-game modifiers, bot management, and workshop map support. See the [CS2 page](../game-servers/cs2.md) for details on DisqtModes.

## Service Management

```bash
sudo systemctl restart disqt-bot    # Restart the bot
sudo systemctl status disqt-bot     # Check status
sudo journalctl -u disqt-bot -f     # Follow logs
```
