# FFXI Lua Metadata

This repository will contain a series of supplemental Lua metadata for use in the development of addons for Windower 4.

### Available Resources

#### Trusts

Trust metadata is meant to supplement what's already available via `spells` resource where `type` is "Trust". Most notably, it contains information about the main and sub jobs for each trust in the game, keyed by the spell id. For usability, it also duplicates the spell name and party name fields from the base resource.

Each entry in this table will include the following fields:

| Field name      | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| id              | The id of the spell used to call this trust                  |
| name            | The name of the spell used to call this trust                |
| en              | The name of the spell used to call this trust (English client) |
| ja              | The name of the spell used to call this trust (Japanese client) |
| party_name      | The name of the trust called by this spell when in a party   |
| model           | The model number of this trust when in a party               |
| main_job        | The three-character shorthand for the trust's main job (i.e. WAR) |
| main_job_id     | The unique id (from the `jobs` resource) of the trust's main job |
| sub_job         | The three-character shorthand for the trust's sub job (i.e. MNK) |
| sub_job_id      | The unique id (from the `jobs` resource) of the trust's sub job |
| non_interactive | A flag indicating whether the trust is non-interactive (i.e. Kupofried) |

Again, this information is all keyed using the id of the spell that calls the respective trust.