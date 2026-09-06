# Hangar+

TROA-Hangar is a clean Torch plugin for managing server-approved Space Engineers grid storage. It does not use or package any Quantum Hangar code. QC data can be copied with the separate migration tool in `tools/QC-to-TROA-Hanger-Migrator`.

## Current Alpha Build

`v2.0.0-alpha.5.0` is the current test build for Torch on .NET Framework 4.8. The package is `TROA-Hangar-v2.0.0-alpha.5.0-econ-plus.zip` with SHA-256 `9D1F91ECB8E048B3A5DA13E1A5C380AC8C34DEB6510C64CED28F3015B02C7B0A`. It uses **TROA Storage by default**. Keen Grid Storage is optional and is not required for player storage, listing, selling, bidding, or buying. Market, Blackmarket, and economy settlement work standalone, and can optionally settle through the **TROA Econ+** escrow API when that plugin is installed.

### What Works

- Creates portable storage folders: `PlayersHangers`, `FactionHangers`, and `MarketHangers`.
- Generates `TROA-Hanger.cfg` on first start.
- Saves major-owner grids into each player's `PlayersHangers` folder.
- Restores stored TROA grids and removes the completed storage record.
- Lists player grids, creates offers, accepts bids, cancels offers, and buys TROA Storage offers.
- Lets server owners rebuild missing player records from existing Steam-ID hangar folders after a crash or catalog problem.
- Lets server owners review and attach current Keen Grid Storage IDs for a player.
- Supports faction-owned TROA storage through `FactionHangers`, with member-only store, list, and load commands.
- Uses the native Space Engineers economy for purchases when enabled.
- Enforces player grid and active-offer limits plus a market command cooldown.
- Supports optional peak-hour market pricing: buyers pay a configurable percentage more during the server owner's configured peak window, while sellers receive the listed price.
- Supports buy-now live listings and timed auctions, with automatic closure at the configured deadline.
- Returns expired live listings and timed listings without a completed sale to the seller's Steam-ID hangar automatically.
- Can post standalone Discord market embeds without installing TROA Discord Monitor. Embeds include the ship name, price, type, description, bid mode, and a Discord-native live countdown.
- Sends private in-game confirmations from **TROA Market Exchange** and supports optional Discord DM embeds through configured Steam-to-Discord mappings.
- Includes admin controls for storage, economy, market availability, limits, terminal setup, inspection, and moderation.
- Runs on Windows and Linux-hosted AMP/Wine installations using .NET path-safe APIs.
- Adds durable market transaction journals, explicit listing states, and crash-recovery records.
- Drives existing in-game LCDs and text-surface trade stations; no client mod or external UI is required.
- Supports searchable categories, station markets, access-controlled blackmarket listings, and audited fees.
- Integrates with the Nexus v3 Mod API for read-only catalog discovery and durable cross-server purchases.
- Supports physical commodity sell custody, escrowed buy orders, claimable commodity vaults, reputation, and analytics.
- Uses the community-neutral **Hangar+** name in game by default. Owners can change it without altering their configured Discord webhook identity.
- Optionally settles grid-market purchases, timed auctions, and Blackmarket sales through the **TROA Econ+** durable, idempotent escrow API (hold, capture, release) when Econ+ is installed and enabled; otherwise uses the native economy. Econ+ is never required.
- Posts rich, structured Discord market cards with a thumbnail, per-event colour, ship-class emoji, inline fields, a live Discord countdown, and a progress bar for timed auctions.
- Lets players turn any in-game LCD or text panel they own into a live ship-sale showroom, or feature a single listing, with `!hangar lcd` commands.

### Test Setup

1. Install the plugin ZIP in Torch and restart Torch.
2. Run `!hangaradmin status` to confirm that TROA Storage and the market are enabled.
3. Look directly at a grid you major-own, within 1,000 meters, then run `!hangar store <name>`.
4. Run `!hangar list`, then `!hangar load <grid-id>` to restore the grid.
5. Store another grid and list it with `!hangar market offer <grid-number> <price>` or store-and-list it with `!hangar sell <price> <type> <live|timed> <minutes> <description>`.
6. Set its presentation and bidding rule: `!hangar market details <market-number> <type> <live|timed> <minutes> <description>`. Use `0` minutes for `live`; timed bids require a positive number of minutes.
7. Test `!hangar buy <offer-id>` against a live listing. Test `!hangar bid <offer-id> <price>` against a timed listing and let its timer settle. The buyer can move to a clear area and use `!hangar claim <claim-code>` when ready to deploy the purchased ship.
8. Optional: configure the standalone Discord webhook in `TROA-Hanger.cfg`, run `!hangaradmin reload`, then run `!hangaradmin webhook test`.
9. Optionally place a Keen Grid Storage Services Terminal and configure it with `!hangaradmin terminalhere` while standing near it, or `!hangaradmin terminal <terminal-entity-id>`.

