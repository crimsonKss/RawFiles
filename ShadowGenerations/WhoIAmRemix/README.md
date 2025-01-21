# How to merge mods

## Credits:
- [ACB Injection Guide](https://gamebanana.com/tuts/18138)
- [@sound-sakura](https://www.youtube.com/watch?v=ZpLtJwSNeKQ)

## Requirements:
- [KwasTools](https://github.com/ThisKwasior/KwasTools/releases/latest)
- raw_files.zip

## Instructions:
1. Extract both the raw_files and the KwasTools to any anywhere you'd like.
2. Copy your game's `bgm_miller.acb` to somewhere else.
   * This file's originally located under `<Game Folder>\image\x64\raw\sound\resident_sound`.
   * **_COPY, DON'T CUT/MOVE_**
3. Drag and drop your `bgm_miller.acb` onto the `cri_utf_tool.exe` from KwasTools.
   * A file named `bgm_miller.acb.xml` should appear alongside a folder. (ignore the folder)
4. Open the `bgm_miller.acb.xml` file with your preferred text editor. `eg. Notepad++, Sublime Text, etc.`
5. This is the ID table of this mod's HCA files included in `raw_files`.
   * ```
     Index#    Replacing                          Filename                  ID#
     --------------------------------------------------------------------------
     11        Neo Devil Doom                     NeoDevilDoom_fight        6
     12        Neo Devil Doom Ending Scene        NeoDevilDoom_ending       7
     ```
   * For adding your own HCA files:
     * 5.1. Find the Index# in the other mod's table or in the `bgm_miller.awb` file if no table is provided.
       * The `bgm_miller.awb` file is found in the same place you originally found the `bgm_miller.acb` file.
       * To find the Index# you need to open the `bgm_miller.awb` file with [foobar2000](https://www.foobar2000.org/) with the [vgmstream](https://vgmstream.org/) plugin installed.
       * Find the track you want to replace, take the number in the `Item Index` and subtract it by 1, that's your Index#
       * For organization purposes, copy the table above, paste it to notepad. (or any other text editor)
         * Add what you want to replace below the others by adding the `Index#`, The name of what you want to replace under `Replacing`, the name of your HCA files in `Filename` and on the `ID#` you just increase it by one. `eg. 8`
6. In the `bgm_miller.acb.xml` file, for each replacement in the table above:
   * Search (CTRL+F): `AWB version="2"`
   * Under: `<files>`
     * Add: `<file seq="ID#" path="[File Folder Path]/[Filename].hca" />` [ always use forwards slashes (/) instead of backslashes (\\) ]
   * Under: `<order>`
     * Add: `<entry id="ID#" />`
7. Also in the `bgm_miller.acb.xml` file, for each replacement in the table above:
   * Search (CTRL+F): `value="Index#" name="StreamAwbId"`
   * Replace: `value="###" name="MemoryAwbId"`
     * With: `value="ID#" name="MemoryAwbId"`
   * Replace: `value="#" name="Streaming"`
     * With: `value="0" name="Streaming"`
8. Save and close the file.
9. Drag and drop the `bgm_miller.acb.xml` file onto the `cri_utf_tool.exe` from KwasTools, this will repack the `bgm_miller.acb` file in the same folder.
10. Create a mod using HedgeModManager by clicking `Add Mod` and selecting `Making one`.
11. On the mod's folder, create a new folder named `raw`, then inside it create a new folder named `sound`, inside the `sound` folder create a new folder named `resident_sound`.
12. Copy or move your repacked `bgm_miller.acb` to the newly created `resident_sound` folder.
    * The path should be `raw\sound\resident_sound\bgm_miller.acb`
13. Enable the mod on HedgeModManager.
14. Save & Play.
