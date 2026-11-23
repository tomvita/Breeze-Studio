# Changelog

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
