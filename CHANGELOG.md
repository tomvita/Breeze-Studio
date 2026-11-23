# Changelog

## [0.07] - 2026-11-23

Use with Breeze **beta129.04** or later (nothing on the Switch changed), emuhost 0.5, and **pchost 0.6c** for games on the PC (the same as in 0.06).

- **Memory tab, like Breeze's Memory Explorer:** a pointer chain on top (`main+44298C0 › +B8 › +0 › +30 › +208 › +20`) with the step the cursor is on highlighted; picking a row moves its offset, following a pointer adds a step, **◀ / ▶** walk the chain (steps gone back from stay greyed), pages move the cursor. Each read resolves the chain again, so the view follows an object the game moves. Chains come along from Bookmarks, Objects, pointer scans and Cheats.
- **Field view in Memory:** when the cursor is in an object Studio knows (Unity, Unreal), the page is that object, field by field, with each field's own type.
- **Smart display:** one detected value per row (pointer, double, float, text, integer, 32.32 fixed); **Detection...** sets each detector's limits, on/off and order. Right-click > **Show as** sets one value's type by hand, kept per game.
- **Make cheat and bookmarks from Memory:** the row's chain from main and a store of the value you set; Add to bookmarks (Studio) or to Breeze's bookmarks; Copy chain.
- **Cheats > Jump to target** goes to the cheat's last address (the value it writes) with its pointer chain, which the cheat reader now follows through `5`, `7`, `9` and `4` opcodes.
- **Value pop-up:** editing a value (Memory, Workbench, Objects, Bookmarks, a cheat line) shows it as decimal, hex, float 32 and float 64 at once; type in one, the others follow. On a cheat line the opcode sets which words are the value and how wide (`400E0000 00000000 00002710`: 8 bytes).
- **Search: a label column** names the field each candidate sits on (`TextTween+20 target`, `Entry<int, int>[]+2C [0].value`).
- **Unity:** Field view, labels and Find chain work inside arrays (a dictionary's entries: coins in Land of Glarefall are `BagData.instance > basedata > _entries > [0].value`). Field view stopped working for the rest of a session after one array address: fixed.
- **Memory: Open in Memory on the page already shown** now picks its row (it did nothing).

## [0.06] - 2026-11-23

Use with Breeze **beta129.04** or later (beta129.06 has the same GAS cap rules on the Switch), emuhost 0.5, and **pchost 0.6c** for games on the PC.

- **GAS attributes (Objects tab, Unreal):** **(attributes, GAS)** lists every attribute of the player with its value and cap, found by reflection. Pick several, right-click > **Make cheats (attributes)...**: fill-from-cap and set cheats with off cheats, **Add all**, then **Try them** checks each one on the game. Caps are paired as `XMax`, `MaxX`, `CurrentX` > `MaxX`, `HealthPower` > `MaxHealth`, or set by hand.
- **pchost 0.6c:** Unreal 5.8 names on the PC (Revenge of the Mage had every class as "None_<n>"). Delete `ue_profile.ini` of a game that 0.6b mapped that way.
- **Studio reads Unreal 5.8 fields:** the Objects tab showed no fields on a 5.8 game.

## [0.05] - 2026-11-23

First release on its own. Use with Breeze **beta129.04** or later on a Switch (nothing on the Switch changed), emuhost 0.5, and **pchost 0.6b** for games on the PC (0.6a replaced 0.6 in this release on Nov 23; 0.6b was added beside it the same day).

- **pchost 0.6b: Unreal maps on Moadra.** 0.6a took a table inside the exe for the object list (40,000 objects, no player) and a world pointer that is empty between levels; 0.6b finds the real list (107,022 objects) and GWorld. Maps built with 0.6a: delete `ue_object_array.txt` and `ue_profile.ini` and build again.

- **pchost 0.6a: cheat window.** A list of the cheats with a check box each opens when the cheat file has cheats (Ctrl+Alt+C shows or hides it), so cheats can be switched without Studio or Python. A tick is saved in `toggles.txt`; folders show as headings, and a Keys column names the buttons a key cheat waits for.

- **pchost 0.6: Unity games on the PC.** A Unity IL2CPP game's code is in its `GameAssembly.dll`, not the exe: main is now that dll, so the IL2CPP maps are built (Void Reaver: 56,224 methods, where 0.5 found none). A Unity cheat made with pchost 0.5 has to be made again.
- **Find chain for Unity (Objects tab):** Field view of a found value, then right-click it > Find chain to this object: the pointer chain from main to the value, ready for Make cheat (Void Reaver's money in 1.4 s). On a pointer, the chains to the object it points at.
- **has field** marks the matching fields of the class you pick; **matching only** shows just them.
- **Unreal games on the PC:** the class list is read (Boltgun), maps and sets open as lists, and Field view of a value inside an array, map or set opens that container.
- **The title names the program on 127.0.0.1** (pchost, emuhost, the Lichii fork) from what it answers, not the name saved for 127.0.0.1 in the connection list.
- Studio has its own version number, shown in its title: 0.05. Before this, Studio came in Breeze's releases (beta129.00 to beta129.04, in `pc_app.zip`).
