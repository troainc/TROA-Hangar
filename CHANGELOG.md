# Hangar+ Changelog

## v2.0.0-alpha.5.8 - Safer grid deployment search

- Hangar estimates the stored ship's clearance radius and searches farther from the player in six directions instead of checking four nearby points.
- Planet checks use the planet body and actual closest surface, avoiding false blocks from the planet's full world AABB. Other grids, voxel maps, and entities still block overlapping space.
- Failed searches leave the ship safely stored. Build/package passed with zero warnings and errors; dedicated-server spawn acceptance remains pending.
- Package: `TROA-Hangar-v2.0.0-alpha.5.8-spawn-clearance.zip`; SHA-256 `74D1EE3FB65257E1EA391906AEC39165B98CE6A7FB5B9B9D5A6DB7CCD1DB7265`.

## v2.0.0-alpha.5.7 - Commands from Discord

- Hangar+ commands now work from Discord through the TROA Monitor+ bridge (Monitor+ v1.1.5K4 or newer). **Root cause of the "nothing happens in Discord" report:** Monitor+ forwarded plugin commands to Torch but sent their replies only to the server log. That is fixed in Monitor+ v1.1.5K4, which now posts Hangar+ replies back to the channel.
- Identity-based player commands now work for a **linked Discord player even while they are offline**. Hangar+ reads the forwarded sender's Steam ID when there is no in-game player. This covers `list`, `clean`, `market list/search/details/classify/offer/bid/buy/finance/cancel`, `bid`, `buy`, `lease list/pay`, `redeem`, `lcd list`, insurance and contract commands, `blackmarket list/listoffer`, `factionhangar list`, and `market reputation`/`commodity cancel`.
- Commands that need your character in the world (`store`, `sell`, `load`, `claim`, `lcd here/feature/clear`, Keen store/retrieve, faction store/load, commodity sell/fill/claim/locprice) now reply "must be used in game" from Discord instead of a generic error. Grid safety is unchanged: nothing that spawns, removes, or moves a grid runs without a live in-game player.
- The admin `override` keyword stays in-game only. A Discord-forwarded command never has an in-game admin, so it can never trigger an override.
- No config changes. Builds with zero warnings and zero errors on .NET Framework 4.8.

## v2.0.0-alpha.5.6 - Admin override keyword & reopen listing

- Adds an admin-only `override` keyword on player market commands: `!hangar bid <market-id> <price> override` and `!hangar buy <market-id> override` let an admin bid on / buy their own offer and skip the cooldown; `!hangar claim <grid-id> override` deploys any player's stored grid for recovery. Non-admins passing the keyword get no bypass.
- Adds `!hangaradmin reopen <market-id>` to reactivate a stuck or closed listing (refuses sold/awaiting-claim listings and requires the grid still in custody, so it cannot duplicate a delivered grid).
- Builds with zero warnings and zero errors on .NET Framework 4.8.

## v2.0.0-alpha.5.5 - Fix all in-game commands failing to register

- Fixes every Hangar+ chat command echoing as plain text with no response. The commodity commands used a `decimal` quantity parameter, which Torch cannot parse; that threw during registration and aborted the whole plugin's commands (`!hangar`, `!hangaradmin`, `!market`). Quantities are now parsed from text inside the command; behavior is unchanged. With the 5.4 duplicate-path fix, the plugin now registers cleanly.
- Builds with zero warnings and zero errors on .NET Framework 4.8.

## v2.0.0-alpha.5.4 - Fix duplicate market command path

- Fixes a Torch startup error (`command path hangar market is already registered`) caused by the standalone `!hangar market` alias colliding with the `market …` subcommand group. Removed the alias: `!hangar market list` still lists offers and every other `market …` command is unchanged; a bare `!hangar market` now shows the subcommand list.
- Builds with zero warnings and zero errors on .NET Framework 4.8.

## v2.0.0-alpha.5.3 - Ship Leasing, Auto-Impound & Econ+ v2.1 Integration

