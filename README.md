# castledb-godot
This is a plugin for [Godot 3](https://godotengine.org/) to import [CastleDB](http://castledb.org/) database files as static data in gdscript with autocomplete.

## Installation

```bash
cd $PROJECT_DIR/addons

# in a git project
git submodule add git@github.com:mauville-technologies/castledb-godot.git

# outside a git project
git clone git@github.com:mauville-technologies/castledb-godot.git

```

Enable the plugin in the Project Settings.

Add a CastleDB file somewhere in your project hierarchy. Your CastleDB file must use the `.cdb` extension for the importer to generate code.

Add the imported CastleDB file to your AutoLoad scripts in Project Settings.

![Add to autoload scripts](docs/project-settings-autoload.png "Add to autoload scripts")

Enjoy code completion of your static data!

![Autocomplete your CastleDB Data](docs/autocomplete.png "Autocomplete your CastleDB Data")

## Interface

```python
# for object
data.sheet_name.get('id')
data.sheet_name.get_index(index)

# for dictionary (for easier dynamic manipulations)
data.sheet_name.as_dictionary()
```

## Usage Notes
- Use lowercase names for your sheets as the type is simply generated from Capitalizing your sheet names.
- String name constants are generated per sheet for your Unique Identifier columns
- Lookup your rows using the Unique Identifier for that sheet i.e. `Data.sheetname.get(Data.SheetName.UniqueId)`. This lookup is hashed and fast.
- Iterate your rows using the `all` field and for better autocompletion use the `get_index()` function when retreiving a row while iterating. i.e.
    ```swift
    for i in Data.sheetname.all.size():
            var item = Data.sheetname.get_index(i)
    ```
- If in doubt look at the generated script data by simply opening the `.cdb` file in Godot's script editor. *You may need to open the file in an extenral editor from it's imported source in the `.import` folder due to  limitation of Godot when re-importing / saving your CDB file as the editor seems to cache the original source, however from my experience autocompletion and testing still works without an editor restart.*

> ADDITIONAL COMMENT FROM A DIFFERENT DEVELOPER: As of 3.2.3, it seems that an editor restart will be needed for autocompletion to work correctly. See [this issue]

## Currently Supported Types
 - ID
 - Bool
 - Int
 - Float
 - Color
 - String
 - File
 - Tile
 - List
 - Dynamic

## Disclaimer
This project is driven entirely by my use of CastleDB in personal projects and is not a complete implementation of all features of CastleDB.

Pull requests welcome!


[this issue]: https://github.com/godotengine/godot/issues/10946