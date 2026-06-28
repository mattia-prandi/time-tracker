# Time Tracker

A simple, personal time tracking web app. No account, no backend, no ads. Everything runs in your browser and stays on your device.

It is built to work as an installable app on iPhone (Add to Home Screen), but it also works fine in any modern desktop browser.

## What it does

**Clock in and out**
Tap Clock In when you start working and Clock Out when you stop. The app records the time automatically.

**Track breaks**
Tap Start Break and End Break as many times as you need during the day. Each break is logged separately and subtracted from your total hours.

**Automatic daily totals**
For every day, the app calculates hours worked as: clock out time minus clock in time, minus the total break time.

**Weekly view**
Days are grouped into weeks (Monday to Sunday), each with a running total. If a week goes over 40 hours, it is marked as overtime so you notice it right away.

**Manual entry and editing**
Forgot to clock in, or want to log a day after the fact? Use the manual entry form to set or fix the date, clock in time, clock out time, and any breaks for a given day. Existing entries can be edited or deleted the same way.

**Copy summaries**
Each day has a Copy button that builds a clean text block with the date, clock in, clock out, breaks, and total hours, ready to paste into another timesheet system. Each week has a Copy week summary button that does the same for every day in that week, plus the week total.

**CSV export**
Export CSV (top of the logged days section) downloads a CSV file with every entry ever logged: date, day, clock in, clock out, breaks, and total hours per day. Each week also has its own Export week CSV button, for just that week's days. Useful for opening in Excel, Numbers, or Google Sheets, or for archiving alongside a real timesheet system.

## How your data is stored

All entries are saved locally on your device using browser storage (`localStorage`). There is no server, no account, and no syncing between devices. Nobody else can see your data, but it also does not back itself up anywhere.

A few practical notes:

- Data persists across page refreshes and app restarts on the same device and browser.
- Clearing your browser's site data (for example, "Clear History and Website Data" in Safari settings) will erase it.
- If you use this on multiple devices, each one keeps its own separate set of entries.
- Use the copy summary buttons regularly to back up your hours into your real timesheet system.

## Getting started from scratch

This app is a single static file. It needs to live at a real web address before it can be opened and installed like an app. The free way to do that is GitHub Pages. Here is the full process, assuming you have never done this before.

### 1. Create a GitHub account (if you don't have one)

Go to [github.com](https://github.com) and sign up. It's free.

### 2. Fork this repository

Forking makes a copy of this repository under your own GitHub account, with the `index.html` file already in place, no need to create anything from scratch or upload files manually.

1. Open this repository's page on GitHub.
2. Tap **Fork** (top right).
3. Confirm with **Create fork**.

You now have your own copy at `https://github.com/your-username/time-tracker` (or whatever the repository is named).

### 3. Turn on GitHub Pages

1. In the repository, go to **Settings** (the tab at the top of the repository page itself, not the GitHub account settings).
2. In the left menu, click **Pages**.
3. Under "Build and deployment", set "Source" to **Deploy from a branch**.
4. Under "Branch", select your default branch (commonly `main`) and the **/ (root)** folder.
5. Click **Save**.

### 4. Get the live URL

Wait a minute or two, then reload the Settings > Pages screen. A box will show the live URL, in the form:

```
https://your-username.github.io/your-repo-name/
```

Use the exact URL shown there. It must match your GitHub username and repository name precisely, any typo (including missing or extra letters) will result in a 404 error.

### 5. Open it and confirm it works

Open that URL in Safari (on iPhone) or any browser, and confirm the app loads and the buttons respond.

### If you get a 404 error

This almost always means the URL you typed doesn't exactly match your GitHub username or repository name. Go back to Settings > Pages and copy the URL shown there instead of typing it from memory.

## Using it on iPhone

Once the app is live at its URL:

1. Open the URL in Safari.
2. Tap the Share icon.
3. Tap Add to Home Screen.

It will then open full screen from your home screen, like a regular app.

## Browser support

Works in any modern browser that supports `localStorage` and the standard `Date`, `time`, and `date` input types: Safari, Chrome, Firefox, and Edge. No installation, build step, or internet connection is required after the first load.
