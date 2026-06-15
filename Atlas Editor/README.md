# SpaceCraft Atlas Editor

A browser-based tool for building and maintaining Atlas map files. As you explore the universe, use the Editor to log your discoveries using pre-set templates — the tool handles the JSON so you don't have to. When you're done, download the updated file and load it straight into the Atlas.

---

## Getting Started

1. Open `SpaceCraft_Atlas_Editor.html` in your browser (no installation required).
2. Load a `.json` file by dragging it onto the drop zone, or clicking to browse. There are two ways to get started:
   - **Starting fresh** — use the blank template from the `Templates/` folder as your base and build your map from scratch.
   - **Continuing an existing map** — load any map from the `Atlas Maps/` folder and add to it.
3. Once loaded, the editor becomes active and shows your map's current sector and system count.

---

## How It Works

The Editor works in three steps for every change:

1. **Pick a template** — choose what you're adding from the tabs along the top.
2. **Fill in the template** — paste your completed template into the input area and click **Parse → Preview JSON**. The editor validates your input and shows you exactly what will be added or changed.
3. **Apply it** — if the preview looks correct, click **Apply to Atlas**. The change is written to memory immediately.

Repeat this as many times as you like. All changes are held in session — nothing is written to disk until you choose to download.

---

## Templates

Select the appropriate tab for what you're adding:

**New Sector**
Creates a new top-level sector. Only requires a name.
```
Name: {Sector Name}
```

**New System**
Adds a star system to an existing sector. List planets one per line — they'll be created as Unknown and can be filled in later using the Planet tab. FTL connections are automatically resolved to system codes if those systems are already in the atlas.
```
Name: {System Name}
Sector: {Sector Name}
Registration Code: {Code}
Planets:
  {Planet Name} I
  {Planet Name} II
Other POI: None
FTL Jump Points:
  System Name (CODE)
```

**New / Update Planet**
Adds a planet to an existing system, or updates it if it already exists. Resources and deposits go one per line. Use `None` if a section is empty.
```
Name: {Planet Name}
Sector: {Sector Name}
Solar System: {System Name}
Designation: {Type}
Conditions: {Weather}
Resources:
  {Resource Name}
Deposits:
  {Deposit Name}
Bases:
  {Base Name}
```

**Space Station**
Adds a station to an existing system, or replaces it if one with the same name already exists. Floors are comma-separated.
```
Name: {Station Name}
System: {System Name}
Owner: {Faction}
Exploration Level: {Level}
Floors: {Facility},{Facility}
```

**Universe Rule**
Adds or merges a resource rule into the universe rules index. The first line is the resource name followed by a colon. Each indented line is a source node and its yield rate, separated by a space.
```
{Resource Name}:
  {Source Node} {Yield Rate}
  {Source Node} {Yield Rate}
```

---

## Naming Conventions

Consistent naming is important — the editor matches sectors, systems, and planets by name, so typos will cause entries to fail or create duplicates.

- **Sectors** — plain name only, no suffix (e.g. `Threshold`, not `Threshold Sector`)
- **Registration Codes** — use the in-game format exactly as it appears (e.g. `AB-1223D`)
- **Planets** — include the Roman numeral suffix where applicable (e.g. `Kepler IV`)
- **FTL Jump Points** — list as `System Name (CODE)` where the code is known, or just the bare code if the system hasn't been added yet; the editor will resolve it automatically once that system is in the atlas
- **Resources and Deposits** — match the exact in-game name, including capitalisation

---

## Session Changes & Undo

Every time you apply a change, it appears in the **Session Changes** log below the input. The log shows a summary of each change — what was added or updated and where it went.

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
