# Player guide

Hangar+ is a server-side Torch plugin. You use it through in-game chat; no client mod is needed. The normal player prefix is `!hangar`.

## Store and retrieve your ship

1. Be near and look directly at a grid you own. The default look distance is 1,000 meters.
2. Store it with `!hangar store <name>`, for example `!hangar store Scout`. Hangar+ moves the grid into your personal server storage.
3. See stored ships with `!hangar list`.
4. Retrieve one with `!hangar load <grid-id>`. Hangar+ searches for clear space near you. If there is no safe spot, the grid remains stored.

A grid must meet the server owner's size, block, PCU, ownership, and storage limits. Ask an administrator if a command reports that a limit blocked the action.

## Buy or sell a ship

To list a ship in one step, look at it and use:

`!hangar sell <price> <type> <live|timed> <minutes> <description>`

Example: `!hangar sell 500000 Fighter timed 120 "Combat-ready interceptor"`. For a live listing, use `live 0`; buyers can purchase it while it is active. A timed listing is an auction. The server constrains the duration to its configured minimum and maximum. Supported ship types include Fighter, Assault, Warship, Capital Ship, Carrier, Miner, Hauler, Explorer, Industrial, Station, Rover, Support, Drone, and Trader.

Browse with `!hangar market list`. Use `!hangar buy <market-id>` for a live listing or `!hangar bid <market-id> <price>` for an auction. You may also use the `!hangar market buy` and `!hangar market bid` aliases. Your purchased ship is held for you; when you are ready, move to open space and use `!hangar claim <claim-code>` to deploy it.

If a seller already stored a grid, they can list it with `!hangar market offer <grid-number> <price>`, then set its type and sale mode with `!hangar market details <market-id> <type> <live|timed> <minutes> <description>`. The seller can cancel an active listing with `!hangar market cancel <market-id>`.

## Other features

- `!factionhangar help` shows faction storage commands. Faction storage depends on the player's faction membership and server settings.
- `!blackmarket list` shows restricted listings. Access is controlled by the server owner.
- `!market commodity list` browses item listings; commodity selling and claiming require being in game.
- `!market reputation` and `!market analytics` show market information.
- `!hangar lcd help` explains player-owned LCD showrooms. Look at an LCD on a grid you own and use `!hangar lcd here` to display your active listings.
- Optional Keen Grid Storage commands are available only if the owner enabled Keen storage and configured its terminal.

See the [full command reference](COMMANDS.md). If something fails, read the exact reply and ask the server owner for help; they can inspect Hangar+ with `!hangaradmin status`.
