# Barts Health ICT programme dashboard

A front screen for the ICT Director showing where each ICT programme stands against its baseline, plus one dashboard page per programme. Every page reads its programme's spreadsheet from this folder each time it opens. The pages use the NHS identity colours and Arial.

## Files

| File | What it is |
|---|---|
| `index.html` | The front screen: portfolio summary, status (RAG) for each programme, forecast against baseline, milestones |
| `wifi.html` | The Wi-Fi access point refresh dashboard |
| `Barts_WiFi_Refresh_Planner.xlsx` | The Wi-Fi plan and install log. Edit this to change what both pages show |
| `barts-health-logo.png` | **You add this:** the Trust logo, shown top right on every page (see below) |
| `README.md` | This note |

The site is at `https://bartshealth.github.io/AP_Deployment/`. The Wi-Fi dashboard is at `https://bartshealth.github.io/AP_Deployment/wifi.html`.

## Adding the Trust logo

The pages don't include the logo itself. NHS logos must be used exactly as supplied, so use the official file rather than a copy from a website or a redrawn one.

1. Get the Barts Health NHS Trust logo from the Trust's communications team (or the brand area of the intranet). Ask for the standard colour version on a white or transparent background, as a PNG or SVG.
2. Name it `barts-health-logo.png` (or `barts-health-logo.svg` / `barts-health-logo.jpg`) and upload it to the repository next to `index.html`.
3. Refresh the site. The logo appears top right on both pages, which is where the NHS identity guidelines place it. Until it's there, the pages show "Barts Health NHS Trust" as plain text in its place.

A logo about 112 pixels tall or more stays sharp; the page shows it at 56 pixels high (42 on phones).

## How the status is set

The front screen rates each programme in delivery:

- **On track (G):** forecast finish no more than 5 working days after the baseline finish.
- **At risk (A):** 6 to 15 working days after the baseline, or nothing logged for more than 5 working days that had installs planned.
- **Off track (R):** more than 15 working days after the baseline.

The forecast is the same one the Wi-Fi dashboard shows: what has actually been installed (the **Install Log** tab), with the rest of the plan run at the pace achieved over the last 10 working days. The baseline is the **20-min baseline** column on the **Order of Works** tab.

To change the thresholds, edit `RAG_RULES` near the top of the script in `index.html`.

## Updating the Wi-Fi plan

Edit `Barts_WiFi_Refresh_Planner.xlsx` in Excel (settings on the **Order of Works** tab; fixed dates, status and notes on the **Buildings** tab; actual installs on the **Install Log** tab), save it with the same name, and upload it in place of the old copy.

Fixed dates: a building marked **Complete** keeps its dates, and the rest of the plan starts the working day after the last completed building. A building with fixed dates that isn't complete yet (such as Central Tower floors 14 and 15 on 6 Nov) is a booking: it keeps its dates and the plan carries on alongside it.

Keep the Install Log up to date: the front screen shows "Figures as of" the last day logged, and turns amber if nothing is logged for more than 5 working days of planned work.

## Adding a programme

Each new programme gets its own page (for example `printers.html`) and its own spreadsheet. In `index.html`, find the `PROGRAMMES` list near the top of the script. The Printer replacement entry is already there with `stage: "planning"`, so it shows as "In planning, not rated yet". When its dashboard is ready, set `link` to the page. Rating it on the front screen also needs a reader for its spreadsheet (like the Wi-Fi one), which can be added when the printer plan exists. You can also fill in `lead` with a programme lead's name to show it on the card.

## Good to know

- Page versions are shown under each title: the front screen is **1.2** and the Wi-Fi dashboard is **1.7** (5 Nov 2026). If you still see an older number after uploading, wait a few minutes and refresh with Ctrl+F5.
- Version 1.6 of the Wi-Fi dashboard also fixes the comparison with the 20-min baseline (the phase table's baseline column and the "same as the baseline" note under the finish date), which earlier versions didn't pick up from the spreadsheet.
- Spreadsheets must keep their tab names and column headings, or the pages can't read them. Adding rows, notes or changing values is fine.
- The pages load their spreadsheet reader from `cdn.sheetjs.com`. If a network blocks that site, download `xlsx.full.min.js` from https://cdn.sheetjs.com/, upload it here, and change the `<script src=…>` near the top of each page to `xlsx.full.min.js`.
- Opening a page straight from your computer can't read its spreadsheet automatically. The Wi-Fi dashboard asks you to choose the file instead.
- The front screen prints cleanly (colours kept, buttons hidden) if you want a PDF for a meeting pack.
- A GitHub Pages site can be seen by anyone with the link, and so can the spreadsheets. Making the repository private doesn't change that unless the organisation is on GitHub Enterprise Cloud, which can restrict Pages to its members. To keep the director's view inside the Trust, host the same files on SharePoint instead.
