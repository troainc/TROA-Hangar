# Server owner setup

## 1. Install and start

1. Download the current Hangar+ package from [GitHub Releases](https://github.com/troainc/TROA-Hangar/releases).
2. Install the ZIP through Torch and restart the server.
3. On first startup Hangar+ creates `TROA-Hanger.cfg` and its data folders. Keep a backup of the config and storage root when backing up the world.
4. In game as a Torch administrator, run `!hangaradmin status`. Confirm that Hangar+ is enabled, TROA Storage is active, and the market/economy provider match your plan.

The public [sample config](../TROA-Hangar.cfg.example) documents every setting. Edit the installed server config, not the public example. Keep webhook URLs and bot tokens private.

## 2. Choose storage and limits

TROA Storage is the default and supports player/faction storage and the market. Set `EnableTroaStorage` to `true` for this path. `StorageRootDirectory` may be blank to use the plugin's default data directory; if you configure it, choose a durable directory with free space and back it up.

Keen Grid Storage is optional. Leave `EnableKeenGridStorage` false unless you want to use Keen's terminal flow. To set it up, place a Keen Grid Storage Services Terminal and run `!hangaradmin terminalhere` while near it, or bind a known entity ID with `!hangaradmin terminal <entity-id>`. Then enable the integration and verify with `!hangaradmin status`.

Review `MaxPlayerGrids`, `LookTargetDistanceMeters`, `MinimumGridBlocks`, block/PCU limits, and the small/large/static grid switches. A value of `0` for configured maximum block/PCU limits means unlimited. Set market cooldowns, active listing caps, bid durations, and minimum listing price to suit your server.

## 3. Economy and optional integrations

Purchases and transfers can use the native Space Engineers economy. `EnableEconomyTransactions` controls whether Hangar+ can move credits. TROA Econ+ integration is optional and defaults off. If Econ+ is installed and you want durable escrow for eligible grid/Blackmarket/auction sales, set `EnableEconPlusIntegration` to `true`, then reload. Check `!hangaradmin econ` to see which provider is active. Econ+ does not own Hangar grids or listings.

Peak-hour pricing, Blackmarket access, listing fees, LCD feeds, Nexus, Discord market cards, and direct-message confirmations are separately configurable. Each is optional; check the corresponding settings and feature notes before enabling it. Market audit log settings are distinct from the public market webhook.

## 4. Discord market cards (optional)

Hangar+ sends its own market cards directly to a Discord webhook; this feature does not require Monitor+.

1. Create a webhook for the intended Discord channel.
2. In the server's private `TROA-Hanger.cfg`, enable `EnableDiscordMarketWebhook` and paste the full Discord webhook URL into `DiscordMarketWebhookUrl`. A webhook ID by itself will not work.
3. Optionally set the display name and HTTPS thumbnail URL.
4. Run `!hangaradmin reload`, `!hangaradmin webhook status`, then `!hangaradmin webhook test`.

Never post a live webhook URL in a public config, screenshot, log, or repository. Rotate it in Discord if exposed.

## 5. Optional Discord command relay

Monitor+ can forward commands from a configured Discord command channel. Hangar+ still executes and owns its commands. Use Monitor+ v1.1.5K4 or later to receive Hangar replies in Discord. Configure Monitor+'s allowed Torch/player command lists for the Hangar command roots you want to expose; do not allow administrative roots to ordinary players.

Identity-based commands such as list and market browsing can work for linked players while offline. Commands that inspect or move grids, use an in-game character, or deploy a claim must be run in game. See the [command reference](COMMANDS.md#discord-command-relay).

## 6. Reload safely and maintain data

After changing XML, run `!hangaradmin reload`. A rejected config edit leaves the running configuration in place; fix the reported XML element and retry. Use `!hangaradmin status` and `!hangaradmin econ` to verify.

Back up `TROA-HangerData` (or your configured storage root), `TROA-Hanger.cfg`, and the world together. Never manually move or rename stored `.sbc` grid files while Torch is running. After a crash or catalog mismatch, use `!hangaradmin recover <steam-id>` or `!hangaradmin recoverall`; inspect status before cleaning data.

Hangar+ does not currently enable every reserved setting. Consult [Configuration](CONFIGURATION.md) and [Troubleshooting](TROUBLESHOOTING.md) before relying on a feature.