### Commands

- `!hangar help`
- `!hangar helper`
- `!hangar store <name>`
- `!hangar load <grid-id>`
- `!hangar claim <claim-code>` *(deploy a purchased ship)*
- `!hangar status`
- `!hangar keen list`
- `!hangar keen store <name>`
- `!hangar keen retrieve <number>`
- `!hangar clean`
- `!factionhangar help`
- `!factionhangar store <name>`
- `!factionhangar list`
- `!factionhangar load <number>`
- `!hangar list`
- `!hangar market list`
- `!hangar market` *(alias for market list)*
- `!hangar market offer <grid-number> <price>`
- `!hangar market details <market-id> <type> <live|timed> <minutes> <description>`
- `!hangar sell <price> <type> <live|timed> <minutes> <description>`
- `!hangar market cancel <market-id>`
- `!hangar bid <market-id> <price>`
- `!hangar market bid <market-id> <price>` *(alias)*
- `!hangar buy <market-id>`
- `!hangar market buy <market-id>` *(alias)*
- `!hangar lcd here` *(bind the LCD you are looking at as your ship showroom)*
- `!hangar lcd feature <market-id>` *(feature one listing on the LCD you are looking at)*
- `!hangar lcd list`
- `!hangar lcd clear`
- `!hangar lcd help`
- `!hangar market search <query> <category> <station> <page>`
- `!hangar market classify <market-id> <category> <station>`
- `!hangar market remotebuy <server-id> <market-id>`
- `!hangar market remotecommit <transaction-id>`
- `!blackmarket list`
- `!blackmarket listoffer <market-id> <category>`
- `!market commodity list <query> <category> <station> <page>`
- `!market commodity sell <definition-id> <quantity> <unit-price> <category> <station>`
- `!market commodity buyorder <definition-id> <quantity> <unit-price> <category> <station>`
- `!market commodity fill <order-id> <quantity>`
- `!market commodity claim <definition-id> <quantity>`
- `!market commodity cancel <order-id>`
- `!market reputation`
- `!market analytics`
- `!hangar storeid <entity-id> <name>` *(Torch admin troubleshooting)*
- `!hangar storage` *(Torch admin)*
- `!hangaradmin help` *(Torch admin)*
- `!hangaradmin helper` *(Torch admin)*
- `!hangaradmin terminal <entity-id>` *(Torch admin)*
- `!hangaradmin terminalhere` *(Torch admin)*
- `!hangaradmin keen <true|false>` *(Torch admin)*
- `!hangaradmin recover <steam-id>` *(Torch admin)*
- `!hangaradmin recoverall` *(Torch admin)*
- `!hangaradmin cleanhangar <steam-id>` *(Torch admin)*
- `!hangaradmin keenlist <steam-id>` *(Torch admin)*
- `!hangaradmin keenattach <steam-id> <keen-grid-id>` *(Torch admin)*
- `!hangaradmin status` *(Torch admin)*
- `!hangaradmin player <steam-id>` *(Torch admin)*
- `!hangaradmin offers` *(Torch admin)*
- `!hangaradmin removeoffer <offer-id>` *(Torch admin)*
- `!hangaradmin troastorage <true|false>` *(Torch admin)*
- `!hangaradmin market <true|false>` *(Torch admin)*
- `!hangaradmin economy <true|false>` *(Torch admin)*
- `!hangaradmin econ` *(Torch admin; shows the active economy provider and Econ+ status)*
- `!hangaradmin marketrecover` *(Torch admin)*
- `!hangaradmin minimumprice <credits>` *(Torch admin)*
- `!hangaradmin listingfee <true|false> <credits>` *(Torch admin)*
- `!hangaradmin bidminimum <minutes>` *(Torch admin)*
- `!hangaradmin limit <count>` *(Torch admin)*
- `!hangaradmin webhook status` *(Torch admin)*
- `!hangaradmin webhook test` *(Torch admin)*
- `!hangaradmin name <display-name>` *(Torch admin; changes in-game chat, notification, and LCD branding only)*
- `!hangaradmin reload` *(Torch admin; reloads and validates `TROA-Hanger.cfg`)*

