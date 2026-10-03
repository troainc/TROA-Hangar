# Troubleshooting

## Commands do not respond

Confirm Hangar+ loaded in Torch and run `!hangaradmin status`. Check the Torch log for command registration errors and use the correct spelling: `!hangar`, `!hangaradmin`, and `!factionhangar`. If commands work in game but not Discord, verify Monitor+ v1.1.5K4 or later and its allowed command lists. Commands that need a live character cannot run from Discord.

## Config reload fails

The config is XML and element names/casing must match the sample. Fix the element named by the Torch error, then run `!hangaradmin reload` again. Hangar+ rejects a bad edit and keeps its prior running config. Never paste webhook URLs or bot tokens into public issue reports.

## Store says the grid is not eligible

Check that you major-own the grid, are looking directly at it, and are within `LookTargetDistanceMeters`. Check small/large/static permissions, minimum blocks, maximum blocks/PCU, and the player's storage limit. An admin can inspect player records with `!hangaradmin player <steam-id>`.

## Load or claim cannot find space

Move to a clear area and retry. Hangar+ uses a clearance search; if no safe location is found, the grid remains stored. Do not manually delete the stored grid or claim record. Ask an admin to inspect the Torch log and recovery status.

## A stored grid is missing from the list

After a crash or catalog mismatch, an admin can run `!hangaradmin recover <steam-id>` or `!hangaradmin recoverall` to rebuild records from existing grid files. Back up the data directory before manual recovery. `!hangar clean` repairs the caller's own records; admin cleanup is `!hangaradmin cleanhangar <steam-id>`.

## Market buy, bid, or payout fails

Check that the listing is active and sale mode is correct, the player has sufficient funds, economy transactions are enabled, and cooldown/offer limits are not blocking the action. For Econ+, run `!hangaradmin econ` and confirm the required compatible API is loaded. If Econ+ is off/unavailable, Hangar+ uses the native economy. Do not repeat a payment manually until an admin checks the market transaction/recovery state.

## Discord market webhook is silent

Check `EnableDiscordMarketWebhook`, confirm `DiscordMarketWebhookUrl` is the full HTTPS webhook URL, then run `!hangaradmin reload`, `!hangaradmin webhook status`, and `!hangaradmin webhook test`. Hangar+ market cards are standalone and do not require Monitor+. Never share the URL; rotate it if exposed.

## Keen storage is unavailable

Keen storage is optional. Confirm `EnableKeenGridStorage`, bind the correct Services Terminal with `!hangaradmin terminalhere` or `terminal <entity-id>`, and verify the active terminal in `!hangaradmin status`. After a world wipe, old Keen grid IDs may no longer exist.
