# How to add a new elemental type to cassette beasts
# Disclaimer
This guide assumes you already read the [Cassette Beasts developer guide](https://wiki.cassettebeasts.com/wiki/Modding:Mod_Developer_Guide) and have already made the first steps in making a cassette beasts mod.

Note that this way of making a modded type is **NOT SAFE TO REMOVE** at all, due to changing some files directly.

This guide currently covers:
- [How to add a simple custom type](#making_the_type).
- [How to add elemental reactions](#adding_the_reactions).
- [How to add elemental hit effects](#adding_the_reactions).
- [How to fix issues due to the new type](#fixing_bugs).

### Needed mods
Before making the mod, be sure to download these two mods and put them in your res://mods folder (**not as a .pkg file!!!!**)
- [Mod utils](https://github.com/Yukitty/CassetteBeasts-modutils)
- [Modded type chart fix](https://github.com/UMshutup/modded_type_chart)

## Making the type
Before you start, be sure to have these things:
- An icon for the elemental type
- A palette for the elemental type
- A palette for elemental effects

Now, in the godot editor, go to the elemental types folder (res://data/elemental_types/), you should see all the elemental types in the game.
Adding a new type, for now, is pretty simple: just duplicate any existsing type, rename it how you want and double click it, on the inspector you should see this:

<img width="439" height="302" alt="tutorial 1" src="https://github.com/user-attachments/assets/4cd2446c-e318-4f51-ab4a-edcbe2089a4f" />