## Standalone Discord Market Embeds

TROA-Hangar can post market listings directly to a Discord channel webhook. It does **not** require TROA Discord Monitor or any other Discord plugin.

1. Create a Discord webhook for the market channel.
2. In the private server `TROA-Hanger.cfg`, set `EnableDiscordMarketWebhook` to `true` and paste the **full Discord webhook URL** into `DiscordMarketWebhookUrl`. A webhook ID alone will not work.
3. Run `!hangaradmin reload`, then `!hangaradmin webhook status` and `!hangaradmin webhook test`. The test command now reports a successful Discord response or a specific HTTP/network error in game.

If reload reports an XML error, it leaves the existing config unchanged. Fix the named tag and reload again; it will not reset the configuration to defaults.

The webhook posts embeds only: new listings, listing updates, accepted bids, sold listings, expired listings, and cancelled listings. Its market-exchange layout contains the **Ship Name**, **Class**, **Description**, **Listed Price**, **Current Buyer Total**, **Bid Mode**, a live Discord countdown, and active **Peak Surcharge** plus its treasury destination. Live listings are green, timed listings are blue, and completed, expired, or cancelled listings are red. Webhook posts intentionally do not include Steam IDs or server file paths.

Each market listing receives a permanent five-character alphanumeric **Market ID**, such as `K7X4Q`. Players can use this ID with market details, bid, buy, and cancel commands.

## In-game LCD and trade-station displays

The default in-game name is `Hangar+`. Rename any text-surface block to include `[HANGAR+ MARKET]`, `[HANGAR+ BLACKMARKET]`, or `[HANGAR+ COMMODITY]`. The server writes the matching paged feed to every surface on that block. `!hangaradmin name <display-name>` changes the in-game name and normal market tag. Older TROA-prefixed LCD tags remain accepted for upgrade compatibility. This feature uses existing Space Engineers blocks and does not install a client UI.

### Player ship-sale showrooms

Players can bind their own displays without renaming blocks. Look directly at an LCD or text panel on a grid you own and run `!hangar lcd here` to show a live showroom of all your active listings, or `!hangar lcd feature <market-id>` to spotlight one listing with full detail and its buy code. `!hangar lcd list` shows your bound panels and `!hangar lcd clear` unbinds the one you are looking at (or all of yours). Bindings persist across restarts and clear automatically if the block is removed. Only the grid owner (or an admin) can bind a panel.

`InGameDisplayName` affects only Space Engineers chat, notifications, and LCD headings. `DiscordMarketWebhookName` remains independent and is used unchanged for the Discord webhook username, embed author, and footer. This lets existing communities preserve their established Discord webhook identity.

The optional market webhook covers normal grid-market cards and lifecycle changes, Blackmarket listings, commodity listings and fills, and cross-server reservation, completion, and recovery events. Player Steam IDs, shared-storage paths, claim codes, and private recovery details are not included in public webhook posts.

## Nexus cross-server market

Enable Nexus integration on every participating Nexus v3 server and use the same channel ID. For purchases, `StorageRootDirectory` and `CrossServerSharedStorageDirectory` must point to the same shared folder on every participating server. A buyer first reserves with `remotebuy`, then explicitly escrows credits with `remotecommit`. Durable locks and transaction records are retained for recovery if delivery or settlement fails.

## Commodity exchange

Commodity definition IDs use Space Engineers notation such as `MyObjectBuilder_Ingot/Iron`. Sell orders remove items from the player's character inventory into durable custody. Buy orders debit their full value into escrow. Completed purchases are placed in the buyer's durable commodity vault and can be claimed into a character inventory later.

## Player Bid Timers

