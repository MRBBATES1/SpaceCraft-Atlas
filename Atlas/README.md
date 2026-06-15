# SpaceCraft Atlas

A browser-based exploration tool for navigating the SpaceCraft universe. Load your server's Atlas map and instantly browse every sector, system, and planet — with full resource and base tracking.

---

## Getting Started

1. Open `SpaceCraft_Atlas.html` in your browser (no installation required).
2. Click **Load Atlas Map** and select the `.json` file for your server or quadrant.
   - Pre-made maps are included in the `Atlas Maps/` folder.
3. The Atlas loads your map and displays a full overview of sectors, systems, and planets.

---

## What's in the Atlas

Each map covers the full hierarchy of your server's space:

- **Sectors** — top-level groupings of systems
- **Systems** — star systems within each sector, with FTL jump connections listed
- **Planets** — individual bodies within each system, showing type, conditions, resources, deposits, and any known installations
- **Stations** — space stations within a system, including owner, exploration level, and available facilities

See Disclaimer for Data Accuracy statement.
---

## Navigating the Atlas

The sidebar lists all sectors. Click a sector to expand it and see its systems. Click any system to open its full detail view on the right.

**Expand / Collapse** buttons at the top of the sidebar let you open or close all sectors at once.

The header bar shows a live count of total sectors, systems, and planets in the loaded map, along with the map's region and quadrant.

---

## Searching

The search bar filters systems in real time across the entire map. It matches against:

- System names and codes
- Planet names
- Resources and deposits found on planets
- Base names
- Station names and facilities

Clear the search with the **✕** button to return to the full sector view.

---

## Resource Index

At the bottom of the sidebar is the **Resource Index**, listing every resource type in the universe rules. Click a resource to see:

- Which source nodes produce it and their yield rates
- A **Find Planets** button that filters the entire sidebar to show only systems containing planets where that resource can be harvested

Click **Clear filter** or click the resource again to remove the filter.

---

## Marking Your Base

On any planet card, click the **⌂** icon to mark it as your base. Marked planets are highlighted across the Atlas — in system detail views and in the sidebar badges — so you can always find your way home.

Your base selection is saved in the browser session. To remove it, click the **⌂** icon again.

---

## Atlas Map Files

The `Atlas Maps/` folder contains pre-built maps for available servers and quadrants. Each `.json` file covers a specific region of space. Load the one that matches where you're playing.

If your region and quadrant is not avilible you can controbute to this project by submitting one. Please see the  Contributing a Map section for more details on how you can Contribute.

---

## A Note on Data Accuracy

The Atlas is built from information gathered and shared by players as its being explored. This means coverage is ongoing — not every system, planet, or resource will be documented yet, and some details may be incomplete as exploration continues. What you see reflects what the community has found and contributed so far for that region / quadrant.

---

## Contributing a Map

If you've mapped your own region/quadrant — or extended an existing map — you're welcome to share it with the community. Open a pull request to add your `.json` file to the `Atlas Maps/` folder and it will be reviewed for inclusion. All contributors are credited within the app.

Before submitting, please read the **Atlas Editor README** for the full contribution guidelines — including JSON structure rules, templates, and naming conventions that maps must follow to be accepted.