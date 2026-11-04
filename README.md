# How to add a new elemental type to cassette beasts
# Disclaimer
This guide assumes you already read the [Cassette Beasts developer guide](https://wiki.cassettebeasts.com/wiki/Modding:Mod_Developer_Guide) and have already made the first steps in making a cassette beasts mod.

Note that this way of making a modded type is **NOT SAFE TO REMOVE** at all, due to changing some files directly.

This guide currently covers:
- [How to add a simple custom type](#making-the-type).
- [How to add elemental reactions](#adding-the-reactions).
- [How to add elemental hit effects](#adding-the-reactions).
- [How to fix issues due to the new type](#fixing-bugs).

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
Adding a new type, for now, is pretty simple: just duplicate any existing type, rename it how you want and double click on it, on the inspector you should see this:

<img width="439" height="302" alt="tutorial 1" src="https://github.com/user-attachments/assets/4cd2446c-e318-4f51-ab4a-edcbe2089a4f" />

Now its time to make it a different type, heres what you should do to each value:
- **ID**: The unique identifier of your custom type, it has to be different to the other types, use only lowercase letters.
- **NAME**: The in-game name, you can use a normal string (just write the name) or you can use translation strings.
- **Sort order**: This makes the type have priority in the type chart instead of being in alphabetical order, all types besides glass and glitter are 0, glass is 1 and glitter is 2, if you want your type to be after the common types make this number higher.
- **Palette**: This will determine the colors a bootleg will have if its your new elemental type, be sure to use 5 gradient colors, from darker to lighter (if you want, you can add additional 5 types to change another color in a bootleg monster!)
- **VFX palette**: Same as the Palette, but this time its used for the vfx of typeless moves (such as spit), it uses 4 colors.
- **Sparkle**: This adds the same shader that glitter has to the palette
- **Loot table**, Leave this empty!

## Adding the reactions
Now, this part is a little tedious as every reaction needs its own file.
Go to the elemental reactions folder (res://data/elemental_reactions/) and duplicate any file, for the name you should put **mod_** at the start to avoid losing track of them.
Heres what it should look like in the inspector:
<img width="436" height="257" alt="tutorial 3" src="https://github.com/user-attachments/assets/d7f07e0b-b13d-4243-8b40-e48ba3b7035c" />
Now its time to make it unique, heres what you should add for each value:
- **Attacker**: The type of the attacker (in other words who deals damage). Drag the elemental type from the types folder here.
- **Defender**: The type of the defender (in other words who takes damage). Drag the elemental type from the types folder here.
- **Result**: This is an array of Status effects that will be added to the defender after an attack, you can put as many as you want, just don't confuse a move resource with a status effect (you can find status effects here: res://data/status_effects/)
- 


