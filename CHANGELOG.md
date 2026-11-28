# Changelog

## [0.12] - 2026-11-28

Use with Breeze **beta129.04** or later (nothing on the Switch needs changing), **emuhost 0.6a** for an emulator and **pchost 0.7a** for games on the PC (both the same as in 0.11).

- **Cheats: changes not saved to SD are shown.** A red line above the status names each cheat that is new, edited or deleted since the list was last loaded or saved, and the button reads **Save to SD \***. Before, an edit that was never saved was lost without a word when the game started again: the game loaded the old cheat from the SD. Edits made outside the tab (another tab, a helper over PC connect) count too, since the code is read every 6 s. Turning cheats on and off does not count.
- **Code: Refresh (Ctrl+R).** The Code tab keeps the code it has read, so a hook or patch that an ASM cheat wrote afterwards did not show until Studio was restarted. **Refresh** beside Decompile reads it again (also what Callers searches on a PC game).
- **Hook here keeps the ASM source.** Add cheat saves the script with the cheat (`studio_hook_sources.json` in the game's folder). **Edit source** on the Cheats tab reopens it in Hook here, and **Replace cheat** puts the new code into that cheat. **Hook sources...** lists every saved source, including those of deleted cheats, to open, copy or delete.
- **Hook here / Patch never take a debugger break as the original.** Under a break, both used to read `brk` as the game's instruction: a hook ran it in its cave, and turning the cheat off wrote it into the game for good. They now ask the host what the break replaced, and refuse when it cannot say.
- **Set in the game:** a strip under the header shows the breaks and watches the game has now (amber when something is set, red when a thread is held); click it to remove them. Closing Studio asks whether to remove what is still set. Every break and watch Studio set is kept per game build and can be turned on again.
- **Objects > Instances:** every object of a class and its subclasses, in a window of its own, each marked live, live? or stale? by who points at it and named by its holder (`UnitManager.unitPool[10][0]`). Group by holder, filter by values (`currentHp > 0`), and add the class's fields as columns. Hadean Tactics on Lichii: all 829 Units in 4 s.
- **Cheats > What it does names each hop** on a Unity IL2CPP game with a field map: `writes 850 (int) to ForgeUI.instance > focusables[0] > _unit > currentHp`, with the value shown as its field's type.
- **Code: "also" columns on an instruction watch:** `+78 f32, +48 s32` adds a column per offset from the watched address's register (a unit's mana and team beside the HP the instruction reads).
- **Memory:** an 8-byte value counts as a pointer only when it points into readable memory (doubles, hashes and text showed as pointers: 1,177 false ones in 256 KB of Hadean Tactics' heap).
- **Files:** Windows' own right-click menu on both sides, and for a host on this PC (Lichii, emuhost, pchost) the SD card side shows full Windows paths.
- **Saved cheat files** start with `[Breeze Studio 0.12 <game> ... TID: ... BID: ...]`, so you can tell who wrote them.
- **Windows** left on a screen that is gone (a monitor unplugged, the display mode switched) come back onto the nearest one.

## [0.11] - 2026-11-26 (emuhost 0.6a and pchost 0.7a added on 2026-11-27)

Added to the 0.11 release on Nov 27, beside 0.6 and 0.7 (Studio itself, `pc_app.zip`, is unchanged):

- **emuhost 0.6a: a breakpoint inside an ASM cheat's code cave stays.** The cheat rewrites its cave on every pass, and that write went over the breakpoint, so F9 there missed the code running. Now an unchanged cave is not written again, and a real change goes in under the breakpoint. Tested on stock Eden: with 0.6 the cheat's next pass wrote over the breakpoint, and once the cave had changed it never stopped again; 0.6a kept it through every pass.
- **pchost 0.7a: What code ran with a code cheat on.** A cheat writing over a function's first bytes removed What code ran's break there (the function never showed), and **Stop** then put the old first byte back into the cheat's `jmp`, which crashed the game when that function ran next. Now the break stays and Stop leaves the cheat's bytes alone. Tested on a test program: 0.7 crashed after Stop, 0.7a ran on in all three orders.


Use with Breeze **beta129.04** or later (nothing on the Switch changed), **emuhost 0.6** for an emulator (the same as in 0.09) and **pchost 0.7** for games on the PC (new; `breeze_mono.dll` comes with it, keep it beside `pchost.exe`).

- **Unity Mono games on the PC (pchost 0.7):** a Unity game built with Mono has no IL2CPP map, so pchost reads one from the game's own Mono runtime through `breeze_mono.dll` (MOUSE: P.I. For Hire: 23,343 classes in 0.3 s, the game kept running). Objects, Memory's field names, Find chain, Pointers and Make cheat work on it. A chain starts at a class's statics, written `{Player}`, and a cheat made from it works in every run: `roots.txt` beside the cheat file names the class for a static register, which pchost fills before each cheat pass (also `{mod:UnityPlayer.dll}` and `{fn:Class::Method}`).
- **x64 code cheats, Cheat Engine style (pchost 0.7):** an AOB cheat finds its code by a byte pattern, puts a cave near it and hooks it while on; off puts the game's bytes back. Code tab > right-click > **Make AOB hook** builds one from an instruction; Cheats > **Import CE table** turns a .ct's AOB injection scripts into cheats.
- **pchost toggle keys:** a key or pad combo per cheat, with a high beep on and a low beep off, set in pchost's cheat window or Studio's Cheats tab (Toggle key...).
- **What code ran and the instruction watch (F8) on PC games (pchost 0.7):** What code ran lists every function of the exe that ran, with a **this** column (the object a method ran on). F8 on an instruction lists the addresses it reaches, so at a method's start it lists its instances. Neither writes the game's code permanently.
- **Methods:** Objects > Methods lists a class's functions with its parents' (IL2CPP, Mono, Unreal with Blueprint functions); the Code tab has **Class of this function** and **Who uses this function**.
- **Unreal, one object list for every tab:** Objects, Memory and Search shared nothing and each read the whole list. Now the first one publishes it; with pchost 0.7's new `peekn` the names are ready in 1.9 s instead of 8.7 s (Queen's Domain, 528,400 objects). Memory names fields of objects over 4 KB (it showed none). Make cheat: **= Field** keeps a value equal to another field (a count to its cap).
- **Memory stays still:** live values 4 times a second, only the rows on screen redrawn, the rows kept as they are between refreshes, and a pointer of the chain that breaks for one read is not followed (the page jumped away and back).
- **Windows:** each detached window has its own **Fit** and **Dock**; a new window grows as its rows come in until you move or resize it; **Ctrl+Tab** / **Ctrl+Shift+Tab**, **Ctrl+1..9, Ctrl+0** and **Ctrl+Space** (type a few letters) switch tabs and windows; dialogs open in the middle of the screen Studio is on.

