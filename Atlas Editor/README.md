# SpaceCraft Atlas Editor

A browser-based tool for building and maintaining Atlas map files. As you explore the universe, use the Editor to log your discoveries through interactive forms — the tool handles the JSON so you don't have to. When you're done, download the updated file and load it straight into the Atlas.

---

## Getting Started

1. Open `SpaceCraft_Atlas_Editor.html` in your browser (no installation required).
2. Load a `.json` file by dragging it onto the drop zone, or clicking to browse. There are two ways to get started:
   - **Starting fresh** — use the blank template from the `Templates/` folder as your base and build your map from scratch.
   - **Continuing an existing map** — load any map from the `Atlas Maps/` folder and add to it.
3. Once loaded, the editor becomes active and shows your map's current sector and system count.

---

## How It Works

Select a category from the tabs along the top, then use the form to add or update entries. Each tab populates its dropdowns from your currently loaded atlas, so you can navigate straight to what you want to edit.

When you click **Save**, the change is written to memory immediately and logged in the Session Changes panel below. All changes are held in session — nothing is written to disk until you choose to download.

---

## Tabs

**Sectors**
Create a new sector or rename an existing one. Select an existing sector from the dropdown to edit it, or leave it on *New sector* to add one. Only a name is required.

**Systems**
Add a star system to a sector, or edit an existing one. Select a sector first to populate the system list. Each system requires a name and a registration code. FTL jump points are managed with the add/remove interface — see [FTL Jump Points](#ftl-jump-points) below.

**Planets**
Add a planet to a system, or update one that already exists. Select a sector, then a system, then a planet (or *New planet* to add one). Resources, deposits, and bases are managed as tag lists — type a value and click **+ Add**, or click **×** to remove.

**Space Stations**
Add a station to a system, or update an existing one. Works the same way as planets — drill down through sector and system to reach the station list. Floors and facilities are managed as a tag list.

**Resources**
Add or edit a universe rule. Select an existing rule to edit its sources, or choose *New rule* to create one. Sources are entered one per line in `key value` format (e.g. `iron 0.8`).

---

## FTL Jump Points

FTL links are managed on the **Systems** tab. Use the input field to add a jump point by typing either the system name or its registration code — the editor will automatically resolve it to the full `System Name (CODE)` format if that system is already in the atlas.

When you save a system, two things happen automatically:

- **Forward resolution** — any bare registration codes in other systems' FTL lists that match this system are expanded to the full name and code.
- **Bidirectional linking** — if the saved system lists another system as an FTL destination, a return link is automatically added to that system if one doesn't already exist.

---

## Naming Conventions

Consistent naming is important — the editor matches sectors, systems, and planets by name, so typos will cause entries to fail or create duplicates.

- **Sectors** — plain name only, no suffix (e.g. `Threshold`, not `Threshold Sector`)
- **Registration Codes** — use the in-game format exactly as it appears (e.g. `AB-1223D`)
- **Planets** — include the Roman numeral suffix where applicable (e.g. `Kepler IV`)
- **Resources and Deposits** — match the exact in-game name, including capitalisation

---

## Session Changes & Undo

Every time you save a change, it appears in the **Session Changes** log below the form. The log shows a summary of each change — what was added or updated and where it went.

You can undo the most recent change at any time using the **Undo** button next to it in the log. Only the last change can be undone.

The footer always shows how many unsaved changes are in the current session.

---

## Saving Your Work

Because this is a browser-based tool, it cannot write directly to a file on your computer. When you're ready to save:

1. Click **Download JSON** in the footer.
2. The file downloads with the same filename as the one you loaded.
3. Move it back into the `Atlas Maps/` folder, overwriting the previous version.
4. Load it in the Atlas to see your changes.

> **Important:** All session changes are lost if you close or refresh the page before downloading. Download regularly if you're making a lot of changes in one sitting.

---

## Contributing Your Map

If you've built or extended a map and want to share it with the community, open a pull request to add your `.json` file to the `Atlas Maps/` folder. All contributors are credited within the app.

Before submitting, make sure your map meets the following requirements:

1. **File naming** — the file must follow the naming convention `SpaceCraft_Atlas_Region_Quadrant.json`, where `Region` and `Quadrant` are replaced with the actual region and quadrant the map covers. For example, a pre-built map for the EU region, Harerus quadrant would be named `SpaceCraft_Atlas_EU_Harerus.json`.

2. **File structure** — the JSON must match the structure of the provided template exactly. Any deviation from the expected layout can break the Editor and Atlas for other users. The accepted structure is:

```json
{
  "map_info": {
    "region": "",
    "quadrant": ""
  },
  "universe_rules": {
    "Resource Name": {
      "Source Name": "yield"
    }
  },
  "sectors": [
    {
      "name": "Sector Name",
      "systems": [
        {
          "name": "System Name",
          "code": "XX-000A",
          "planets": [
            {
              "name": "System Name I",
              "type": "Unknown",
              "conditions": "Unknown",
              "resources": [],
              "deposits": [],
              "bases": []
            }
          ],
          "stations": [
            {
              "name": "Station Name",
              "owner": "Faction",
              "exploration_level": 0,
              "floors": []
            }
          ],
          "ftl": [
            "System Name (XX-000A)"
          ]
        }
      ]
    }
  ]
}
```

A blank copy of this template is available in the `Templates/` folder.
