# MechKeysInfo
Little tidbits about making mechanical keyboards

## Rookie Mistakes
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
