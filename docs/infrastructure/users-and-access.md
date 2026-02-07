# Users & Access

## Linux User Isolation

Each service runs under its own dedicated Linux user for isolation and security:

| User | Purpose | Home Directory |
|------|---------|---------------|
| `cs` | CS2 server + Discord bot | `/home/cs/` |
| `minecraft` | Minecraft PaperMC server | `/home/minecraft/` |
| `xonotic` | Xonotic server | `/home/xonotic/` |
| `dev` | APIs + metrics monitoring | `/home/dev/` |

## SSH Access

- **Port**: 24420 (not the default 22)
- All service users have **passwordless sudo** for administrative tasks.
