# Unsorted

These are functions that aren't in any specific table.

---

#### `Maybe<LuaFunction>, Maybe<String>` loadstring(`String` source, [`String` name, [`LuaValue` env]])

Compiles the provided **source** and returns it as a callable function.
If there are any syntax errors, returns `nil` and the error as a string instead.

- **name** is used for error messages, the default is the name of the script that called `loadstring`.
- **env** is used as the environment of the returned function, the default is `_ENV`.

---

# Root

The root table now contains extra asset bindings and bindings to return the tile variant that is used for material and matmods at any position.

---

#### `String[]` root.assetsByExtension(`String` extension)

Returns an array containing all assets with the specified file extension.

By the way, here's a list of every file extension the game does Special Things™ for when loading assets.

<details><summary><b>File Extensions</b></summary>

- Items: `item`, `liqitem`, `matitem`, `miningtool`, `flashlight`, `wiretool`, `beamaxe`, `tillingtool`, `painttool`, `harvestingtool`, `head`, `chest`, `legs`, `back`, `currency`, `consumable`, `blueprint`, `inspectiontool`, `instrument`, `thrownitem`, `unlock`, `activeitem`, `augment`
- Materials: `material`, `matmod`
- Liquids: `liquid`
- NPCs: `npctype`
- Tenants: `tenant`
- Objects: `object`
- Vehicles: `vehicle`
- Monsters: `monstertype`, `monsterpart`, `monsterskill`, `monstercolors`
- Plants: `modularstem`, `modularfoliage`, `grass`, `bush`
- Projectiles: `projectile`
- Particles: `particle`
- Name Gen: `namesource`
- AI Missions: `aimission`
- Quests: `questtemplate`
- Radio Messages: `radiomessages`
- Spawn Types: `spawntypes`
- Species: `species`
- Stagehand: `stagehand`
- Behaviors: `nodes`, `behavior`
- Biomes: `biome`, `weather`
- Terrain: `terrain`
- Treasure: `treasurepools`, `treasurechests`
- Codex Entries: `codex`
- Collections: `collection`
- Statistics: `event`, `achievement`
- Status Effects: `statuseffect`
- Functions: `functions`, `2functions`, `configfunctions`
- Tech: `tech`
- Damage: `damage`
- Dances: `dance`
- Effect Sources: `effectsource`
- Command Macros: `macros`
- Recipes: `recipe`
</details>

#### `String` root.assetData(`String` path)

Returns the raw data of an asset.

#### `String, Maybe<LuaTable>` root.assetOrigin(`String` path, [`bool` getPatches])

Returns the asset source path of an asset, or nil if the asset doesn't exist. If you specify getPatches as true then also returns the patches for the asset as an array, each element containing the source path and patch path in indexes 1 and 2 respectively.

#### `LuaTable` root.assetSourcePaths([`bool` withMetadata])

Without metadata: Returns an array with all the asset source paths.
With metadata: Returns a table, key/value being source path/metadata.

#### `Image` root.assetImage(`String` image)

Returns an image.

#### `Json` root.assetFrames(`String` imagePath)

Returns an array containing a `file` (the frames file used for the image) and `frames` (the frame data of the image).

#### `JsonArray` root.assetPatches(`String` asset)

Returns a list of asset sources which patch the specified asset and the paths to those patches.

---

#### `Json` root.getConfiguration(`String` key)

Gets a configuration value in `/storage/starbound.config`.

#### `Json` root.getConfigurationPath(`String` path)

Gets a configuration value in `/storage/starbound.config` by path.

*Both getters will error if you try to get `title`, as that can contain the player's saved server login.*

#### `Json` root.setConfiguration(`String` key, `Json` value)

Sets a configuration value in `/storage/starbound.config`.

#### `Json` root.setConfigurationPath(`String` path,  `Json` value)

Sets a configuration value in `/storage/starbound.config` by path.

*Both setters will error if you try to set `safeScripts`, as that can break Starbound's sandbox.*

---

#### `JsonArray` root.allRecipes()

Returns all recipes.

---
# Interface

The interface table contains bindings which allow scripts to display a message at the bottom of the screen, among other things.

#### `void` interface.queueMessage(`String` message, [`float` cooldown, [`float` springState]])

Queues a message popup at the bottom of the screen with an optional **cooldown** and **springState**.

#### `void` interface.setHudVisible(`bool` visible)

Sets the HUD's visibility.

#### `bool` interface.hudVisible()

Returns the HUD's visibility.

