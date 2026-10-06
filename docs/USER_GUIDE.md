# Hangar+ — player and server owner guide

Hangar+ lets Space Engineers players store and retrieve ships through a Torch server plugin. Players do not install a client mod. Hangar+ owns its storage records, listings, auctions, claims, commodity exchange, and its own market webhook. Monitor+ and Econ+ are optional integrations, not requirements for basic ship storage.

## Player workflow

Use `!hangar help` in game to see commands available on the installed build. Depending on server settings, a player can store an eligible ship, browse/list stored ships, retrieve a ship at a supported spawn point, list a ship for sale, buy a listing, create or participate in bids, and claim an auction or market result. The server can apply listing fees, taxes, market rules, ownership checks, ship-size limits, and spawn-clearance rules. Always read the in-game response before confirming a paid action.

Retrieval can fail if no supported spawn area is clear, the grid's ownership/state does not satisfy policy, or storage data is unavailable. Move to an allowed location, clear the required space, and ask staff before repeatedly retrying a failed paid claim.

## Server owner install and configuration

Install the matching ZIP from the [Hangar releases](https://github.com/troainc/TROA-Hangar/releases) and start Torch once to generate its config/data. Follow [Server Owner Setup](SERVER-OWNER-SETUP.md), then review [Configuration](CONFIGURATION.md) and the credential-free root sample. Set storage paths with adequate disk space and backups; configure eligibility, spawn clearance, pricing/fees, marketplace, auction, and commodity options intentionally. Add Discord credentials only to the live server config and keep them private.

Start with a test faction/player and small-value listing. Confirm store, list, buy/bid, claim, and retrieval paths end to end before enabling them on a live economy. The exact available commands and Discord restrictions are documented in [Commands](COMMANDS.md).

## Ownership and integrations

Hangar validates players and grids before performing storage or sale operations. A stored ship's state is server data; keep backups and use staff recovery paths rather than modifying storage files while Torch is running. Econ+ can provide durable credit escrow where both integrations are configured; otherwise the supported transaction mode depends on the installed build. GridVault+ may provide backup/recovery integration. Check the current docs before relying on either connection.

## Troubleshooting

For failed storage/retrieval, check player ownership, grid condition, configured size/eligibility rules, spawn clearance, and server logs. For missing listings or payment failures, check the market rules, escrow integration, and Hangar data directory. For Discord notices, verify Hangar's webhook config and permissions; Monitor+ routing does not substitute for Hangar's market webhook. Use [Troubleshooting](TROUBLESHOOTING.md) with the precise Hangar version and sanitized logs.
