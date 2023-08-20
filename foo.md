## Full Subscreen Rewrite
The entire code behind how the subscreen functions has been entirely reworked to be less janky and more manageable. This makes editing the subscreen further a LOT easier of a task for us, and makes everything just a lot nicer in general.

### General mechanics tweaks
Several mechanics have been generally tweaked, including basic things like how the selector behaves and how items are equipped. These changes are mostly spread across a variety of quest rules, but for easy swapping, there are now "New Subscreen" and "Old Subscreen" Rule Templates available [see Quest->Options->Pick Rule Templates]. These change almost every new rule related to the subscreen - the only important one that they leave alone is `Old Gauge Tile Layout`, which changes the tile layout used by Gauge Piece widgets.

These new QRs, as well as many existing QRs that relate to the subscreen, have been moved to the new "Subscreen" tab. These are searchable as usual via the QR Search feature.

TL;DR New QRs, check the new Rule Templates or the Subscreen tab.

### Button Equipment Stuff
* QR 'No Button Verification'- if enabled, the engine will no longer auto-equip things to buttons for you.
* Also allows UNEQUIPPING items (try to equip it to the slot it's already equipped to)
* Problem: With this enabled, even if you start with items, now the engine won't equip any of them for you!
* Solution: Now you can set "Default Equipment" for each button slot! Just check the box in the ItemSlot widget, for the Active Subscreen that is set on the Starting DMap, and these items will begin pre-equipped to the buttons you set them to.

### Brand New Features
#### Overlay Subscreens
These subscreens draw over the screen at all times, both during play and the active subscreen.
As usual, widgets can have the 'Display' settings on widgets to change their visibility while the active subscreen is up, down, and scrolling.
This can be used for various things, such as:
* Displaying your current keys over the corner of the game screen, either using a 'Counter' for a number of keys or a 'Gauge Piece: Counter' to actually physically display each key.
* Displaying button items or other similar widgets transparently over the game screen, similar to LTTP

#### Active Subscreen: Pages
You can now add multiple PAGES to Active Subscreens! You can either set buttons (like L and R) to cycle pages, or trigger page transitions by pressing a button on an appropriately configured widget. Changing between pages will use one of currently 3 animation styles:
* Instant (It just jumps right to the other page)
* Slide (Both pages slide in the same direction, the current page going offscreen as the new page comes onscreen)
  * Direction and Speed (in px/frame, with 4 decimal places) are configurable for this transition type.
* Pixellate (Seemingly-but-not-actually random pixels from across the screen change bit by bit from the old page to the new page)
  * Duration is configurable for this type, in frames, as well as the "Invert", "XOffset", and "YOffset" parameters. These parameters only change the pattern of pixellation by altering the formula used to create the pixellation pattern.

By default, the Selector is not drawn during transitions- but this can be toggled as a checkbox on each transition.

#### Select Any Widget
Instead of only being able to move the cursor to "Current Item" objects (now renamed to "Item Slot"), the cursor can now be set to move to ANY widget you want it to! This has some nice interactions with other new features....

#### New Selector Features
The selected widget can now be set to:
* Have overridden selection text, which will be displayed in the "Selected Text" widget (formerly "Selected Item Name")
* Start a page transition animation on button press
* Run a generic frozen script on button press

Yes, you heard right, there is now SOME level of scripting on the engine subscreen, even if not much.

#### Gauge Piece Rework
Life and Magic gauge pieces received a MASSIVE overhaul, and the "Gauge Piece: Counter" has been added to allow gauges for ANY counter! All of these behave identically to each other, except for these differences:
* Magic gauge still has the "Show Drain" property, which is used to make a gauge piece display conditionally based on your magic drain rate (ex. show the half magic symbol when you have half magic)
* Counter gauge lets you configure which counter to use, and how many per container to use for that gauge.
Aside from these differences, they ALL can:
* Specify a Gauge Wid/Hei, making a single widget draw _**more than one gauge piece**_, instead drawing an entire GRID of gauge pieces for you!
  * Specify an XOffset/YOffset to be applied to each row/column to create an offset-grid
  * Specify an HSpace/VSpace to space out the grid
  * Flags to specify which direction the grid "moves" in (Right to Left? Top to Bottom? Move in columns first, then rows? Snake back and forth?)
* Hide the gauge (Or only show the gauge) when you have the Infinite Item for this gauge (works the same way as counter infinite items)
* Specify a "Units per Frame" to reduce tile page usage. For instance, if "Units per Frame" is "2", then it uses half as many tiles for the gauge, as it uses the same tile for "1" as it would for "0", and the same for "2" as it would for "3", etc.
* Specify frames/speed/delay for an animated gauge
* Specify an animation CONDITION, wherein the gauge will only animate if it is above or below a certain value (either as a hard value, or as a percentage of being full). Additionally, you can specify it so that it skips the first frame of the animation when the condition is true.
  * A good example of how you can use this, is to have your life gauge only animate when your health is critically low, and use the skip first frame feature. This way, normally, your life gauge uses a single still tile- but when you reach critical life, it starts using the second tile in the animation instead (as well as any more if you supply more of an animation). This would allow for, say, cracked heart containers, blood dripping from heart containers, etc, as low-health visual effects.
* Specify "Full Tile" mode, which causes the gauge to use full tiles instead of mini-tiles, becoming twice as wide and twice as tall in the process.

#### Counter Addition
Counters can now have a "Max Digits" specified, and if the counter has too large a value to fit in that many digits, it will instead display that many digits as all 9s.

### GUI Work
#### The Subscreen Lister
The dialog where you select which subscreen to edit is now upgraded to the new dialog system. This dialog now shows you _**3 separate lists**_ for the 3 different types of subscreen!

#### The Subscreen Editor
* Now somewhat auto-resizes itself situationally. This means it will be smaller for passive subscreens, larger for overlay subscreens, and will adjust to font changes.
* Now has text displaying information about the currently copied widget
* When editing an Active Subscreen, a whole new set of buttons for adding/removing/changing Pages is present.
* R-Click menu has been entirely revamped, with many new options added.
* R-Click menu now also exists if r-clicking in a spot that has no widget, which previously would give no r-click menu at all.
* Slight tweaks to the existing menus
* New Menu: Options.
  * Options->Mouse Settings allows you to change how the mouse behaves in the subscreen editor. You can choose between "Classic" (for the old behavior), or "Modern" (the new default, reworked behavior). Notably, in the Modern behavior, you are able to click-and-drag widgets around the subscreen editor.
  * Subscreen Settings dialog, allows you to specify settings specific to the subscreen. Currently only has settings for Active Subscreens, where some settings related to swapping pages are housed.
* Several new "View" menu options, such as previewing what it would look like if every counter were full, or if every max counter was 65535, or if you had the "Infinite Item" for every counter, etc. Also includes an option to toggle "Show Unowned Items". If off, the editor display will show only the items as you have in Init Data.

#### The Widget Properties Dialog
Slight spacing tweaks, every widget now has an additional tab for selection-related settings. More widgets will use tabs for formatting now, giving the dialog a bit more breathing room overall.
=end