#### `PaneId` interface.bindRegisteredPane(`string` paneName)
Binds a registered pane (defined in `/source/frontend/StarMainInterfaceTypes`) to a Lua value, which can then call widget functions on that pane.
<details><summary><b>Panes</b></summary>
EscapeDialog<br>
Inventory<br>
Codex<br>
Cockpit<br>
Tech<br>
Songbook<br>
Ai<br>
Popup<br>
Confirmation<br>
JoinRequest<br>
Options<br>
QuestLog<br>
ActionBar<br>
TeamBar<br>
StatusPane<br>
Chat<br>
WireInterface<br>
PlanetText<br>
RadioMessagePopup<br>
CraftingPlain<br>
QuestTracker<br>
MmUpgrade<br>
Collections<br>
</details>

#### `void` interface.displayRegisteredPane(`string` paneName)
Displays a registered pane.


#### `?` interface.bindCanvas()
TODO


#### `int` interface.scale()
Returns the scale used for interfaces.


---

# World

The world table now contains extra bindings.

---

#### `bool` world.isServer()

Returns whether the script is running on the server or client.

---

#### `bool` world.isClient()

Returns whether the script is running on the server or client.

---

The following additional world bindings are available only for scripts running on the client.

---

#### `entityId` world.mainPlayer()

Returns the entity ID of the player hosting the world.

---

#### `Vec2F` world.entityAimPosition(`entityId` entityId)

Returns the current cursor aim position of the specified entity.

---

#### `bool` world.inWorld()

Returns whether any players are in the world.

---

The following additional world bindings are available only for scripts running on the server.

---

#### `void` world.setExpiryTime(`float` expiryTime)

Sets the amount of time to persist a ephemeral world when it is inactive.

---

#### `string` world.id()

Returns a `String` representation of the world's id.

---

#### `?` world.callScriptContext(`?` ?)

TODO

---

#### `?` world.sendPacket(`?` ?)

?

---

# Player

The player table now contains bindings which contains functions to save/load, access and modify the player's identity, mode, aim, emote and more.

---

#### `Json` player.save()

Serializes the player to Json the same way Starbound does for disk storage and returns it.

#### `void` player.load(`Json` save)

Reloads the player from a Json **save**. This will reset active ScriptPanes and scripts running on the player.
  
---

#### `String` player.name()

Returns the player's name.

#### `void` player.setName(`String` name)

Sets the player's name.

---

#### `String` player.description()

Returns the player's description.

#### `void` player.setDescription(`String` description)

Sets the player's description. The new description will not be networked buntil the player warps or respawns.

---

#### `void` player.setSpecies(`String` species)

Sets the player's species. Must be a valid species.

---

#### `void` player.setGender(`String` gender)

Sets the player's gender.

---

#### `String` player.imagePath()

If the player has a custom humanoid image path set, returns it. otherwise, returns `nil`.

#### `void` player.setImagePath(`String` imagePath)

Sets the player's image path. Specify `nil` to remove the image path.

---

#### `Personality` player.personality()

Returns the player's personality as a `table` containing a `string` idle, `string` armIdle, `Vec2F` headOffset and `Vec2F` armOffset.

#### `void` player.setPersonality(`Personality` personality)

Sets the player's personality. The **personality** must be a `table` containing at least one value as returned by `player.personality()`.

---

#### `String` player.bodyDirectives()

Returns the player's body directives.

#### `void` player.setBodyDirectives(`String` bodyDirectives)

Sets the player's body directives.

---

#### `String` player.emoteDirectives()

Returns the player's emote directives.

#### `void` player.setEmoteDirectives(`String` emoteDirectives)

Sets the player's emote directives.

---

#### `String` player.hair()

Returns the player's hair group.

#### `void` player.setHair(`String` hairGroup)

Sets the player's hair group.

---

#### `String` player.hairType()

Returns the player's hair type.

#### `void` player.setHairType(`String` hairType)

Sets the player's hair type.

---

#### `String` player.hairDirectives()

Returns the player's hair directives.

#### `void` player.setHairDirectives(`String` hairDirectives)

Sets the player's hair directives.

---

#### `String` player.facialHair()

Returns the player's facial hair type. Same as player.facialHairType?

#### `void` player.setFacialHair(`String` facialHairGroup, `String` facialHairType, `String` facialHairDirectives)

Sets the player's facial hair group, type, and directives.

---

#### `String` player.facialHairType()

Returns the player's facial hair type.

#### `void` player.setFacialHairType(`String` facialHairType)

Sets the player's facial hair type.

---

#### `String` player.facialHairGroup()

Returns the player's facial hair group.

#### `void` player.setFacialHairGroup(`String` facialHairGroup)

Sets the player's facial hair group.

---

#### `String` player.facialHairDirectives()

Returns the player's facial hair directives.

#### `void` player.setFacialHairDirectives(`String` facialHairDirectives)

Sets the player's facial hair directives.

---

#### `String` player.facialMask()

Returns the player's facial mask group.

#### `void` player.setFacialMask(`String` facialMaskGroup, `String` facialMaskType, `String` facialMaskDirectives)

