# Command reference

Commands are entered in Torch game chat unless the Discord relay section says otherwise. Replace angle-bracket placeholders with values and do not type the brackets. `!hangar help`, `!factionhangar help`, `!blackmarket help`, and `!hangaradmin help` provide in-game help where available.

## Player commands

| Command | Use |
|---|---|
| `!hangar help`, `!hangar helper` | Show player help. |
| `!hangar store <name>` | Store the grid you are looking at. |
| `!hangar list` | List your stored ships. |
| `!hangar load <grid-id>` | Deploy one of your stored ships near you. |
| `!hangar claim <claim-code>` | Deploy a market purchase held for you. |
| `!hangar status` | Show player storage status. |
| `!hangar clean` | Repair your own storage/listing records. |
| `!hangar market list` | Browse active listings. |
| `!hangar market search <query> <category> <station> <page>` | Search/filter market listings. |
| `!hangar market offer <grid-number> <price>` | List a stored grid. |
| `!hangar market details <market-id> <type> <live|timed> <minutes> <description>` | Configure listing presentation and sale mode. |
| `!hangar sell <price> <type> <live|timed> <minutes> <description>` | Store the looked-at grid and list it. |
| `!hangar market cancel <market-id>` | Cancel your active listing. |
| `!hangar bid <market-id> <price>` | Bid on a timed listing. |
| `!hangar buy <market-id>` | Buy a live listing. |
| `!hangar market bid/buy ...` | Equivalent market subcommand aliases. |
| `!hangar market classify <market-id> <category> <station>` | Set listing category/station where enabled. |
| `!hangar lcd here`, `feature <market-id>`, `list`, `clear`, `help` | Manage your owned LCD showroom. Use full root `!hangar lcd ...`. |
| `!factionhangar store <name>`, `list`, `load <number>` | Use faction storage. |
| `!hangar keen list`, `store <name>`, `retrieve <number>` | Use optional Keen storage if enabled. |
| `!blackmarket list` | Browse listings available to you. |
| `!blackmarket listoffer <market-id> <category>` | Create a restricted listing where permitted. |
| `!market commodity list <query> <category> <station> <page>` | Browse commodity listings. |
| `!market commodity sell <definition-id> <quantity> <unit-price> <category> <station>` | Offer physical commodities. |
| `!market commodity buyorder <definition-id> <quantity> <unit-price> <category> <station>` | Create a commodity buy order. |
| `!market commodity fill <order-id> <quantity>` | Fill an order. |
| `!market commodity claim <definition-id> <quantity>` | Claim vaulted commodity items. |
| `!market commodity cancel <order-id>` | Cancel your order. |
| `!market reputation`, `!market analytics` | View market reputation and analytics. |
| `!hangar market remotebuy <server-id> <market-id>` | Reserve a cross-server purchase when Nexus is configured. |
| `!hangar market remotecommit <transaction-id>` | Commit the reserved purchase. |

Some older/advanced player commands exist in the plugin but are omitted here until their setup and availability are verified for the current package. Use in-game help and the current README for the full release-specific list.

## Administrator commands

All `!hangaradmin` commands require Torch admin privileges.

| Command | Use |
|---|---|
| `!hangaradmin help`, `helper` | Show administrator help. |
| `!hangaradmin status` | Inspect storage, market, economy provider, and integration state. |
| `!hangaradmin player <steam-id>` | Inspect a player's records. |
| `!hangaradmin offers` | Inspect market offers. |
| `!hangaradmin recover <steam-id>`, `recoverall` | Rebuild records from stored files. |
| `!hangaradmin cleanhangar <steam-id>` | Repair a player's hangar records. |
| `!hangaradmin storage` | Inspect storage information. |
| `!hangaradmin marketrecover` | Run market recovery. |
| `!hangaradmin removeoffer <offer-id>`, `reopen <market-id>` | Moderate/recover a listing, subject to safety checks. |
| `!hangaradmin terminal <entity-id>`, `terminalhere` | Bind the optional Keen terminal. |
| `!hangaradmin keen <true|false>`, `troastorage <true|false>` | Select storage providers. |
| `!hangaradmin market <true|false>`, `economy <true|false>` | Toggle market or economy transactions. |
| `!hangaradmin econ` | Show active economy provider and Econ+ binding. |
| `!hangaradmin minimumprice <credits>`, `listingfee <true|false> <credits>`, `bidminimum <minutes>`, `limit <count>` | Change supported market policy settings. |
| `!hangaradmin webhook status`, `webhook test` | Inspect/test the standalone market webhook. |
| `!hangaradmin name <display-name>` | Change in-game/LCD branding. |
| `!hangaradmin reload` | Reload and validate the XML config. |

## Discord command relay

When Monitor+ is configured to forward commands, linked players can run identity-based commands such as list, market browsing, bids, and buys while offline. Grid actions, character/looking-target actions, claims/deployments, LCD binding, and commodity custody actions require the player to be in game. Admin overrides are in-game only. Monitor+ controls which command roots Discord accepts; Hangar+ remains the command owner and executor.

For full current syntax of less common advanced modules, use `!hangaradmin help` and the [current README command list](../README.md#commands).
