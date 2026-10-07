# Client Task Board

One self contained HTML file. No build step, no framework, no dependencies beyond Google Fonts. Drop it into the Netlify site folder and it deploys like any other page. Open it in any browser and it works offline after first load.

This file is the single source of truth. If an older copy is floating around from an earlier download, replace it with this one.

## What changed in this version (v7)

Two things you asked for, plus a round of smaller additions. No storage key changed and nothing is converted, so every board loads exactly as it was. Before this version first runs it keeps one untouched local copy of the board, and on its first sync one untouched copy of the cloud board (Settings, Earlier copies, Before v7). Update every device to this file; an older build still works alongside it, but it does not carry the time log on, so the time log only lives on devices running v7 until all of them are.

**The clock on In progress.** Drag a task to In progress on the Board (or set its status anywhere) and a clock starts for that task. Move it back to To do or complete it and the clock stops. Each stretch is kept, so a task that goes in and out of In progress three times adds the three stretches up. A small timer chip shows on the card and row while it runs and after, and the task sheet has a Time section with the total, the running stretch, every stretch so far (any of them can be removed) and a Start or Stop button. The monthly log is on Progress, Time spent: pick any month, see the total, the split by client and every task with its time, and export that month or the whole log as CSV from Progress or Settings. The log syncs with the board and is part of every backup. A stretch under fifteen seconds (a drag in and straight back out) is not kept.

**Estimates that correct themselves.** The Focus timer logs time as well: a stretch opens when the timer runs on a task and closes when it pauses, ends, skips or the screen closes, and a task already on the clock is never counted twice. Every stretch also appears in the task's Activity list. A task with a duration shows estimated against actual in its Time section. Finished tasks with both a duration and logged time teach a correction factor per client (the median of actual over estimate, falling back to all tasks, kept between half and triple). With that, rows show your estimate and the corrected figure (45m → 1h), the Today load uses the corrected figure, the Duration panel in the task sheet suggests the corrected duration with a one tap Use button, and Progress, Time spent, shows the factors per client. Turn the correction off in Settings.

**Away, the time off planner.** A new tab. Pick the first and last day you are away and the page shows what to finish before you go (grouped by day, overdue first, with a progress bar that tracks what you tick off), what would be missed while away (with Before I go and After I am back buttons on each task, All before and All after for the lot, and Skip while away for repeats), and the week you are back. Today shows a banner in the two weeks before you leave. Away days count as vacation days, so streaks and overdue penalties pause on their own and the calendar and Upcoming mark them.

**Also new**

- Dark mode. Follows the system, with a manual override in Settings, Appearance. Per device.
- Compact rows. Settings, Appearance. About forty tasks on a desktop screen.
- Bulk select. Select on Today, Upcoming and the Board, tap tasks, then move their date, client, assignee or priority, complete them, or hide them, together. One undo covers the lot.
- Swipe on a phone. Swipe a task row right to complete it, left to move it to tomorrow.
- Daily plan ritual. In the morning Today asks you to pick up to three tasks; they sit at the top with a progress ring. From five in the evening (or once all three are done) it shows a recap and offers to roll what is left to tomorrow. Turn it off in Settings.
- Holidays. Settings sets your country and a country per client. Public holidays appear on the calendar (amber marker, a list under the month, the name in the day panel), as a tag on Upcoming days and in the Today hero. Festival dates that move each year are built in for 2026 to 2028 for India and Singapore; add anything else by hand in Settings, Holidays.
- Completions heatmap on Progress, 18 weeks, GitHub style.
- Weekly cloud copies. On top of the daily copy for 14 days, one copy a week is kept for 8 weeks. Both show under Earlier copies.
- Focus ambience. Rain (made on the device, no file to load) or a slow drifting gradient, from a row of chips in the Focus screen.
- A leaf burst, in the brand greens, for #TaskZero and the weekly goal. The daily goal keeps confetti.
- Empty state illustrations for Habits, an empty calendar day and an empty day in Upcoming, in the same style as Today and Notes.
- A typography pass on Notes in Preview: a reading width of about 68 characters, a larger body size and clearer heading sizes and spacing in the display face.
- A web app manifest (manifest.json, deploy it beside index.html), so Android offers a proper install. There is no service worker and no push, see below.