Sets the player's facial mask group, type, and directives.

---

#### `String` player.facialMaskDirectives()

Returns the player's facial mask directives.

#### `void` player.setFacialMaskDirectives(`String` facialMaskDirectives)

Sets the player's facial mask directives.

---

#### `PlayerMode` player.mode()

Returns the player's mode.

#### `void` player.setMode(`String` mode)

Sets the player's mode. **mode** must be either `"casual"`, `"survival"` or `"hardcore"`.

---

#### `Color` player.favoriteColor()

Returns the player's favorite color.
It is used for the beam shown when wiring, placing, and highlighting with beam-tools (Matter Manipulator).

#### `void` player.setFavoriteColor(`Color` color)

Sets the player's favorite color. **color** can have an optional fourth value for transparency.

---

#### `Vec2F` player.aimPosition()

Returns the player's aim position.

---

#### `void` player.emote(`String` emote, [`float` cooldown])

Makes the player do an emote with the default cooldown unless a **cooldown** is specified.

#### `String, float` player.currentEmote()

Returns the player's current emote and the seconds left in it.
  
---

#### `unsigned` player.actionBarGroup()

Returns the player's active action bar.
  
#### `void` player.setActionBarGroup(`unsigned` barId)
  
Sets the player's active action bar.
  
#### `Variant<unsigned, EssentialItem>` player.selectedActionBarSlot()

Returns the player's selected action bar slot.
  
#### `void` player.setSelectedActionBarSlot(`Variant<unsigned, EssentialItem>` slot)
  
Sets the player's selected action bar slot.
  
#### `void` player.setDamageTeam(`DamageTeam` team)
  
Sets the player's damage team. This must be called every frame to override the current damage team that the server has given the player (normally controlled by /pvp)

---

#### `void` player.say(`String` line)

Makes the player say a string.

---

#### `Json` player.humanoidIdentity()

Returns the specific humanoid identity of the player, containing information such as hair style and idle pose.

#### `void` player.setHumanoidIdentity(`Json` humanoidIdentity)

Sets the specific humanoid identity of the player.

---

#### `ItemDescriptor` player.item(`ItemSlot` itemSlot)

Returns the contents of the specified itemSlot.

#### `void` player.setItem(`ItemSlot` itemSlot, `ItemDescriptor` item)

Puts the specified item into the specified itemSlot.
Item slots in item bags are structured like so: `{String bagName, int slot}`

---

#### `int` player.itemBagSize(`String` itemBagName)

Returns the size of an item bag.

#### `bool` player.itemAllowedInBag(`String` itemBagName, `ItemDescriptor` item)

Returns whether the specified item can enter the specified item bag. 

---

#### `ActionBarLink` player.actionBarSlotLink(`int` slot, `String` hand)

Returns the contents of the specified action bar link slot's specified hand.

#### `bool` player.setActionBarSlotLink(`int` slot, `String` hand, `ItemSlot` itemSlot)

Links the specified slot's hand to the specified itemSlot.

---

#### `Float` player.interactRadius()

Returns the player's interact radius.

#### `void` player.setInteractRadius(`Float` interactRadius)

Sets the player's interact radius. This does not persist upon returning to the main menu.

---

#### `JsonArray` player.availableRecipes()

Returns all the recipes the player can craft with their currently held items and currencies.

---
#### `String` player.currentState()

Returns the player's current movement state.

<details><summary><b>Player States</b></summary>
idle<br>
walk<br>
run<br>
jump<br>
fall<br>
swim<br>
swimIdle<br>
lounge<br>
crouch<br>
teleportIn<br>
teleportOut<br>
</details>
---

#### `List<Json>` player.teamMembers()

Returns an array, each entry being a table with `name`, `uuid`, `entity`, `healthPercentage` and `energyPercentage`

---

# Renderer

The new renderer table is accessible from almost every clientside script and allows configuring shaders.

---

#### `void` renderer.setPostProcessGroupEnabled(String group, bool enabled, [bool save])

Enables or disables a post process shader group. If save is true, this change is saved to configuration as well.

---

#### `bool` renderer.postProcessGroupEnabled(String group)

Returns true if the specified post process group is enabled.

---

#### `Json` renderer.postProcessGroups()

Returns every post process group. Identical to grabbing them from client.config with root.assetJson.

---

#### `Json` renderer.setEffectParameter(String effectName, String parameterName, RenderEffectParameter value)

Sets the specified scriptable parameter of the specified shader effect to the provided value. 
This is accessed from the shader as a uniform and must be defined in the effect's configuration.

---

#### `RenderEffectParameter` renderer.getEffectParameter(String effectName, String parameterName)

Returns the specified scriptable parameter of the specified shader effect.

---