All players can use `!hangar store`, `!hangar load`, `!hangar list`, `!hangar claim`, `!hangar sell`, `!hangar bid`, and `!hangar buy`; these are not admin-only commands. A player can create a listing in one step, for example: `!hangar sell 100000 Fighter timed 60 "Combat-ready ship"`. Live listings can be purchased immediately with `!hangar buy` until their timer reaches zero. Timed listings accept bids and automatically award the highest valid bid when the timer ends. If no purchase or valid timed settlement occurs, the ship returns to the seller's Steam-ID hangar. Discord cards use relative timestamps that visibly count down in each viewer's local time.

## Private Market Confirmations

`EnableMarketInGameConfirmations` sends private in-game messages from **TROA Market Exchange** for listing creation, bids, purchases, timed-auction results, cancellations, and expired returns. This is enabled by default and does not require Discord.

Optional Discord private embeds require `EnableDiscordMarketDirectMessages`, `DiscordMarketBotToken`, and one `DiscordMarketPlayerMappings` entry per player in `SteamID:DiscordUserID` format. A normal Discord webhook cannot send private messages. Keep the bot token private and never include a live token in a public release.

## Peak-Hour Market Pricing

Set `EnablePeakHourMarketPricing` to `true` in `TROA-Hanger.cfg` to add a purchase-only surcharge during a chosen time window. Configure `PeakHourStart` and `PeakHourEnd` with whole hours from `0` through `23`, then set `PeakHourPriceIncreasePercent`. `18`, `22`, and `10` means 6:00 PM through 9:59 PM has a 10% buyer surcharge. Use `PeakHourTimeZoneId` for a Windows timezone such as `Eastern Standard Time`, or leave it blank for the server's local time. Sellers always receive the listed price. The surcharge is deposited into `PeakHourRevenueFactionTag`, which defaults to the `TRO` admin faction. If that faction is missing, TROA-Hangar creates it as an NPC faction and creates its economy account.

## Configuration Reference

The generated `TROA-Hanger.cfg` retains its legacy filename for upgrade compatibility. Every setting used by `.4.39` is listed here; keep webhook URLs and bot tokens private.

| Settings | Purpose |
|---|---|
| `Enabled` | Master plugin enable switch. |
| `InGameDisplayName` | Player-facing Space Engineers name; defaults to `Hangar+` and does not rename Discord webhooks. |
| `StorageRootDirectory` | Blank uses the default `TROA-HangerData` folder. |
| `EnableTroaStorage` | Enables normal Steam-ID-based TROA file storage. |
| `EnableCrossServerStorage`, `CrossServerSharedStorageDirectory`, `CrossServerLockTimeoutMinutes` | Enables shared Nexus custody, its durable shared root, and stale-lock recovery timeout. |
| `EnableNexusIntegration`, `NexusMarketChannelId`, `NexusCatalogRefreshSeconds` | Nexus v3 discovery, read-only catalog broadcast, and purchase-message channel. |
| `EnableMarketLcdDisplays`, `MarketLcdNameTag`, `MarketLcdRefreshSeconds`, `MarketLcdRowsPerPage` | Existing-block LCD feeds and paging. |
| `EnableBlackmarket`, `BlackmarketListingFeeCredits`, `BlackmarketRevenueFactionTag`, `BlackmarketAccessSteamIds` | Blackmarket access, listing fees, revenue, and auditing. |
| `EnableKeenGridStorage`, `KeenGridStorageTerminalEntityId` | Optional Keen storage and bound Services Terminal. |
| `MaxPlayerGrids` | Player storage limit; `0` is unlimited. |
| `LookTargetDistanceMeters` | Maximum look-target distance for store and sell. |
| `MinimumGridBlocks`, `MaximumBlocksPerGrid`, `MaximumPcuPerGrid` | Grid limits; maximum values use `0` for unlimited. |
| `AllowSmallGrids`, `AllowLargeGrids`, `AllowStaticGrids` | Allowed grid sizes and station storage. |
| `EnableMarket`, `MarketCommandCooldownSeconds`, `MaxMarketOffersPerPlayer` | Market availability, cooldown, and active-offer limit. |
| `MinimumMarketListingPrice` | Lowest valid listing price. |
| `ChargeMarketListingFee`, `MarketListingFeeCredits` | Optional economy-backed listing fee. |
| `EnableEconomyTransactions` | Enables purchases and native credit transfers. |
| `EnableEconPlusIntegration`, `EconPlusMinimumApiVersion`, `EconPlusPurposeLabel` | Optional TROA Econ+ escrow settlement for grid/Blackmarket/auction sales, the minimum Econ+ API version required, and the audit label recorded on Econ+ transactions. Defaults to disabled; native economy is used when off or Econ+ is absent. |
| `LiveBidDurationMinutes` | Live buy-now lifetime; `0` is unlimited. |
| `DefaultTimedBidDurationMinutes`, `MinimumTimedBidDurationMinutes`, `MaximumTimedBidDurationMinutes` | Timed-auction default and seller-selected range. |
| `EnablePeakHourMarketPricing`, `PeakHourStart`, `PeakHourEnd`, `PeakHourPriceIncreasePercent` | Peak buyer surcharge and time window. |
| `PeakHourTimeZoneId`, `PeakHourRevenueFactionTag` | Peak timezone and receiving faction. |
| `EnableDiscordMarketWebhook`, `DiscordMarketWebhookUrl`, `DiscordMarketWebhookName` | Player-facing Discord market cards. |
| `DiscordMarketThumbnailUrl` | Optional HTTPS image (for example a server logo) shown as the thumbnail on every market embed. Blank for none. |
| `EnableMarketInGameConfirmations` | Private in-game market confirmations. |
| `EnableDiscordMarketDirectMessages`, `DiscordMarketBotToken`, `DiscordMarketPlayerMappings` | Optional Discord DMs using `SteamID:DiscordUserID` mappings. |
| `EnableMarketAuditWebhook`, `MarketAuditWebhookUrl` | Reserved fields; `.4.39` does not send Discord audit embeds. |
| `ChargeForStorage`, `StorageFeeCredits`, `ChargeForRetrieval`, `RetrievalFeeCredits` | Reserved for future use; no storage/retrieval fee is charged. |

