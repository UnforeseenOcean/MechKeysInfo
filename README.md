# MechKeysInfo
Little tidbits about making mechanical keyboards

### Foreword
These information have been compiled from what I've gathered online, through other people and/or by word-of-mouth. 

Please consult other people if you are not sure, and don't treat this as a be-all-end-all truth. This document is provided for guidance use only.

## Rookie Mistakes and Things That Are Good To Know
- Where are the 2.25U and 2.75U key stabilizers?

2.25 and 2.75U keys both use 2U key stabilizers. See the picture below. Smallest outline is 2U key, and the largest key is the 2.75U key.

![IMG1638253131](https://user-images.githubusercontent.com/11834016/143998260-911e83b7-2f63-46ab-92d4-2c786fce3f3a.png)

- Oh no, I forgot to add LCSC field to the component before copying it XX times! I'm doomed!

Fear not, click this button in KiCad and you can add them en masse.

![IMG1638254048](https://user-images.githubusercontent.com/11834016/143997649-3ac55c43-f12a-4c0a-b97f-475d91188de9.png)

On KiCad Nightly / KiCad 6, the button looks like this:

![IMG1638254030](https://user-images.githubusercontent.com/11834016/143997706-24d8c1f8-6aec-465d-9064-381d80a22e05.png)

- How do I set up the keys so they don't collide?

On KiCad, set the user grid to exactly 0.79375 x 0.79375 mm.

![IMG1638254753](https://user-images.githubusercontent.com/11834016/143998902-23701c8e-6257-4865-b946-45f8c72667bd.png)

Then start setting up your keys. They will fit together like a glove.

- I'm confused, what keys are what length?

See here in keyboard-layout-editor.com after selecting the key in question:

![IMG1638254960](https://user-images.githubusercontent.com/11834016/143999993-c9d62e9a-2731-4802-a5be-ddbb688916e1.png)

U unit is calculated by how many regular key (for example, Q key) you can fit into the same space this key is taking up. So for 2U keys, it takes two, and 6.5U takes six and a half keys.

Common lengths for the longer keys are:
- 1.25U (Ctrl, Alt, Win, Menu, FN)
- 1.5U (Tab, Backslash)
- 1.75U (Caps Lock)
- 2U (Backspace, Num Pad +, Num Pad Enter, Num Pad 0)
- 2.25U (Left Shift, ANSI Enter)
- 2.75U (Right Shift)
- 6.5U (Spacebar)

- I can't decide what switch to get! There are too many!

First of all, don't worry. First make your board with "MX-Alps footprint", which supports both Cherry MX and Alps style switches (two major types of switches), then try to narrow the switch selection later.

Think of what you're looking for, or maybe go to your local electronics store and give the display units a try. What do you feel is the most important aspect? Sound and the feel? Or just the tactile feeling? Or none of the above?

- Sound and tactile feel is important to me
  - Go for Tactile/Clicky switches
- Don't care about the sound / I hate the clicking noises / The keyboard shouldn't be this loud
  - Go for Quiet/Silent Tactile (which has muted sound) or Linear switches
- I hate all of the above, can I go back to membrane keyboard?
  - You certainly can, but try Linear switches first

Remember: You do NOT have to go for the most expensive or most exotic switch to enjoy building mechanical keyboards. You have options to modify the switch, such as adding a film between top and bottom case, or lubricating the switch.