- Adds optional ship leasing / financing with auto-impound: recurring payment plans held in Hangar+ custody, admin lease/impound commands, and financed market purchases (`!hangar market finance`). All default off; every credit moves through the economy authority.
- Adds a reflection-bound Econ+ v2.1 service surface (territory docking, location pricing, insurance, contracts), all default off and capability-gated; Hangar+ still never requires Econ+.
- Builds with zero warnings and zero errors on .NET Framework 4.8.

## v2.0.0-alpha.5.2 - Market Search/Classify, Cross-Server Buying & Commodity Escrow

- Adds market commands: `!hangar market search` (search active listings by text, category, and station), `!hangar market classify` (set a listing's category and station), `!hangar market remotebuy` (reserve a listing on another Nexus server), and `!hangar market remotecommit` (escrow credits and commit a cross-server purchase).
- Cross-server buyers are notified in game with their claim code as soon as the source server completes delivery.
- Commodity sell-order fills settle through the durable economy escrow (Econ+ when enabled); commodity buy orders keep their pre-escrowed native credit pool.
- Builds for .NET Framework 4.8 with zero warnings and zero errors.

## v2.0.0-alpha.5.1 - Webhook Restore, Prettier Cards & Ship Types

- Fixes the Discord market webhook: real market cards were not posting after the previous rich-embed change. Cards now use a single reliably rendered embed and post again.
- Redesigns the market card: sectioned Ship Registry / Market Exchange / Transmission layout with emoji, per-event colour, a live countdown, and a progress bar for timed auctions.
- Shows the last webhook delivery error (Discord HTTP status and response, never the URL) in `!hangaradmin webhook status` so delivery problems are diagnosable.
- Adds defined ship types with emoji — Fighter, Assault, Warship, Capital Ship, Carrier, Miner, Hauler, Explorer, Industrial, Station, Rover, Support, Drone, Trader — shown on cards and listed in help.
- Builds for .NET Framework 4.8 with zero warnings and zero errors.

## Unreleased - Hangar+ Market Expansion

- Adds explicit market transaction states and a durable recovery journal.
- Adds server-driven LCD and trade-station feeds using existing text surfaces; no client UI is required.
- Adds market search, filtering, categories, and station-specific listings.
- Adds access-controlled Blackmarket listings, fees, anonymous presentation, and local auditing.
- Adds optional Nexus v3 discovery, read-only catalog synchronization, and locked cross-server purchases.
- Adds physical commodity sell custody, escrowed buy orders, claimable vaults, reputation, and analytics.
- Expands the optional Discord market webhook to grid-market, Blackmarket, commodity, and cross-server lifecycle events.
- Uses **Hangar+** as the default in-game identity and adds `!hangaradmin name <display-name>`.
- Keeps `DiscordMarketWebhookName` independent so established Discord webhook names remain unchanged.
- Retains legacy filenames, storage paths, Nexus identifiers, record values, and LCD tags for upgrade compatibility.
- Builds for .NET Framework 4.8 with zero warnings and zero errors.

## v2.0.0-alpha.4.39 - Command Spelling Correction

- Changes player commands from `!hanger` to the correctly spelled `!hangar`.
- Changes administrator commands from `!hangeradmin` to `!hangaradmin`.
- Changes faction commands from `!factionhanger` to `!factionhangar`.
- Renames `!hangaradmin cleanhanger` to `!hangaradmin cleanhangar`.
- Updates all README instructions and configuration tips to match the working in-game commands.
- Keeps legacy plugin filenames and storage folders unchanged so existing server data upgrades safely.

## v2.0.0-alpha.4.38 - Market Lifecycle

- Allows players to buy active live listings until their configured deadline.
- Keeps timed listings as auctions that settle the highest valid bid when time expires.
- Adds Discord-native relative countdowns to both live and timed market cards.
- Closes expired live listings and returns unsold ships to the seller's Steam-ID hangar.
- Returns timed listings when no valid sale can be completed.
- Runs expiry settlement on Torch's game thread and prevents duplicate timer processing.
- Sends private in-game confirmations from **TROA Market Exchange** to sellers, buyers, and bidders.
- Adds optional Discord DM confirmation embeds using a bot token and `SteamID:DiscordUserID` mappings.
- Refreshes existing active market cards once after startup so they receive the new countdown format.