## Market Audit

Market activity is persistently recorded in `TROA-HangerData/TROA-HangerMarketAudit.log` (or the configured storage root). The market-audit webhook settings exist in the config but are not wired to Discord delivery in `.4.39`; do not describe or test them as an active webhook feature.

## Not Yet Enabled

Keen-storage market purchases, alliance hangars, automated cleanup, and Discord audit-webhook delivery are not enabled. Player and faction TROA Storage, local and Nexus market custody, LCD feeds, commodity escrow, timed settlement, and local market auditing are available.

## Recovery Notes

TROA Storage folders are organized by Steam ID. If Torch crashes after files are written but before the catalog is updated, run `!hangaradmin recover <steam-id>` or `!hangaradmin recoverall` to attach the existing `.sbc` files again.

Run `!hangar clean` to repair your own listing when a file and catalog record no longer match. Server owners can run `!hangaradmin cleanhangar <steam-id>`. Unreadable `.sbc` files are moved to that player's `Quarantine` folder; they are never deleted by cleanup.

Keen Grid Storage IDs are generated by the active world. A server wipe creates a new world and new Keen IDs, so use `!hangaradmin keenlist <steam-id>` and `!hangaradmin keenattach <steam-id> <keen-grid-id>` again after a wipe. An old Keen ID cannot restore a grid that no longer exists in the new world.

See `ARCHITECTURE.md` for the full roadmap and compatibility rules.

## TROA Econ+ integration

[TROA Econ+](https://github.com/troainc/TROA-Econ-Plus) is the optional economy companion for Hangar+. Econ+ provides durable credit holds, captures, refunds, treasury policy, and recovery through a versioned server-side API while Hangar+ remains responsible for grids and market custody.

To enable it, install both plugins and set `EnableEconPlusIntegration` to `true`. Hangar+ discovers Econ+ at runtime (by reflection — there is no hard assembly dependency) and, if a compatible API version is present (`EconPlusMinimumApiVersion`, default `1.1.0`), routes grid-market purchases, timed-auction settlements, and Blackmarket sales through Econ+ **durable, idempotent escrow**: the buyer's funds are held before the grid moves, captured to the seller only after custody transfers, and released or refunded on any failure. Retrying the same purchase reuses the existing hold instead of charging twice.

When the setting is off, Econ+ is not installed, or its API version is too low, Hangar+ automatically uses the native Space Engineers economy. **Econ+ is never required.** Listing fees, Blackmarket fees, and peak-hour surcharges are deposited to the configured faction treasury regardless of provider, because Econ+ escrow is player-to-player. Run `!hangaradmin econ` to see the active provider and binding status.