**Not done, on purpose**

- Push reminders when the app is closed, and a service worker. Push needs a server to send from; a service worker that caches the page can serve an old copy after a deploy, so it needs testing on the live site first.
- Attachments in Supabase Storage, Supabase Auth login, a read only client share link. Each needs changes inside the Supabase project (a bucket, policies, auth) that cannot be made or tested from this file alone.
- A timeline or Gantt view per client. Nothing blocks it; it was left out to keep this version to things that could be tested end to end.
- An activity log per task already exists: open any task and expand Activity at the bottom.

## Before v7

### v6

Everything can be arranged by dragging. The tabs (Today, Upcoming, Calendar, Board, Notes, Habits, Progress) reorder by dragging them in the sidebar, by pressing and holding them in the phone tab bar, or from Settings and More, Arrange tabs. The first five sit in the phone tab bar and the rest under More. Clients reorder from the sidebar, the Today groups, Settings, and now the client chips on the Board. In Upcoming's week view tasks drag between days and reorder within a day. Habits and notes drag into any order.

The board now opens on Board. Settings, Open the board on, changes that, including a Last tab used option.

Notes is a new tab for written notes. Type a title and press return, then keep writing. Notes save as you type, take lists, checkboxes and headings (see Preview), can be tagged to a client, pinned to the top, turned into a task, and show up in search. They sync between devices note by note, the same way tasks do.

A new mark (a checkmark that grows a leaf, in the brand greens) replaces the old favicon and the sidebar logo, with a short opening animation while the board loads. Tab changes, completions, new items, the hero scene, buttons and cards all got gentle motion. Colours, fonts and spacing are unchanged, and everything goes still for anyone with reduced motion turned on.

Your data. No existing storage key changed, so every board loads as it is. Notes live under a new key of their own. On first run this version keeps one untouched local copy of the board and, on its first sync, one untouched copy of the cloud board (it shows under Settings, Earlier copies, as Before v6). Restoring a backup file made before notes existed leaves your notes in place.

## Before v6

Latest tweaks. Your Google client ID is built in, so the Calendar tab opens straight to Connect. Tap it once, allow access, and your meetings load. If sign in ever fails, the only thing left to do is add your live site address to the Authorised JavaScript origins in your Google Cloud project. Done tasks can be cleared in one tap now, there is a Clear all button on the Done column and the Done list group, with an undo on the toast in case you change your mind. Empty tabs now sit centred in the middle of the screen instead of hugging the top. The Focus tab and stage got a visual pass, a softer setup card, a warm gradient backdrop, a progress bar under the timer, and a time readout that uses a dot rather than a colon.

Before that, three larger additions.

Primary tabs. A bar with Tasks, Calendar, and Focus. On a phone it sits at the bottom as a thumb friendly nav that respects the iPhone home bar. Your last open tab is remembered.

Google Calendar. A Calendar tab that shows your real meetings and lets you add, edit, and delete events straight from here. Because this board is a single file with no server, it talks to Google from the browser, which needs a free client ID tied to your own Google account. That ID is now baked in. It is a public identifier, not a password. The Google libraries load only when you tap Connect, so the rest of the app stays fast and works offline as before. Google only allows this over an https address, so use it on the live pratimnarayan.com or the Netlify address, not a file opened straight off the phone.

Focus. A Pomodoro tab. Pick one task, set your minutes, and start. The screen goes full and dark, showing only that task, its checklist, and a large timer. It runs focus and break rounds on a loop and keeps going until you stop it. Pause, skip a phase, tick off steps, or mark the task done from inside. A gentle sound and a banner mark each phase change if you leave that on. If you reload or your phone sleeps, the running session comes back where it should be.

