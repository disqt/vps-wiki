# Services

The VPS runs several supporting services alongside the game servers.

## Service Directory

| Service | Repository | Description |
|---------|-----------|-------------|
| Discord Bot | [disqt-discord-bot](https://github.com/disqt/disqt-discord-bot) | CS2 server control via Discord |
| Server Status API | [lgsm-info-api](https://github.com/disqt/lgsm-info-api) | Game server status JSON endpoint |
| Scheduler API | [miaro-scheduler-api](https://github.com/disqt/miaro-scheduler-api) | Work schedule tracker |
| Website | [disqt-info-website](https://github.com/disqt/disqt-info-website) | Server status dashboard |

## Service Pages

- [Discord Bot](discord-bot.md) -- Python bot for controlling the CS2 server via Discord slash commands
- [lgsm-info-api](lgsm-info-api.md) -- Go API that queries game servers and returns their status as JSON
- [miaro-scheduler-api](miaro-scheduler-api.md) -- Go API for a 10-day rotating work schedule
- [Website](website.md) -- Static dashboard displaying live game server status
