# ZQuest Classic: 2.55 Development Summary
ZQuest Classic has grown by a ***huge*** amount between 2.50.2/2.53 and 2.55 versions. There are many new features, for gameplay, editing, ui, ease-of-use, scripting, and really every possible part of the engine you could imagine. Here, I'm going to go through each feature in some amount of depth to show what's new.

* [Editor](#editor)
   * [GUI changes](#gui-changes) 
   * [Drawing Modes](#drawing-modes)
 * [Player](#player)
 * [New Quest Features](#new-quest-features)
   * [New Combo Features (all types)](#new-combo-features-all-types)
   * [Real Dark Rooms](#real-dark-rooms)
   * [Pitfalls](#pitfalls)
   * [New Pushblock Features](#new-pushblock-features)
   * [Light Beam Puzzles](#light-beam-puzzles)
   * [Chests / Lockblocks](#chests-lockblocks)
   * [Other Combo Types](#new-combo-types)

## Editor
### GUI changes
Previously, ZQ had 'Small Mode' and 'Large Mode'. This divide could no longer be feasibly supported, mainly because small mode's base resolution was simply too small to fit the GUI for many of the new features, requiring us to make entirely separate GUIs for small mode, which was simply too much work to keep up. However, numerous users took issue with this from an accessibility standpoint, as the large mode GUI had a lot of spots where text was too small to read for some, among other issues. As such, BOTH of these modes have recieved a giant overhaul, to create a brand new and more customizable GUI.

<img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162485199477682338/compact.png?ex=653c1bb5&is=6529a6b5&hm=81bdc3963037226cd4fc6f1a0cdd6414fc59e6d25cbb0c73505013bb2b05940f&" alt="Screenshot of the editor, set to compact mode" width="50%" height="50%"/><img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162485199767085086/expand.png?ex=653c1bb5&is=6529a6b5&hm=2e73a19a27318427f1b9ee0b0fc41ff35ae4f681c5bf2dd1295eadbe9ba7b6af&" alt="Screenshot of the editor, set to expanded mode" width="50%" height="50%"/>

Pictured above on the left is compact mode, and on the right is expanded mode. The `< Expand` / `> Compact` button in the top bar toggles between these modes. Since both modes use the *exact same window size*, many things can be easily supported between them, including switching without the need to relaunch the entire program. Additionally, there are several other minor toggles that you can use in the GUI.

* The `<|>` / `>|<` button above the combo columns allows you to toggle how many columns show. This toggles between 1/2 in compact, and 2/4 in expanded. Obviously, less columns means they have room to display larger, making them easier to read- while more columns gives you more combos usable at once.
* The `+` / `-` button near the `Favorites` functions similarly, allowing more to be shown at once at the cost of being smaller, or vice-versa.
* The `<` / `>` buttons near the `Favorites` allow you to change *pages*, because there are now multiple pages of favorites. Right-clicking these buttons allows you to jump straight to a specific page.
* The `+` / `-` button near the `Favorite Commands`... also functions similarly, allowing more or less commands to show. Some of the text may be cut off (abbreviated with `...`) if it cannot fit, which is more of a problem when showing more commands- though hovering over a command with tooltips enabled will display a tooltip of the full text.
* The `X` buttons near the `Favorites` and `Favorite Commands` respectively, clear all favorites/favorite commands (with an `Are you sure?` popup to prevent accidental deletion)
* The `SWP` button, *only available in Compact mode*, changes the bottom pane to work more similarly to the old small-mode pane, only displaying one set of: `4 warp return squares`, `item + stairs + green square + flags`, or `screen's enemies` at a time, with up/down arrows to cycle between these 3 panels. (This allows the text here to be larger and more readable, if you find it too small to read otherwise).
* By right-clicking on the minimap, you can *zoom in* on it, making it much larger. While it is zoomed, any click that is not on the minimap will un-zoom, as will pressing `Esc`, or right-clicking again.<br/><img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162493082009354270/compact_zoomed_minimap.png?ex=653c230c&is=6529ae0c&hm=d19a72b31cc44ebad7bc1935c7165f28e8fbfd4d6168648d18e3b297cdb2b12b&" alt="Screenshot of the editor, with the minmap zoomed in, in compact mode." width="50%" height="50%"/>
* In `Etc->Options`, you can change what fonts are used by various portions of the program. The default font is larger than it used to be, to improve readability. NOTE: Some older dialog windows will have overlapping text as a result of this, such sections need to be upgraded eventually to be able to handle variable font size, but just haven't been gotten to yet.

### Drawing Modes
Previously, you had to cycle through drawing modes one-by-one using the draw mode button in the upper-right. But now, you can simply right-click on the draw mode button to pop up a selector menu.<br/><img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162494416603324607/drawmode_rclick.png?ex=653c244b&is=6529af4b&hm=0c0a7342131077782882af566b63ca5f577e7ff00f83c7dcf22f6744559b5a37&" alt="Screenshot of the drawing mode dropdown" width="50%" height="50%"/>

Additionally, you may notice that the available drawing modes have changed.
* Normal drawing mode, for placing combos just as normal.
* Alias drawing mode is mostly unchanged.
* Pool drawing mode is entirely new; combo pools are weighted collections of combos, and when drawn on the screen, a random combo is selected from the pool for each position. This is useful for randomized decorations, like cracked/mossy/etc floor tiles, or variety in flowers/grass. Actions like floodfill (`Ctrl+Click`) work as expected, filling each position with a separately randomized combo. Undo/Redo do not re-randomize, though placing the pool again obviously will.<br/><img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162496106056388799/combopool.png?ex=653c25dd&is=6529b0dd&hm=f63e8fa647180c16b8db5e3f07c7fc4c57ee16a55fd793a569e83466220189be&" alt="Screenshot of the combo pool editor" width="50%" height="50%"/>
* Auto Combo drawing mode has some brand-new features, as well as everything the old `Relational` and `Dungeon Carving` modes had, merged into one mode. This allows you to set up specificly-laid-out sets of combos, and chooses which combos to place smartly based on the surrounding combos on the screen. This can be used to automatically draw entire mountains, lakes, etc, automatically handling the edges/corners for you as you draw.<br/><img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162497044045365340/autocombo.png?ex=653c26bd&is=6529b1bd&hm=d7dfbdacc62ca22758c20d592f858c965500565b8fa0fa9f45fe4ff0f62fa7b2&" alt="Screenshot of the auto combo editor" width="50%" height="50%"/>

## Player

## New Quest Features
There are plenty of new features that can be used in your quests. Some used to be popularly scripted, but are now in engine; others are brand-new ideas that were added. Altogether the focus when adding new features has been to give questmakers all the options we possibly can. This does have the effect of some systems being more difficult to learn, though in most cases we try to aim for "easy to use, difficult to master".

Features below are not listed in any particular order, though I will attempt to group similar features together.
### New Combo Features (all types)
Combos in general have been improved drastically.
* Each combo type has up to 8 attribytes (0 to 255 values), 8 attrishorts (-32768 to +32767 values), 4 attributes (-214748.3648 to +214748.3647 values), and 16 flags (checkboxes) for custom configuration that is specific to the combo type. Not all of these type-specific features will be covered in this summary, as many of the features are simple small customizations of the type (like damage dealt by damage combos, conveyor speed and direction, etc). Many combo types have a special "Wizard" dialog available via a button in the combo editor which is designed to make these easier to set up.
* Every combo has checkboxes for if they are hookshot-grabbable or switch-hookable, allowing things like chests and signs to be hookable inherently.
* In addition to the solidity square, combos now have a green `Effect` square. By default this square is filled in, and any section that is NOT filled in acts as though it is `(None)` type, regardless of its' actual type.
* Every combo has a `General` tab, which currently has the following neat settings:
  * Speed modification settings (apply to the player when the combo is centered under the player)
  * Sprites / SFX that display / play in various conditions, such as when the combo appears onscreen, disappears from the screen, or is being walked/stood on by the player.
* Every combo has the `Triggers` tab, which allows for INSANELY powerful customization of the combo through various settings. Due to the sheer number of options on the triggers tab, it may be a bit confusing to navigate, but hopefully the many `?` buttons throughout should make it easier to navigate. Creating simple behaviors should be easy; ex. a `Step->Next` trigger could be created simply by checking the `Step->` flag, and setting the `Combo Change` value to `1`. (`Step->Previous` would be just as easy, instead using `-1` for the combo change).
  * Additionally, some combo types support the extra-special `->ComboType Effects` flag, which will cause an effect to occur related to the specific combo type. A great example of this is `Damage` combos, which will hurt the player when their `->ComboType Effects` trigger occurs (regardless of if the player is anywhere near the combo or not).
    * A great use of this specific interaction would be a damaging "Hot Room"- by simply combining a `Timer` trigger with the `->ComboType Effects` result (optionally using an inverted item condition to make it **only trigger if you do not have a specific item**), you have yourself a ticking damage hot room in any room the combo is placed in.
  * Going over every trigger available would make this summary far too long and complex, so have a look at the options yourself and play around with them! This system was designed with pure creativity in mind.
* Every combo also has a `Lifting` tab, related to the `Lift Glove` itemclass which allows the player to pick up combos above their head and throw them. This can be used for things like lifting pots or bomb flowers.
* And finally, combos now have their own script type which can be assigned to each combo.

### Real Dark Rooms
Enabled via the Quest Rule `New Dark Rooms`, this changes from the classic dark room style which darkens the entire palette, and changes to a style which allows circles/cones of light to reveal what's underneath the darkness.
* `Lantern` itemclass allows the player to cast a shape of your choice of light (from the options that have been implemented, which are currently `Circle`, `Cone`, and `Square`, as well as having a configurable size for the shape.
* `Torch` combo type functions similarly, but, placed instead of being the player's light.
* New dark rooms can be previewed in the editor via `View->Show Darkness` (default hotkey `L`)<br/><img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162503653563830402/image.png?ex=653c2ce5&is=6529b7e5&hm=de37cdbcbd1200bd1ca77ea49597e5a24692a5274c03862f0a6869f3f68f209d&" alt="Screenshot of the editor previewing a dark room" width="50%" height="50%"/>
* Various options are available in `Init Data->Vars` which can configure how new dark rooms look!<br/><img src = "https://cdn.discordapp.com/attachments/1162478250208022679/1162504184839540857/dark_initdata.png?ex=653c2d63&is=6529b863&hm=4da08e1db0abe4c344eb8517c1ce04bec5c514ed32fe4b749f79fc2c43e919d6&" alt="Init Data dialog, showcasing the settings related to dark rooms"/>
  * `Dither Type`/`Dither Arg` can be used to configure what dithering effect is used. Changing the 'type' will change the whole shape, such as checkerboard, vertical bars, diagonal bars, seemingly-random static, and more. Changing the 'arg' changes something ABOUT the shape, such as the size of each square of the checkerboard, width of each bar, thickness of the static, etc.
  * `Dither Percentage` indicates how much dithered light will be cast beyond normal light- ex. a circle of light with radius 32, with a dither percentage of 50, would cast a fully-clear 32 radius circle of light, and a dithered 48 radius circle of light (50% greater radius).
  * `Transp. Percentage` works similarly to `Dither Percentage`, except the larger radius that it casts is *transparent* rather than *dithered*, giving an alternative to how you want to cast light. Additionally, these settings can *combine*- if they were both 50% for example, the larger radius shape would be drawn transparently-dithered.
  * `Light Radius` is a default radius used by some objects, such as `Fire` type weapons.
  * `Darkness Color`, which defaults to a hardcoded system-black (will always be pure black in any tileset), is the color to use for the darkness itself.

### Pitfalls
The new `Pitfall` combo type acts as a classic bottomless pit, either dealing damage to you or possibly warping you somewhere (as if 'falling down a level'). The falling works similar to drowning mechanically, though has a separate `Falling` sprite. Enemies that fall use a sprite from `Quest->Graphics->Sprites->Misc Sprites`, while the player has a separate animation for this, which *regardless of animation style*, is 7 frames 10 speed animation, for a total of 70 frames duration.
The Hover Boots and Ladder are able to interact with pitfalls.

### Paired Switches
`Switch` and `Switch Block` combos together form what's needed for basic "red/blue switch blocks".
* You can have up to 32 pairs that are "level-specific" (per level), which can only toggle between `on` and `off` states
* You can have up to 256 that are "global" (quest wide), which can either be `on`/`off` toggles, or can be ***timed switches***, which toggle `on` for a set time before toggling back to `off` on their own.
* You can optionally set switch blocks to allow the player to walk along the tops of them if the player is inside them when they become solid. This additionally adds a "pseudo height layer" to the engine (not used by anything outside of these combos).

### New Pushblock Features
Multiple quest rules affect new push block features, of which there are several.
* Moving blocks can have "real solidity" (helps prevent clipping through a moving block, allows the block to *push enemies*)
* Blocks on layers can be pushed. These will use the undercombo *of that layer*, which will be placed *on that layer*. (Push flags must be on the layer, or inherent to the combo on the layer).
  * Blocks on layers have interesting interactions with triggers/block holes. There is a Quest Rule that makes them only interact with triggers/holes on the *same* layer as them, but if that is off, they interact with layers below them as well.
  * In this way, blocks can be pushed *over* a block trigger without "clicking into place" the instant it is on a trigger, and a block can "fall" into a hole on a lower layer.
* The `Push (Generic)` combo type is a new type of pushblock, which does NOT use push *flags* at all- instead, the ways in which it can be pushed are defined as part of the combo's attributes. These combos can be set to be pushable in many unique ways, such as "down up to 3 times and left up to 3 times, but not right or up", or "left up to 2 times, and you can undo the push by pushing it back to the right, but not past its' starting point".
* Sliding blocks can exist, either via a `Push (Generic)` with the `Icy Block` flag checked, or by any block sliding across `Icy Floor` combos with the `Slides Blocks` flag checked. (Currently, this is the ONLY use of `Icy Floor`, though more non-block-related uses are planned eventually)

### Light Beam Puzzles
<img src="https://cdn.discordapp.com/attachments/1162478250208022679/1162563996931600474/lightbeam.png?ex=653c6518&is=6529f018&hm=4b8b8ddd2d5cf6eec70a0b7442590f9b4156626d6e59154d9f383e84af0764ba&" alt="Screenshot of the player, showcasing a beam of light reflecting off of two mirrors before hitting a wall" width="50%" height="50%"/>

* Light Beams are shot out of `Spotlight` combos, in any of the 4 main directions, or aimed from the camera at the screen for a true "spotlight" effect. These beams will bounce off of any mirror combos and be duplicated by prism combos in the same way weapon reflection works.
* Beams continue until they exit the side of the screen or hit a solid combo. (Exception: the `Glass` combo type allows beams to pass through despite solidity)
* The `Light Trigger` combo type has two states, active and inactive. These combos must be set up in pairs, as the combo changes between the two combos in the pair when hit with a beam or when a beam stops hitting it. Each trigger can be required to either be activated by a beam, or activated by LACK of a beam. When all triggers onscreen are activated, the screen's secrets will trigger, and the screen's light beam state will be set, permanently "solving" the beam puzzle.
* Both `Spotlight` combos and `Light Trigger` combos can be given a `Trigger Set`, as a value from 0 to 32. These can be used for puzzles requiring "different colored beams affect their matching color targets" type logic.
  * Any `Spotlight` with a `Trigger Set` of `0` will trigger ANY `Light Trigger`.
  * Any `Light Trigger` with a `Trigger Set` of `0` will be triggered by ANY `Spotlight`.
  * `Trigger Set` of 1 through 32 are unique, and only interact with their matching number (or number 0).
* Additionally, the new `Mirror (Custom)` combo can be configured to create custom reflections, such as "Anything coming from above, below, or the right is reflected to the left; anything coming from the left passes through to the right". You can set which direction out a light beam (or reflected weapon) will go for each input direction, fully customly. 

### Chests / Lockblocks
* Chests can be given specific items, rather than being set per-screen
* Can use one of 32 "Ex States" instead of the normal chest/lockblock states, allowing up to 32 extra chests/lockblocks that can be on the same screen
* Each of the 4 directions can be set as interactable or not (as opposed to chests only being openable from below)
* Any combination of the buttons A,B,L,R,Ex1-Ex4 can be set as interaction buttons for the combo. If any are set, the chest/block will open when that button is pressed while facing it from a valid side instead of when walking into it from a valid side.
  * You can set a "Prompt Combo" which will display at a given x,y offset from the player (ex. above the player's head) when they are able to interact with it. For locked chests/blocks, you can also set a secondary combo to display *instead* when you are unable to unlock them.
* Locked chests/blocks can be given various lock settings, instead of just "1 key unlocks it"
* Locked chests/blocks can be given a message string to display when the player tries and fails to unlock it (ex. "You do not have a Small Key!")

### New Combo Types
* `Block Weapon (Custom)` can block any variety of weapons as set in the `Triggers` tab
* `Bridge` combos can "cover up" combos on layers below them (making the covered combos solidity and type-effects not occur)
* `Button Prompt` combos can display a prompt (ex. above player's head) when faced
* `Cutscene Trigger` combos, combined with the `Triggers` tab features, can enter/exit a "cutscene mode" that can disable various player inputs
* `Glass` combos allow [Light Beams](#light-beam-puzzles) to pass through even when solid
* `Icy Floor` combos allow customizable slipperiness. Currently, only implemented to be able to slip Pushblocks, though more features are planned.
* `Light Trigger` combos can trigger secrets as part of [Light Beam Puzzles](#light-beam-puzzles)
* `Liquid` combos are not new- `Water` was just renamed. Though, there are a LOT more features to it now, including being able to passively heal or damage the player. (`Shallow Liquid` was changed from `Shallow Water` similarly)
* `Mirror (Custom)` combos can reflect weapons/light beams in fancy custom ways based on directions.
* [`Pitfall` combos](#pitfalls) act as bottomless pits, with falling similar to drowning.
* `Push (Generic)` combo types allow fancy custom [pushblock](#new-pushblock-features) stuff
* `Shooter` combos act as turrets. They can fire either automatically at a fixed or variable rate, or via `Triggers` tab `->ComboType Effects` flag. They can either fire friendly (player) weapons, or harmful (enemy) weapons.
* `Signpost` combos can be read, either by walking into them or via any combination of the buttons A,B,L,R,Ex1-Ex4, configured the same way as [chests and lockblocks](#chests-lockblocks)- including the ability to set up a prompt combo. When read they cause a message string to display.
* `Slope` combos can create custom diagonal collision. This can be useful for angled mountains in overhead view, or standard 2d sideview slopes. Additionally, in sideview, they can be set to act like optional stairs, which you will walk *past* by default, unless you are holding up/down as you walk past to indicate you want to go on the slope. Additionally, they can be set to be pass-throughable from specific directions.
* `Spotlight` combos shoot [Light Beams](#light-beam-puzzles).
* [`Switch` combos](#paired-switches), when triggered via `Triggers` tab `->ComboType Effects`, can toggle various states usable by `Switch Block` combos and the `Triggers` tab.
* [`Switch Block` combos](#paired-switches) can change based on various either level-based or global states.
* `SwitchHook Block` combos can be swapped with by the `SwitchHook` item, and can be customized with some additional settings.
* `Torch` combos light up [New Dark Rooms](#real-dark-rooms)
