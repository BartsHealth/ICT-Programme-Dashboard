# Barts Health ICT programme dashboard

A front screen for the ICT Director showing where each ICT programme stands against its baseline, plus one dashboard page per programme. Every page reads its programme's spreadsheet from this folder each time it opens. The pages use the NHS identity colours and Arial.

## Files

| File | What it is |
|---|---|
| `index.html` | The front screen: portfolio summary, status (RAG) for each programme, forecast against baseline, milestones |
| `wifi.html` | The Wi-Fi access point refresh dashboard |
| `printers.html` | The printer replacement dashboard |
| `pcm.html` | The patient monitoring replacement dashboard (St Bartholomew's) |
| `Barts_WiFi_Refresh_Planner.xlsx` | The Wi-Fi plan and install log |
| `Barts_Printer_Replacement_Planner.xlsx` | The printer plan and install log |
| `Barts_PCM_Replacement_Planner.xlsx` | The patient monitoring status, timeline, actions, risks and membership |
| `status-photo.jpg` | The photo shown with the rating on the front screen |
| `barts-health-logo.png` | **You add this:** the Trust logo, shown top right on every page (see below) |
| `README.md` | This note |

**Not for this folder:** `Barts_Printer_Replacement_Tracker.xlsx`, the device-by-device printer list, has serial numbers and room locations. Keep it on the Trust's SharePoint or Teams. The website only needs the planner.

The site is at `https://bartshealth.github.io/AP_Deployment/`. The dashboards are at `…/wifi.html`, `…/printers.html` and `…/pcm.html`.

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

## Excel summary

Each programme page has an **Export** section at the bottom (the **Export** link at the top of the page jumps to it). **Download Excel summary** saves a workbook with the figures as they are at that moment:

- **Summary:** progress against plan, recent pace, planned and forecast finish against the baseline, and the plan settings
- **Phases:** each phase's dates, progress and change against the baseline
- **Buildings** (Wi-Fi) or **Areas** (printers): every building or area with its dates, progress, status and notes, in date order
- **Daily:** planned and actual for each working day, with running totals and the forecast, ready to chart in Excel
- **Install Log** and **Tracker Issues:** as they are in the planner

The file is named with the day you download it, for example `Barts_WiFi_Refresh_Summary_2026-11-09.xlsx`. If you've picked a different number of minutes on the page, the Phases and Buildings tabs use those dates and the Summary says so. The colours and bold text come from a library the page loads from `cdn.jsdelivr.net` when you click; if a network blocks it, the file still downloads with the same figures, just without formatting.

## Everything in one file, from the front screen

The front screen has an **Export** section near the bottom. **Download web page (all programmes)** saves one HTML file, for example `Barts_ICT_Programmes_2026-11-10.html`, with:

- the overview as it is now, including the status of each programme and the rating
- the full Wi-Fi, printer and patient monitoring dashboards, on tabs at the top of the file (**Overview**, **Wi-Fi**, **Printers**, **PCM**). The **Open the … dashboard** buttons on the overview go to the same tabs, and the browser's Back button returns to the overview.
- each dashboard's Excel summary, from **Download Excel summary** on its tab

To make the file, the front screen opens each dashboard out of sight and takes a saved copy of it, which takes a few seconds. Do this from the website, not from a copy saved on your computer. The file is about 1 MB and works offline, like the single-dashboard copies described below. Keep it on SharePoint or Teams, or send it by email.

## Index_Dashboard Master: one file you can update

`Index_Dashboard Master.html` holds the overview and all three dashboards in one file, with the three planner spreadsheets saved inside it. Unlike the copy described above, you can update it yourself. It works offline and when kept on SharePoint, Teams or OneDrive: SharePoint downloads it when someone clicks it, and it opens in their browser from there.

- **Updating the figures:** select **Update figures**, then do one of these:
  - **Choose the folder…** (Edge or Chrome): pick the SharePoint folder that holds the planners. You only do this once. After that, **Update from this folder** reads the newest planner of each kind in that folder. **Save in this folder** writes the file back to the folder, replacing the old copy, and OneDrive then copies it to SharePoint.
  - **Choose spreadsheets…**: pick one or more planners, or drag them onto the page.
- **Saving:** select **Save** to keep the new figures in the file. If no folder has been chosen, Save downloads the file. Upload it to SharePoint in place of the old copy.
- **Reaching SharePoint from these buttons:** sync the document library first. Open it in SharePoint and select **Sync**, or **Add shortcut to My files**. It then appears in File Explorer under the Trust's name.
- **Which file is which:** each planner is recognised by its tabs, not its name, so a renamed copy still works. A site tracker or the original patient monitoring plan is turned away with a note, because tracker progress goes into the Wi-Fi planner first. Before the figures change, each new planner is opened by its dashboard. If the dashboard can't read it, the figures from before are kept.
- **Today's date:** the overdue actions, late milestones and forecasts use today's date, the same as the website.
- **Spreadsheet reader:** the file uses the current spreadsheet reader from its website when it's online, and the copy built into the file when it isn't.
- **When a page changes:** if wifi.html or another page gets a new version, the master file needs rebuilding with the new pages.

## A copy of a dashboard for SharePoint or Teams

**Download web page**, in the same Export section, saves the whole dashboard as one HTML file, for example `Barts_WiFi_Refresh_Dashboard_2026-11-10.html`. The figures, the Trust logo (once it's in the repository) and the Excel summary are built into it. It doesn't need the spreadsheet, the internet or any other file, so it works offline and sends nothing anywhere.

- **Keeping it on SharePoint or Teams:** upload it to a document library or a channel's Files. When someone clicks it, SharePoint downloads it rather than showing it, and it opens in their browser from there. Files synced with OneDrive open with a double-click. It also works as an email attachment.
- **It's a snapshot.** It shows the figures as they were when it was saved, and says so at the top. Download a new one after the planner is updated.
- Charts, tooltips, the minutes setting and the views all still work. The link back to the other pages is hidden, because they aren't in the file. **Download Excel summary** in the copy gives the Excel file made at the same time.

**Why SharePoint downloads it instead of showing it:** SharePoint Online won't run web pages kept in a document library. It handles .html files in "strict" mode, which Microsoft no longer lets tenants turn off. The old workaround was to rename the file to .aspx, which needs "custom script" allowed on the site. Since 2024 Microsoft switches custom script off again after 24 hours. Since March 2026 SharePoint has also enforced a content security policy that blocks scripts from places it doesn't trust, including inline scripts. To show the dashboards inside a SharePoint page, put the live website in an Embed web part instead (next section).

## Showing the front screen on a SharePoint page

The live front screen can sit on a SharePoint page, such as the Project Delivery home page, in an **Embed** web part. The page stays here on GitHub and SharePoint shows it in a frame, so the SharePoint page is up to date as soon as a planner here is updated. Nothing on SharePoint needs changing after that.

1. **Allow the address.** This is done once for the site, by a site owner. Go to **Settings** (the gear) › **Site information** › **View all site settings**, then under **Site Collection Administration** select **HTML Field Security**. Choose **Allow contributors to insert iframes only from the following domains**, type `bartshealth.github.io`, select **Add**, then **OK**. Until then, SharePoint says "Embedding content from this website isn't allowed".
2. **Add the web part.** Edit the page, add a one-column section, add an **Embed** web part to it, and paste this code into it:

   ```html
   <iframe src="https://bartshealth.github.io/AP_Deployment/" width="100%" height="4000" style="border:0" title="ICT programme dashboard"></iframe>
   ```

3. **Add a link to the full page.** Above the Embed web part, add a **Button** or **Quick links** web part that opens `https://bartshealth.github.io/AP_Deployment/`. Then select **Republish**.

- **Height:** a height of 4000 shows the whole front screen on a desktop with no scroll bar inside the frame. A lower height, such as 1400, shows the top part with its own scroll bar.
- **Opening the dashboards:** the **Open … dashboard** buttons open each dashboard inside the frame, and **← All programmes** comes back.
- **Downloads:** SharePoint can limit what a page in a frame is allowed to do. If a download button does nothing on SharePoint, use it from the full page.
- **Who can see it:** anyone who can open the SharePoint page. It is the same public website.
- **Making it the site's home page:** put the Embed web part on a new page of its own and publish it. Then go to **Settings** › **Site contents** › **Site Pages**, select the page, and choose **…** › **Make homepage**. This needs a site owner. The old home page stays in Site Pages, and **Make homepage** on it switches back. The `index.html` file itself can't be the home page: SharePoint only uses pages from Site Pages as a home page, and it downloads .html files rather than showing them.

## How the status is set

The front screen rates each programme in delivery:

- **On track (G):** forecast finish no more than 5 working days after the baseline finish.
- **At risk (A):** 6 to 15 working days after the baseline, or nothing logged for more than 5 working days that had work planned.
- **Off track (R):** more than 15 working days after the baseline.

The forecast is the same one each dashboard shows: what the **Install Log** tab says has been done, with the rest of the plan run at the pace achieved over the last 10 working days. The baselines are the **20-min baseline** (Wi-Fi) and **30-min baseline** (printers) columns on each planner's **Order of Works** tab.

To change the thresholds, edit `RAG_RULES` near the top of the script in `index.html`.

The patient monitoring replacement is rated differently: it's a project with a timeline rather than a count of devices, so its project team sets **Overall status** (On track, At risk or Off track) and a **Reason** on the **Status** tab of its planner, and the front screen shows them as written. Until they're filled in, it shows as **Not rated yet**.

## The patient monitoring replacement

`pcm.html` and `Barts_PCM_Replacement_Planner.xlsx` cover replacing the GE patient monitoring at St Bartholomew's Hospital with Philips. The planner was filled in from *PCM_Replacement_Project_Plan_July_2026.xlsx* on 16 Nov 2026, and includes everything in it: names, the leave dates and the budget note included. The site and its spreadsheets can be seen by anyone with the link (see **Good to know**).

The planner's tabs:

- **Status:** the overall status, the reason, when it was set and by whom. Yellow cells are for you to fill in. Below them, counts of actions and risks are worked out from the other tabs.
- **Timeline:** one row per bar or milestone on the plan's chart, by month. **From** and **To** are months: an activity runs from the start of its From month to the end of its To month. Set **Status** to Complete as each one finishes. Tendering, the business case and the contract award are marked Complete already, as the purchase order has been raised. **Category** gives the colour, as in the plan's legend.
- **Actions:** both action logs from the plan, the project working group's and the ICT and clinical systems workstream's. **Due** can be a date or words such as ASAP; only dated actions count as overdue. Completed or Closed counts as done. Workstream names follow the five workstreams (the logs spelt some several ways).
- **Risks and Issues:** from the plan's Issue & Risks discussion, with a new **Status** column (Open or Closed).
- **Workstreams**, **Membership** and **Governance:** as on the plan's Membership and Governance tabs.

The dashboard shows the status and reason, the timeline with today marked, the milestones (a milestone whose month has passed without being marked Complete is shown in red), the actions with filters for open, overdue and completed, by workstream and by search, the risks and issues, and who's involved. Its **Export** section gives an Excel summary and a one-file copy of the page, like the other dashboards.

To update it, edit the planner in Excel and upload it with the same name. Changes made to the original project plan don't reach the dashboard unless they're copied into the planner.

## Updating a plan

Edit the planner spreadsheet in Excel (settings on the **Order of Works** tab; fixed dates, status and notes on the **Buildings** tab for Wi-Fi or the **Areas** tab for printers; actual work on the **Install Log** tab), save it with the same name, and upload it in place of the old copy.

Fixed dates: a building or area marked **Complete** keeps its dates, and the rest of the plan starts the working day after the last completed one. One with fixed dates that isn't complete yet (such as Alexander Wing, booked for 9 to 13 Nov) is a booking: it keeps its dates and the plan carries on alongside it.

Keep the Install Log up to date: the front screen shows "Figures as of" the last day logged, and turns amber if nothing is logged for more than 5 working days of planned work.

## The printer replacement

- **Source:** the supplier's device list, *Barts SoT October 2026* (1,469 printers). Each printer's site comes from its postcode, and its building and floor from the location fields.
- **Areas:** each area is one floor of a building, or the whole building where it has fewer than 20 printers. Area names start with the site code (for example `RLH Main hospital – floor 2`) so they're unique in the Install Log list. Printers with no floor in the list are in each building's "floor not recorded" area.
- **Remote and community sites** are grouped into 8 areas by district, one day each. The 7 printers in Apogee storage (Lincoln) and the 4 at the Lewisham and QEH pathology partnership sites are included, as you asked; mark those areas Out of scope if they don't need replacing.
- **Plan:** same site order as the Wi-Fi refresh, from Mon 16 Nov 2026, 30 minutes per printer, one team of 2 (14 printers a day), the same Christmas break. That finishes on 11 May 2027, which is the 30-min baseline. Add a second team on the Order of Works tab if there will be one.
- **Tracker:** the engineers fill in Status, date, new serial and model, engineer and whether the old printer was taken away. Its **Summary** tab totals each area; type a date at the top and it shows each area's count for that day, ready to copy into the planner's Install Log.
- **Tracker Issues** (in the planner) lists 7 problems found in the supplier's list, such as 189 printers with no floor and 12 whose site name doesn't match the postcode.

## Adding a programme

Each new programme gets its own page and its own spreadsheet. In `index.html`, find the `PROGRAMMES` list near the top of the script and add an entry. If its planner follows the same layout as the Wi-Fi and printer planners, add a line to `SPECS` (tab name, column names and wording) and it will be rated like them. A project like the patient monitoring replacement can use `engine: "pcm"` with a planner laid out like `Barts_PCM_Replacement_Planner.xlsx`. You can fill in `lead` with a programme lead's name to show it on the card.

## Good to know

- Page versions are shown under each title: the front screen is **1.12** (16 Nov 2026); the Wi-Fi dashboard is **2.6**, the printer dashboard **1.8** and the patient monitoring dashboard **1.1** (23 Nov 2026). The timelines always list phases and areas in date order, and always fit the width of the page with no scroll bars: on a narrower screen the name column gets narrower, long names end in "…", and the month labels thin out (years dropped except where the year changes, then every other month, or quarters on the patient monitoring timeline). Under **Planned vs actual**, the plan is a red dashed line, the actual a thick blue line with a dot for each day logged, and the forecast a blue dotted line; the gap between plan and actual is shaded green (ahead) or red (behind). **Progress so far** (the default while work is under way) zooms in on the dates to date and the next week; **Whole plan** shows everything to the finish. Below it, two bar charts show how far ahead (above the zero line) or behind (red, below it) the Install Log is against the plan: one for each day and one for the running total, with the figures available as a table. If you still see an older number after uploading, wait a few minutes and refresh with Ctrl+F5.
- **On phones** (laid out for iPhone 15 and Android phones 360 to 412 pixels wide, portrait or landscape): charts are drawn at the phone's width so their text stays at least 12 px; the building and area lists become one card per row; the timeline fits the screen, with shorter names and fewer month labels, and the notes beside the patient monitoring bars are left off (tap a bar to see them); tapping a bar or a chart shows its figures. All pages use the Arimo font (same shapes and widths as Arial) from Google Fonts so iPhones and Android phones look the same; if a network blocks Google Fonts they fall back to Arial.
- Spreadsheets must keep their tab names and column headings, or the pages can't read them. Adding rows, notes or changing values is fine.
- The pages load their spreadsheet reader from `cdn.sheetjs.com`. If a network blocks that site, download `xlsx.full.min.js` from https://cdn.sheetjs.com/, upload it here, and change the `<script src=…>` near the top of each page to `xlsx.full.min.js`.
- Opening a page straight from your computer can't read its spreadsheet automatically. The dashboards ask you to choose the file instead.
- The front screen prints cleanly (colours kept, buttons hidden) if you want a PDF for a meeting pack.
- A GitHub Pages site can be seen by anyone with the link, and so can the spreadsheets. Making the repository private doesn't change that unless the organisation is on GitHub Enterprise Cloud, which can restrict Pages to its members. To keep the director's view inside the Trust, host the same files on SharePoint instead.
