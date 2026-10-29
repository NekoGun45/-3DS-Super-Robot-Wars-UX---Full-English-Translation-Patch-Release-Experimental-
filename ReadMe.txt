Pre-Patched download: https://www.mediafire.com/file/4g1d1cndwpreskg/SRW_UX_EN_v1.0.3.zip/

Acknowledgements

Special thanks to Utopiaray, the first person to work on an interface
mod for Super Robot Wars UX. Their "Super Robot Wars UX Partial English
Translation" (v2.0), which covered the menus, the battle UI, spirits
and the intermission screen, was the starting point for this project:
it showed that the game's interface could be translated and gave me a
base to build on. This translation would not have been possible
without that groundwork.

Original thread:
https://gbatemp.net/threads/wip-super-robot-wars-ux-partial-english-translation.469496/

  Tip: when the name screen opens, press "Default" first. This fills in
   the canonical name correctly (Agnes / Berge / Arnie), and you can
   then edit it or just press "OK".
## Installation (Citra)

You need:
- A **decrypted** dump of your own Japanese Super Robot Wars UX cartridge (`.3ds` / `.cci` / `.cxi`).
- [xdelta3](https://github.com/jmacd/xdelta-gpl/releases), or a GUI patcher such as Delta Patcher.
- Python 3, only if you use the helper scripts.

### 1. Get the original files

- **RomFS files:** in Citra, right-click the game and choose **"Dump RomFS"**. From the dumped folder you need `arcTacPrmDat.bin`, `arcCmnPrmDat.bin`, `arcBtlPrmDat.bin` and `arcBtlMsgDat.bin`.
- **code.bin:** run `python tools/extract_code.py "your_rom.3ds"`. It writes `code_original.bin` next to the ROM.

### 2. Apply the patches

**Easy way:** put `xdelta3.exe` inside the `tools` folder and run:

```
python tools/apply_patches.py <dumped_romfs_folder> <code_original.bin>
```

It checks that your files are the right ones, applies every patch, and creates a ready-to-use `0004000000078A00` folder inside `tools`.

**Manual way:** apply each patch from `patches/` to the matching original file with xdelta3 or Delta Patcher:

| Original file | Patch |
|---|---|
| `arcTacPrmDat.bin` | `arcTacPrmDat.xdelta` |
| `arcCmnPrmDat.bin` | `arcCmnPrmDat.xdelta` |
| `arcBtlPrmDat.bin` | `arcBtlPrmDat.xdelta` |
| `arcBtlMsgDat.bin` | `arcBtlMsgDat.xdelta` |
| `code_original.bin` | `code.xdelta` (name the result `code.bin`) |

### 3. Put the files in Citra's mods folder

Right-click the game in Citra, choose **"Open Mods Location"**, and place the patched files like this:

```
0004000000078A00/
  code.bin
  romfs/
    arcTacPrmDat.bin
    arcCmnPrmDat.bin
    arcBtlPrmDat.bin
    arcBtlMsgDat.bin
```

Then boot the game from your original, unmodified ROM.

Notes:
- arcCmnPrmDat.bin is about 67 MB. That's normal, the original
  file is the same size.
- Always use the included code.bin. The battle dialogue file needs
  it, and the game will crash with the original code.bin.

* Luma3DS (real hardware): only tested on Citra so far. It may also
  work through Luma's built-in LayeredFS (Luma 7.0 or later) by
  copying the same files into a folder named 0004000000078A00, as
  Utopiaray's original instructions describe, but this hasn't been
  confirmed.



Q&A

Q: Why are some lines awkward or abridged?
A: The game has strict text limits: each dialogue box and battle
   message only fits a set number of characters per line. Some lines
   had to be shortened or reworded to fit, while keeping their meaning
   and the character's voice.

Q: Why do the Festum speak in broken English?
A: That's how they speak in their home series, Fafner. Their odd,
   fragmented way of talking is part of what makes them alien, so I
   kept it.

Q: Why do the SD Gundam Sangokuden units use Japanese readings in the
   UI, but Chinese names in the story?
A: Game guides and wikis use the Japanese unit names, and so does the
   UI, so I kept those for easy reference. In the story, though, I use
   the Chinese names (Liu Bei, Cao Cao...), because anyone familiar
   with Romance of the Three Kingdoms knows them that way. Both SD
   Gundam and this game reference the original novel a lot, so this
   makes the story easier to follow.

Q: Why does Linebarrel use English terms like "Factor", "Machina"
   or "champion of justice"?
A: That's the terminology the series itself already uses, so I kept
   it for consistency with the source.

Q: Why does Fei-Yen talk in lowercase with odd spacing?
A: Fei-Yen's voice is synthetic. In Japanese she speaks in "childlike"
   hiragana, and I imitated that in English.

Q: Why is the protagonist called "Arnie" in some battle lines, even
   after I renamed him?
A: In the story, the game uses whatever name you enter. Battle
   dialogue, however, is pre-written and can't insert your custom
   name, so a few lines use "Arnie", the protagonist's canonical
   nickname (his default name is Agnes Berge). This is the same in
   the original Japanese version.

Q: The name entry screen is clunky. How do I enter a name?
A: It works, but it's awkward. To make room for the English interface
   text, the Japanese kana and kanji were removed from the keyboard, and
   the Latin letters were switched to a standard font so thin letters
   like "i", "l" and "1" display properly. As a side effect, the cursor
   doesn't line up perfectly with the letters, and the labels overlap
   the text fields.
   Switch to "Alphanumeric" with Y, pick letters one by one, use B for
   a space and L/R to move the cursor. It takes some trial and error
   (it took me about 4 minutes to name my character), but it works,
   and the name is saved and used in the story. If you'd rather skip
   it, "Default" keeps Agnes Berge / Arnie.

Q: Does this work on real hardware?
A: It has only been tested on Citra. It may work on a 3DS through
   Luma3DS's built-in LayeredFS (Luma 7.0 or later), but this hasn't
   been confirmed. If you try it, let me know!

Q: The game crashes when a battle starts. What's wrong?
A: You're most likely missing the patch's code.bin, or using the
   original one. The translated battle dialogue needs the included
   code.bin, so make sure it's in place.

Q: Can I use this together with Utopiaray's patch?
A: No. This patch already replaces the same files, so just use this
   one on its own.

Q: Why are some screens still showing Japanese graphics? Why weren't
   they translated?
A: Some text in the game isn't text at all, but part of the image
   files (title screens, logos, certain menus and effects). Editing
   in-game graphics is something I'm not familiar with, and I didn't
   feel confident enough to work on it without risking breaking
   something. Everything else, from the story and battle dialogue to
   the interface, is in English.


Contact

For any suggestions, complaints or detailed bug/glitch/crash reports,
contact me at: witchofdarkness666@protonmail.com

Lastly, special thanks to Eli. 
