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

## How your data is stored

All entries are saved locally on your device using browser storage (`localStorage`). There is no server, no account, and no syncing between devices. Nobody else can see your data, but it also does not back itself up anywhere.

A few practical notes:

- Data persists across page refreshes and app restarts on the same device and browser.
- Clearing your browser's site data (for example, "Clear History and Website Data" in Safari settings) will erase it.
- If you use this on multiple devices, each one keeps its own separate set of entries.
- Use the copy summary buttons regularly to back up your hours into your real timesheet system.

## Using it on iPhone

1. Open the app's URL in Safari.
2. Tap the Share icon.
3. Tap Add to Home Screen.

It will then open full screen from your home screen, like a regular app.

## Browser support

Works in any modern browser that supports `localStorage` and the standard `Date`, `time`, and `date` input types: Safari, Chrome, Firefox, and Edge. No installation, build step, or internet connection is required after the first load.