## [0.10] - 2026-11-25

Use with Breeze **beta129.04** or later (nothing on the Switch changed), **emuhost 0.6** for an emulator and **pchost 0.6g** for games on the PC (both the same as in 0.09).

- **First start without Pillow or capstone:** a message box lists the missing packages and installs them if you say Yes (pip in a window you can watch). Before, Studio started from the .bat showed nothing at all.
- **A failed Connect says why:** "nothing answers at 127.0.0.1:6801" (nothing is listening: turn on PC connect, start emuhost or pchost), "no answer from ..." (wrong IP, Switch asleep, another network), "... is not an address"; the Start tab lists what to check. A wrong code already said where the right one is.
- **The Start tab covers every target:** a Switch, the Lichii fork, another emulator through emuhost (turn on its GDB stub first) and a PC game through pchost, each with the address and code to type.
- **README: First time** - install Python, unzip, start, and a table of what to start and type for each target.

## [0.09] - 2026-11-25

Use with Breeze **beta129.04** or later (nothing on the Switch changed), **emuhost 0.6** (added on Nov 25; released here from now on, 0.5 was in Breeze beta129.04) for an emulator, and **pchost 0.6g** for games on the PC.

- **Pointer scan keeps the chains a cheat uses (pchost 0.6g):** a pointer that can lead on through several objects is followed through all of them (only the nearest was), and the last level no longer stops early when it holds too many objects. The Killing Stone's card battle chain was missing; now it is among the first 5,000 of about 20,000, in the same 12 s.
- **Pointers tab:** pointer chains in a tab of their own, every scan kept per game. **Find target by chains** puts the place the chains reach that holds the value in the Address box after the value moved, instead of a new search. **Remove broken**, **Auto clear** (broken / not the value / not the target, once or every 3 s, never down to nothing) and **Undo**. Chains kept by a scan: 5,000 at first (was 500).
- **Faster chain reads:** `chains` (new on pchost) reads 1,000 chains a request; 5,000 in 0.17 s instead of 1.5 s.
- **Find chain on Unreal:** named fields first (The Killing Stone: 110 s, was nothing in 937 s), value rows too (Sackboy's TrophyPoints), memory read once into an index (Sackboy 70-90 s -> 16 s), progress shown in the pane.
- **emuhost 0.6:** the same core as pchost 0.6g (every route kept, `chains`); on Fast Fusion in unchanged Lichii the restart-proof coin chain is found and 696 chains read in 0.02 s.
- **Cheats > What it does** reads again every 2 s while shown. **GAS view** says "in a menu?" at a main menu.

## [0.08] - 2026-11-24

Use with Breeze **beta129.04** or later (nothing on the Switch changed), emuhost 0.5, and **pchost 0.6d** for games on the PC.

- **Beside:** when one tab sends you to another (Open in Memory, Field view, Jump to target, Open in Code...), that tab opens as a window of its own next to the one you were in, fitted to what it shows, instead of taking its place. The next action of the same kind reuses that window. A check box in the header turns it off.
- **Mouse back and forward buttons** step through the views of Memory, Objects and Code. Memory and Objects got Forward.
- **Fit** (header) makes the window as small as it can be with everything in the tab shown, and **rows** sets the most rows Fit gives one table or list. **On top** keeps Studio and its windows above the game.
- **Cheats and Bookmarks keep up by themselves:** a cheat added, removed or switched elsewhere shows within 1.5 s (an edit you have not applied is kept); a bookmark added from Memory, Search, Workbench or Objects shows without Reload.
- **pchost 0.6d:** cheats run while the game is paused, so a Resume Game cheat can resume it (only F9 could).
- **Fixed:** the Objects tab lost **(attributes, GAS)** once the Unreal class list was read; a class whose parent is missing from the map showed gaps instead of the inherited fields; bookmarks from Objects landed in the Bookmarks group when that group came later in the file.

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
