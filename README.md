# Barts Health ICT programme dashboard

A front screen for the ICT Director showing where each ICT programme stands against its baseline, plus one dashboard page per programme. Every page reads its programme's spreadsheet from this folder each time it opens. The pages use the NHS identity colours and Arial.

## Files

| File | What it is |
|---|---|
| `index.html` | The front screen: portfolio summary, status (RAG) for each programme, forecast against baseline, milestones |
| `wifi.html` | The Wi-Fi access point refresh dashboard |
| `printers.html` | The printer replacement dashboard |
| `Barts_WiFi_Refresh_Planner.xlsx` | The Wi-Fi plan and install log |
| `Barts_Printer_Replacement_Planner.xlsx` | The printer plan and install log |
| `status-photo.jpg` | The photo shown with the rating on the front screen |
| `barts-health-logo.png` | **You add this:** the Trust logo, shown top right on every page (see below) |
| `README.md` | This note |

**Not for this folder:** `Barts_Printer_Replacement_Tracker.xlsx`, the device-by-device printer list, has serial numbers and room locations. Keep it on the Trust's SharePoint or Teams. The website only needs the planner.

The site is at `https://bartshealth.github.io/AP_Deployment/`. The dashboards are at `…/wifi.html` and `…/printers.html`.

## Adding the Trust logo

The pages don't include the logo itself. NHS logos must be used exactly as supplied, so use the official file rather than a copy from a website or a redrawn one.

1. Get the Barts Health NHS Trust logo from the Trust's communications team (or the brand area of the intranet). Ask for the standard colour version on a white or transparent background, as a PNG or SVG.
2. Name it `barts-health-logo.png` (or `barts-health-logo.svg` / `barts-health-logo.jpg`) and upload it to the repository next to `index.html`.
3. Refresh the site. The logo appears top right on every page, which is where the NHS identity guidelines place it. Until it's there, the pages show "Barts Health NHS Trust" as plain text in its place.

A logo about 112 pixels tall or more stays sharp; the page shows it at 56 pixels high (42 on phones).

## The rating on the front screen

Next to the summary in **At a glance** there's a photo and a rating on a scale of 1 to 5 thumbs up, currently set to **5 out of 5**. To change it, edit `RATING` near the top of the script in `index.html`:

- `score`: the setting, 1 to 5
- `title`: the heading above the thumbs (now "ICT Director Overall Happiness Rating")
- `name` and `role`: optional, shown under the heading if you fill them in
- `photo`: the image file; replace `status-photo.jpg` with another photo of the same name to change it. A copy of the current photo is also built into `index.html`, so the photo still shows if `status-photo.jpg` is missing. The current one is 120 × 120 pixels; a square photo of 250 pixels or more looks sharper on phones.
- `show: false` hides the whole panel

## How the status is set

The front screen rates each programme in delivery:

- **On track (G):** forecast finish no more than 5 working days after the baseline finish.
- **At risk (A):** 6 to 15 working days after the baseline, or nothing logged for more than 5 working days that had work planned.
- **Off track (R):** more than 15 working days after the baseline.

The forecast is the same one each dashboard shows: what the **Install Log** tab says has been done, with the rest of the plan run at the pace achieved over the last 10 working days. The baselines are the **20-min baseline** (Wi-Fi) and **30-min baseline** (printers) columns on each planner's **Order of Works** tab.

To change the thresholds, edit `RAG_RULES` near the top of the script in `index.html`.

## Updating a plan

Edit the planner spreadsheet in Excel (settings on the **Order of Works** tab; fixed dates, status and notes on the **Buildings** tab for Wi-Fi or the **Areas** tab for printers; actual work on the **Install Log** tab), save it with the same name, and upload it in place of the old copy.

Fixed dates: a building or area marked **Complete** keeps its dates, and the rest of the plan starts the working day after the last completed one. One with fixed dates that isn't complete yet (such as Central Tower floors 14 and 15 on 6 Nov) is a booking: it keeps its dates and the plan carries on alongside it.

