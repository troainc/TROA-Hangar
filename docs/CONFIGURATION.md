# Configuration reference

The complete XML example is [`TROA-Hangar.cfg.example`](../TROA-Hangar.cfg.example). Copy it only as a reference; configure the file generated on your server. XML is case-sensitive. After edits, use `!hangaradmin reload` and verify with `!hangaradmin status`.

| Setting group | Purpose | Notes |
|---|---|---|
| `Enabled`, `InGameDisplayName` | Master enable and in-game/LCD name | Discord webhook identity has its own setting. |
| `StorageRootDirectory`, `EnableTroaStorage` | TROA grid storage location and provider | Blank root uses the default plugin data directory. |
| `EnableCrossServerStorage`, `EnableNexusIntegration`, `NexusMarketChannelId`, `CrossServerSharedStorageDirectory` | Optional Nexus discovery and cross-server storage/market | Requires consistent shared storage/configuration across participating servers. Leave disabled unless deliberately setting up Nexus. |
| `EnableKeenGridStorage`, `KeenGridStorageTerminalEntityId` | Optional Keen terminal integration | TROA Storage is the default and does not need Keen. |
| `MaxPlayerGrids`, `LookTargetDistanceMeters`, `MinimumGridBlocks`, `MaximumBlocksPerGrid`, `MaximumPcuPerGrid` | Storage eligibility and player limits | Configured maximum block/PCU `0` means unlimited. |
| `AllowSmallGrids`, `AllowLargeGrids`, `AllowStaticGrids` | Accepted grid types | Restrict these to your server rules. |
| `EnableMarket`, `MarketCommandCooldownSeconds`, `MaxMarketOffersPerPlayer`, `MinimumMarketListingPrice` | Player market and listing rules | `EnableEconomyTransactions` separately gates credit movement. |
| `LiveBidDurationMinutes`, `DefaultTimedBidDurationMinutes`, `MinimumTimedBidDurationMinutes`, `MaximumTimedBidDurationMinutes` | Live listing lifetime and timed auction bounds | Timed seller durations are constrained by configured limits. |
| `EnableEconPlusIntegration`, `EconPlusMinimumApiVersion`, `EconPlusPurposeLabel` | Optional Econ+ settlement | Defaults off. If unavailable/incompatible, native economy is used. Econ+ is not required. |
| `EnablePeakHourMarketPricing`, `PeakHourStart`, `PeakHourEnd`, `PeakHourTimeZoneId`, `PeakHourPriceIncreasePercent`, `PeakHourRevenueFactionTag` | Optional buyer surcharge window | Sellers receive the listed price; surcharge goes to the configured faction. |
| `EnableBlackmarket`, `BlackmarketAccessSteamIds`, `BlackmarketListingFeeCredits`, `BlackmarketRevenueFactionTag` | Restricted market listings and fee | Confirm access IDs and faction policy before enabling. |
| `EnableMarketLcdDisplays`, `MarketLcdNameTag`, refresh/page settings | Owner-tagged LCD feeds | Uses existing in-game text surfaces; no client UI. |
| `EnableDiscordMarketWebhook`, `DiscordMarketWebhookUrl`, `DiscordMarketWebhookName`, `DiscordMarketThumbnailUrl` | Standalone market event cards | Use the full secret URL and keep it private. Does not require Monitor+. |
| `EnableMarketInGameConfirmations`, `EnableDiscordMarketDirectMessages`, bot/mapping fields | Private confirmations | Discord DMs need a bot token and Steam-to-Discord ID mappings; keep credentials private. |
| `ChargeForStorage`, `StorageFeeCredits`, `ChargeForRetrieval`, `RetrievalFeeCredits` | Reserved storage fee fields | Current docs mark these as not active; do not assume fees are charged. |
| `EnableMarketAuditWebhook`, `MarketAuditWebhookUrl` | Reserved audit webhook fields | Not the same as market cards; see README's Market Audit note for current support. |

Feature availability can change between alpha packages. Check the current release changelog and README before enabling Nexus, leasing, insurance, contracts, or other Econ+ v2 API features. See [owner setup](SERVER-OWNER-SETUP.md) and [troubleshooting](TROUBLESHOOTING.md).
