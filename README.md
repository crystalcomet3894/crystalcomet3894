<h1 align="center">Hey, I'm [Your Name]</h1>
<p align="center">Roblox Developer · Luau Scripting · Systems & Gameplay Programming</p>

### About

I build games on Roblox and have been scripting in Luau for the better part of [X] years.
Most of my work sits on the technical side of things: networking, data persistence,
combat systems, and the kind of backend plumbing that players never notice when it
works and immediately notice when it doesn't.

I care about clean architecture, readable code, and shipping things that actually hold
up under load. If a system can't survive a few thousand concurrent players, I'm not
done with it yet.

### What I work on

- Gameplay systems (combat, inventory, progression, economy)
- Client-server networking with RemoteEvents and RemoteFunctions
- DataStore design and session-locked save systems
- Performance profiling and memory optimization
- Tooling and plugins to speed up the rest of the team

### Tooling

```
Languages      Luau, Lua
Engine         Roblox Studio
Workflow       Rojo, Wally, Git
Frameworks     Knit, ProfileService, ProfileStore
Testing        TestEZ
```

### A bit of how I write code

```lua
local ProfileStore = require(ServerScriptService.Packages.ProfileStore)

local PlayerData = {}
PlayerData.__index = PlayerData

local PROFILE_TEMPLATE = {
    Coins = 0,
    Level = 1,
    Inventory = {},
}

function PlayerData.new(store, player)
    local self = setmetatable({}, PlayerData)

    self.Player = player
    self.Profile = store:StartSessionAsync(`player_{player.UserId}`, {
        Cancel = function()
            return player.Parent ~= game.Players
        end,
    })

    if not self.Profile then
        player:Kick("Your data failed to load. Please rejoin.")
        return nil
    end

    self.Profile:AddUserId(player.UserId)
    self.Profile:Reconcile()

    return self
end

return PlayerData
```


<p align="center"><i>Always shipping. Always refactoring.</i></p>
