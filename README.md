# How to add a new elemental type to cassette beasts
# Disclaimer
This guide assumes you already read the [Cassette Beasts developer guide](https://wiki.cassettebeasts.com/wiki/Modding:Mod_Developer_Guide) and have already made the first steps in making a cassette beasts mod.

Note that this way of making a modded type is **NOT SAFE TO REMOVE** at all, due to changing some files directly.

This guide currently covers:
- [How to add files that are not in the mod folder in your mod](#metadata-inclusion).
- [How to add a simple custom type](#making-the-type).
- [How to add elemental reactions](#adding-the-reactions).
- [How to fix issues due to the new type](#fixing-bugs).
- [How to add new status effects](#adding-status-effects).

### Needed mods
Before making the mod, be sure to download these two mods and put them in your res://mods folder (**not as a .pkg file!!!!**)
- [Mod utils](https://github.com/Yukitty/CassetteBeasts-modutils)
- [Modded type chart fix](https://github.com/UMshutup/modded_type_chart)

## Metadata inclusion
**EVERY** file you add outside the mod folder are required to have their path referenced in the metadata.tres of your mod, otherwise it will work only in the editor.

<img width="437" height="229" alt="image" src="https://github.com/user-attachments/assets/c90dd998-ac46-4943-a12d-cfd6dfeb6564" />

This includes all of the types and elemental reactions and modified files outside the folder.

## Making the type
Before you start, be sure to have these things in the folder of your mod:
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

Be sure to add the file path in the metadata.tres!

## Adding the reactions
Now, this part is a little tedious as every reaction needs its own file.
Go to the elemental reactions folder (res://data/elemental_reactions/) and duplicate any file, for the name you should put **mod_** at the start to avoid losing track of them.
Heres what it should look like in the inspector:
<img width="436" height="257" alt="tutorial 3" src="https://github.com/user-attachments/assets/d7f07e0b-b13d-4243-8b40-e48ba3b7035c" />

Now its time to make it unique, heres what you should add for each value:
- **Attacker**: The type of the attacker (in other words who deals damage). Drag the elemental type from the types folder here.
- **Defender**: The type of the defender (in other words who takes damage). Drag the elemental type from the types folder here.
- **Result**: This is an array of Status effects that will be added to the defender after an attack, you can put as many as you want, just don't confuse a move resource with a status effect (you can find status effects here: res://data/status_effects/)
- **Varied result amount**: this is an array of numbers, each corresponding to the status effect, it will change the amount of the stat randmly by that number
- **Default result amount**: this will determine the amount of turns the status effects will last
- **Result hint**: This is the color of the hint for the reaction, "negative" is red and used for debuffs, "transmutation" is used for type changes and neutral effects, "positive" is for buffs
- **Toast message**: This is the little text that appears above a character when getting hit by an elemental reaction

Now repeat this step until you are happy with all the reactions!
Be sure to add the files paths in the metadata.tres!

## Fixing bugs
Now, due to how Cassette beasts handles type variations in certain moves, you will have to add your own variations... You can either add new vfx for each type in some moves or re-use existing types of vfx.

Heres an example, using the fusion power move, to avoid a crash when generating the name (found here res://data/battle_moves/fusion_power.tres):

First, doubleclick fusion_power.tres and find this array (Name prefixes):
<img width="821" height="295" alt="image" src="https://github.com/user-attachments/assets/816750f8-5791-43c3-9886-1a75709ce650" />

Now exand it and you will see every type variation for the name prefix

At the bottom you should find two new slots, click the pencil icon on the left to add a data type:
- in the first, add a string, and **Name it with the id of your type!**
- in the second add a "PoolStringArray", and fill it with name prefixes for the fusion move

**DONT FORGET TO CLICK ADD VALUE! OTHERWISE IT WILL NOT ADD IT!**

Now heres the same thing but for vfx, using The sword fusion power (res://data/attack_vfx/fusion_sword.tres)
- Find this array (Type cases):
- In the first, use string and add the Type id
- In the second, use "Object" and add a VFX .tres file, lets just use a pre-existing one for now. (res://data/attack_vfx/fusion_sword_metal.tres)
**DONT FORGET TO CLICK ADD VALUE! OTHERWISE IT WILL NOT ADD IT!**

Do the same for res://data/attack_vfx/fusion_axe.tres

## Adding status effects
Due to how cassette beasts handles some moves its necessary to add three status effects for each type
- a new coating
- a new wall
- a new contact damage

Locate the status effect folder (res://data/status_effects/) and duplicate a coating, a wall and a contact damage
For everyone of them, locate in the inspector and change only these values:
- **Name**: the status effect name
- **Tags**: the move tags, cassette beasts handles what moves go on specific beasts by using tags, you can find them [here](https://wiki.cassettebeasts.com/wiki/Category:Move_Tags)
- **Icon**: self explanatory

For a coating, change these values:
- **Elemental types**: drag here your custom type, this will make the monster turn into that type when the status effect is applied
Then go to res://data/battle_moves/coating_elemental.tres, and add to type cases the type id and the coating.tres of the new type

For contact damage, change these values:
- **Damage Type**: the type of damage it will deal, drag your custom type here.
then go to res://data/battle_moves/sharp_edges.tres and change Damage on contact statuses by adding your type id and the status effect.

For walls, this is a little harder! Especially if you want a custom appearance...
In the github theres should be a .ase file that is a template