Keep the Install Log up to date: the front screen shows "Figures as of" the last day logged, and turns amber if nothing is logged for more than 5 working days of planned work.

## The printer replacement

- **Source:** the supplier's device list, *Barts SoT October 2026* (1,469 printers). Each printer's site comes from its postcode, and its building and floor from the location fields.
- **Areas:** each area is one floor of a building, or the whole building where it has fewer than 20 printers. Area names start with the site code (for example `RLH Main hospital – floor 2`) so they're unique in the Install Log list. Printers with no floor in the list are in each building's "floor not recorded" area.
- **Remote and community sites** are grouped into 8 areas by district, one day each. The 7 printers in Apogee storage (Lincoln) and the 4 at the Lewisham and QEH pathology partnership sites are included, as you asked; mark those areas Out of scope if they don't need replacing.
- **Plan:** same site order as the Wi-Fi refresh, from Mon 16 Nov 2026, 30 minutes per printer, one team of 2 (14 printers a day), the same Christmas break. That finishes on 11 May 2027, which is the 30-min baseline. Add a second team on the Order of Works tab if there will be one.
- **Tracker:** the engineers fill in Status, date, new serial and model, engineer and whether the old printer was taken away. Its **Summary** tab totals each area; type a date at the top and it shows each area's count for that day, ready to copy into the planner's Install Log.
- **Tracker Issues** (in the planner) lists 7 problems found in the supplier's list, such as 189 printers with no floor and 12 whose site name doesn't match the postcode.

## Adding a programme

Each new programme gets its own page and its own spreadsheet. In `index.html`, find the `PROGRAMMES` list near the top of the script and add an entry. If its planner follows the same layout as these two, add a line to `SPECS` (tab name, column names and wording) and it will be rated like the others. You can fill in `lead` with a programme lead's name to show it on the card.

## Good to know

- Page versions are shown under each title: the front screen is **1.9**, the Wi-Fi dashboard **2.2** and the printer dashboard **1.4** (6 Nov 2026). The timelines always list phases and areas in date order. Under **Planned vs actual**, the plan is a red dashed line, the actual a thick blue line with a dot for each day logged, and the forecast a blue dotted line; the gap between plan and actual is shaded green (ahead) or red (behind). **Progress so far** (the default while work is under way) zooms in on the dates to date and the next week; **Whole plan** shows everything to the finish. Below it, two bar charts show how far ahead (above the zero line) or behind (red, below it) the Install Log is against the plan: one for each day and one for the running total, with the figures available as a table. If you still see an older number after uploading, wait a few minutes and refresh with Ctrl+F5.
- **On phones** (laid out for iPhone 15 and Android phones 360 to 412 pixels wide, portrait or landscape): charts are drawn at the phone's width so their text stays at least 12 px; the building and area lists become one card per row; the timeline scrolls sideways with the names kept in view; tapping a bar or a chart shows its figures. All pages use the Arimo font (same shapes and widths as Arial) from Google Fonts so iPhones and Android phones look the same; if a network blocks Google Fonts they fall back to Arial.
- Spreadsheets must keep their tab names and column headings, or the pages can't read them. Adding rows, notes or changing values is fine.
- The pages load their spreadsheet reader from `cdn.sheetjs.com`. If a network blocks that site, download `xlsx.full.min.js` from https://cdn.sheetjs.com/, upload it here, and change the `<script src=…>` near the top of each page to `xlsx.full.min.js`.
- Opening a page straight from your computer can't read its spreadsheet automatically. The dashboards ask you to choose the file instead.
- The front screen prints cleanly (colours kept, buttons hidden) if you want a PDF for a meeting pack.
- A GitHub Pages site can be seen by anyone with the link, and so can the spreadsheets. Making the repository private doesn't change that unless the organisation is on GitHub Enterprise Cloud, which can restrict Pages to its members. To keep the director's view inside the Trust, host the same files on SharePoint instead.
