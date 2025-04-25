# FFXI Lua Metadata

This repository will contain a series of supplemental Lua metadata for use in the development of addons for Windower 4.

### Available Resources

#### Buffs

Buff metadata allows you to find buffs by name, but it goes beyond that. Many buffs have more than one associated id, and we expose an interface that allows you to perform several common tasks:



- `buff_meta:get_ids_by_name(name)` - With a buff name, find the id of all buffs which share that name.

- `buff_meta:get_with_shared_name_by_id(id)` - With a buff id, find the id's of all buffs that share that name.

- `buff_meta:has_buff(name, buffs)` - With a buff name and an array of active buffs (such as the one obtained via `windower.ffxi.get_player().buffs`), determine if that buff is active. This internally accounts for any buffs with multiple id's, and will return the specific id that triggerd the match on success. **In most cases, this will be the only function you'll likely be using.**



The following shows how you can use this in your own Lua:

```lua
local buff_meta = require('meta/buffs')

...

local player = windower.ffxi.get_player()
local paralyzed = buff_meta:has_buff('Paralysis', player.buffs)
if paralyzed then
  print('I am paralyzed!')
  -- TODO: Other more interesting things should go here
end
```



#### Trusts

Trust metadata is meant to supplement what's already available via `spells` resource where `type` is "Trust". Most notably, it contains information about the main and sub jobs for each trust in the game, keyed by the spell id. For usability, it also duplicates the spell name and party name fields from the base resource.

Each entry in this table will include the following fields:

| Field name      | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| id              | The id of the spell used to call this trust                             |
| name            | The name of the spell used to call this trust                           |
| en              | The name of the spell used to call this trust (English client)          |
| ja              | The name of the spell used to call this trust (Japanese client)         |
| party_name      | The name of the trust called by this spell when in a party              |
| model           | The model number of this trust when in a party                          |
| main_job        | The three-character shorthand for the trust's main job (i.e. WAR)       |
| main_job_id     | The unique id (from the `jobs` resource) of the trust's main job        |
| sub_job         | The three-character shorthand for the trust's sub job (i.e. MNK)        |
| sub_job_id      | The unique id (from the `jobs` resource) of the trust's sub job         |
| non_interactive | A flag indicating whether the trust is non-interactive (i.e. Kupofried) |

Again, this information is all keyed using the id of the spell that calls the respective trust.
