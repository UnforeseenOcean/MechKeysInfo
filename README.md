# MechKeysInfo
Little tidbits about making mechanical keyboards

### Foreword
These information have been compiled from what I've gathered online, through other people and/or by word-of-mouth. 

Please consult other people if you are not sure, and don't treat this as a be-all-end-all truth. This document is provided for guidance use only.

## Rookie Mistakes and Things That Are Good To Know

### Where are the 2.25U and 2.75U key stabilizers?

2.25 and 2.75U keys both use 2U key stabilizers. See the picture below. Smallest outline is 2U key, and the largest key is the 2.75U key.

![IMG1638253131](https://user-images.githubusercontent.com/11834016/143998260-911e83b7-2f63-46ab-92d4-2c786fce3f3a.png)

### Oh no, I forgot to add LCSC field to the component before copying it XX times! I'm doomed!

Fear not, click this button in KiCad and you can add them en masse.

![IMG1638254048](https://user-images.githubusercontent.com/11834016/143997649-3ac55c43-f12a-4c0a-b97f-475d91188de9.png)

On KiCad Nightly / KiCad 6, the button looks like this:

![IMG1638254030](https://user-images.githubusercontent.com/11834016/143997706-24d8c1f8-6aec-465d-9064-381d80a22e05.png)

### How do I set up the keys so they don't collide?

On KiCad, set the user grid to exactly 0.79375 x 0.79375 mm.

![IMG1638254753](https://user-images.githubusercontent.com/11834016/143998902-23701c8e-6257-4865-b946-45f8c72667bd.png)

Then start setting up your keys. They will fit together like a glove.

### I'm confused, what keys are what length?

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


### I can't decide what switch to get! There are too many!

First of all, don't worry. First make your board with "MX-Alps footprint", which supports both Cherry MX and Alps style switches (two major types of switches), then try to narrow the switch selection later.

Think of what you're looking for, or maybe go to your local electronics store and give the display units a try. What do you feel is the most important aspect? Sound and the feel? Or just the tactile feeling? Or none of the above?

- Sound and tactile feel is important to me
  - Go for Tactile/Clicky switches
- Don't care about the sound / I hate the clicking noises / The keyboard shouldn't be this loud
  - Go for Quiet/Silent Tactile (which has muted sound) or Linear switches
- I hate all of the above, can I go back to membrane keyboard?
  - You certainly can, but try Linear switches first

Remember: You do NOT have to go for the most expensive or most exotic switch to enjoy building mechanical keyboards. You have options to modify the switch, such as adding a film between top and bottom case, or lubricating the switch.

### Is this footprint 3-pin or 5-pin?

You can count the pins with this order:

![IMG1638418209](https://user-images.githubusercontent.com/11834016/144357720-5f24b704-7efe-4c73-a539-271485dfa567.png)


In this case, this is a 5-pin switch footprint. Same can be done to a switch.

(Note: 3-pin switch can be used on 5-pin footprint without modification, but the opposite cannot be done without modification.)

### How do I set up QMK for my keyboard?

(NOTE: This section is what I understood from the documentations and pointers people gave me. This may include incomplete info or incorrect info. Please refer to the latest QMK documentation for clarification.)

1. Get QMK MSYS from their site.
2. Type `qmk setup`.
3. Answer `y` to everything. This will clone the QMK repository into your user folder.
4. Now you type your new keyboard's name in lowercase letters or numbers. For example, `luna80`
5. It will ask you about the name. It is recommended to just press Enter if you've set up the Git environment, or use your GitHub name. I personally didn't because I won't be selling this board and as you can see my GitHub name does not match the name I operate under.
6. Press Enter to confirm, and you will see a message that tells you that a keyboard template has been created under the `keyboards` folder.
7. Go to `(username)/qmk_firmware/keyboards` and find your keyboard's name.
8. You will find a bunch of files, but just look at `config.h` for now.
9. Don't touch the `VENDOR_ID` unless you know exactly what you're doing, and change the `PRODUCT_ID` to something unique, using `0-9 A-F`. For example, `0x0539` or `0xDEAD`
10. If you've installed `MSYS` (Git for Windows will set it up for you) you will also find some Windows version of Linux utilities. `cd` into the `keyboards` folder and type: `grep "0x(your id)" -r`. If you see multiple entries, you might want to change that to something unique-er. It's probably fine to use similar values for your keyboard, but as far as I can understand it's not recommended. For example, `grep "0x1337" -r` results in the following:
 
![IMG1639175263](https://user-images.githubusercontent.com/11834016/145649307-bd83ad3f-b066-42c8-a07b-29f3e29bfb0a.png)

11. Now move down to other sections. Set `MANUFACTURER` and `PRODUCT` to something that fits your business, then...
12. Go to `MATRIX_ROWS` and `MATRIX_COLS`. This is where you absolutely need the schematic. Find how many ELECTRICAL columns and rows you have, and write it down there. (for example, this is 11 by 11 matrix)

![IMG1639175534](https://user-images.githubusercontent.com/11834016/145649655-8605f035-931f-459e-8139-2ab4c0cebbf8.png)

This is NOT the same as key columns. You must use what is shown on your schematic.

13. Go to `MATRIX_ROW_PINS` and `MATRIX_COL_PINS`. Read the numbers shown in the schematic, and translate it here. 

![IMG1639175999](https://user-images.githubusercontent.com/11834016/145650268-82e7a6d0-9585-4925-b4d0-9ad71ca0de9e.png)

For example, with this schematic it would be:
```
#define MATRIX_ROW_PINS { B7, D0, D1, D2, D3, D5, D4, D6, D7, B4, B5 }
#define MATRIX_COL_PINS { B3, B2, B1, B0, E6, F0, F1, F4, F5, F6, F7 }
```

Note: What you write here and what you said how large the matrix is up there must match. If you write 11 on `MATRIX_ROWS`, `MATRIX_ROW_PINS` should be 11 elements long.

14. If you wired your diode in other direction you have to change `DIODE_DIRECTION`. If yours was set up like mine, you don't have to touch this.
15. If your keyboard has NUM LOCK, CAPS LOCK, and/or SCROLL LOCK LEDs, define them in `LED_NUM_LOCK_PIN` and so on then uncomment it (remove two slashes in the front of the line).
16. Now open `(keyboard name).h` in your code editor. Go down to `LAYOUT`. You will see a message about how layout works. You will want to do the second part first. Look at your schematic and write down the matrix. You don't have to do fancy things, just make a grid of numbers and mark any empty spots (meaning, no switches exist there) with `XXX`, like so:

```
    { k00, k01, k02, k03, k04, k05, k06, k07, k08, k09, k0A }, \
    { k10, k11, k12, k13, k14, k15, k16, k17, k18, k19, k1A }, \
    { k20, k21, k22, k23, k24, k25, k26, k27, k28, k29, XXX }, \
    { k30, k31, k32, k33, XXX, XXX, k36, k37, k38, k39, k3A }, \
    { k40, k41, k42, k43, k44, k45, k46, k47, k48, XXX, k4A }, \
    { k50, k51, k52, k53, XXX, k55, k56, k57, k58, k59, k5A }, \
    { k60, k61, k62, k63, k64, k65, k66, k67, k68, k69, k6A }, \
    { k70, k71, k72, k73, XXX, k75, k76, k77, k78, k79, XXX }, \
    { k80, k81, k82, k83, XXX, k85, XXX, k87, k88, k89, k8A }, \
    { k90, XXX, k92, k93, k94, k95, k96, k97, k98, k99, XXX }, \
    { kA0, kA1, kA2, XXX, kA4, kA5, kA6, kA7, XXX, kA9, kAA } \
}
```
You'll have easier time if you are using "what I have is what I use" layout (meaning, the rows and columns match up exactly with your layout with no "dead keys") because you don't need to mark anything as empty.

17. Now move up one section and you will see something like:
```
#define LAYOUT( \
    k00, k01, k02, \
      k10,  k12    \
) { \
```
This is where you put your *actual* key layout, using the values from the matrix below. Usually people format it so it looks like what the keyboard has, like so: (Example file: `gh80-3000/gh80-3000.h`)
```
#define LAYOUT( \
    k00,      k01, k02, k03, k30, k31, k32, k33, k36, k37, k38, k39, k3A,        k04, k05, k06,   k07, k08, k09, k0A, \
\
    k10, k11, k12, k13, k40, k41, k42, k43, k44, k45, k46, k47, k48, k49, k4A,   k14, k15, k16,   k17, k18, k19, k1A, \
    k20, k21, k22, k23, k50, k51, k52, k53, k55, k56, k57, k58, k59, k5A,        k24, k25, k26,   k27, k28, k29, k2A, \
    k80, k81, k82, k83, k60, k61, k62, k63, k66, k67, k68, k69,      k6A,                         k87, k88, k89, k8A, \
    k90, k91, k92, k93, k70, k71, k72, k73, k75, k76, k77, k78, k79, k7A,             k96,        k97, k98, k99, k9A, \
    kA0, kA1, kA2, kA3,      k84, k85, k86,           k64, k65, k94, k95,        kA4, kA5, kA6,   kA7, kA8, kA9, kAA \
) { \
```

You can swap the numbers around if you want, but make sure it is reflected on the bottom matrix too, else you will have messed up keys.

18. Copy the layout and bring it to `(keyboard name)/keymaps/default/keymap.c`. Paste it like so:
```
    [_BASE] = LAYOUT(
    k00,      k01, k02, k03, k30, k31, k32, k33, k36, k37, k38, k39,             k04, k05, k06,   k07, k08, k09, k0A, \
\
    k10, k11, k12, k13, k40, k41, k42, k43, k44, k45, k46, k47, k48, k4A,        k14, k15, k16,   k17, k18, k19, k1A, \
    k20, k21, k22, k23, k50, k51, k52, k53, k55, k56, k57, k58, k59, k5A,        k24, k25, k26,   k27, k28, k29,      \
    k80, k81, k82, k83, k60, k61, k62, k63, k66, k67, k68, k69,      k6A,                         k87, k88, k89, k8A, \
    k90,      k92, k93, k70, k71, k72, k73, k75, k76, k77, k78, k79,                  k96,        k97, k98, k99,      \
    kA0, kA1, kA2, kA3,          k85,                 k64, k65, k94, k95,        kA4, kA5, kA6,   kA7,      kA9, kAA  \
    ),
    [_FN] = LAYOUT( 
    ...
```

19. Start changing the key names with ones from the QMK wiki key list. If you don't have a FN key or if you are not planning to use one, remove references to the FN keymap.