Easier dates. Due date, deadline, and reminder now have one tap chips like Today, Tomorrow, Saturday, and In a week, with the native picker still there for anything precise. The reminder is split into a date and a time, and the time has its own chips like 9 am, Noon, and 6 pm. A Clear button sits beside each one.

Cleanup. The location note field is gone from tasks. The favicon you supplied is built into the page and also serves as the iPhone home screen icon if you add the site to your home screen.

## Earlier fix, still in place

The close bug was one line of CSS. The dialog backdrop set display flex, which quietly overrode the hidden attribute, so both dialogs rendered open on load and no close button could ever win. A single global rule near the top of the stylesheet now makes the hidden attribute always win. It carries a comment saying never remove it. Close buttons register on pointerdown so a keyboard opening cannot move a button out from under your finger, and there are always four ways out, the X, Cancel, tapping the dark area, and Esc on a desktop. The board still opens quietly, with reminders that lapsed while it was closed marked as seen instead of firing on open.

## What a task can hold

Title, client, assignee, priority, status, due date, hard deadline, repeat rule, reminder, labels, steps (checklist), attachments (links or small files), and free notes. Every field is editable on any task, new or old. Open a task by tapping its card or row.

## Recurring tasks

Set a Repeat rule and the board handles the rest. When you finish a repeating task it stays in your history as done, and the next occurrence is created automatically with the date advanced.

Rules available are every day, every weekday, every week on the same weekday, every two weeks, every month on the same date, every month on the same weekday position (this is your "first Monday of the month" case), and every year. Month end dates clamp sensibly, so the last day of a short month does not skip.

## Reminders

Set a reminder date and time. While the board is open in a tab it checks every thirty seconds and alerts you with a banner, plus a browser notification if you allow it. A static file cannot alert a closed phone on its own. For that your dev adds a service worker and a push service later. The reminder data is already stored on each task, so nothing needs re working when that day comes.

## Location note

This is a text note shown on the card, useful for "HDFC branch" or "site visit". True geofenced alerts that fire when you arrive somewhere need a native app, which a browser page cannot do, so this is a label rather than a trigger. Honest about that up front.

## Views, filters, board tools

Board view has three columns with drag and drop between and within them. List view groups by status, sorted by due date then priority, with Done collapsed by default. Filter by client, assignee, priority, label, or free text search. The Edit board button lets you rename or recolour clients and add or remove people.

## Data and storage

Everything lives in the browser under these keys.

```
pn_tb2_tasks           the task array
pn_tb2_comp            completions of repeating tasks
pn_tb2_exc             skipped or moved repeats
pn_tb2_cfg             clients, people and settings
pn_tb2_x               goals, streak settings, tab order, tombstones
pn_tb2_ui              view, filters, last tab and the tab to open on (this device only)
pn_tb2_notes           written notes (new in v6)
pn_tb2_time            the time log, one record per stretch in progress (new in v7)
pn_tb2_preupgrade_v6   one untouched local copy taken before v6 first ran
pn_tb2_preupgrade_v7   one untouched local copy taken before v7 first ran
```

Data never leaves the device. Backup downloads a JSON file, Restore reads one back, CSV downloads an Excel friendly copy. Small file attachments are stored inside the board as base64, capped at 400 KB each, with a warning when storage is tight. Use links for anything larger.

## For the dev

All logic sits in one script block at the bottom of index.html. Config constants (clients, people, statuses, priorities, repeat rules) are at the top of that block. Adding a client or person is one entry, the UI picks it up.

Every read and write goes through the small `store` wrapper, never localStorage directly. That wrapper is the single seam for adding sync. Swapping its two functions for Supabase calls turns this into a synced app across devices without touching the rest of the code. Pratim already runs a Supabase project for his finance tracker, so the same setup applies. File attachments should move to Supabase Storage at that point rather than base64 in a row.

Brand tokens are CSS variables in the `:root` block. Fraunces for display, Inter for body, Space Mono for utility labels.
