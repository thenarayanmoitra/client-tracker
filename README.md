# Client Task Board

One self contained HTML file. No build step, no framework, no dependencies beyond Google Fonts. Drop it into the Netlify site folder and it deploys like any other page. Open it in any browser and it works offline after first load.

This file is the single source of truth. If an older copy is floating around from an earlier download, replace it with this one.

## What changed in this version

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
pn_taskboard_v1        the task array
pn_taskboard_ui_v1     view and selected client
pn_taskboard_cfg_v1    clients and people
pn_taskboard_page      last open tab
pn_focus_v1            the running focus session
pn_gcal_client_id      your Google client ID, this browser only
```

Data never leaves the device. Backup downloads a JSON file, Restore reads one back, CSV downloads an Excel friendly copy. Small file attachments are stored inside the board as base64, capped at 400 KB each, with a warning when storage is tight. Use links for anything larger.

## For the dev

All logic sits in one script block at the bottom of index.html. Config constants (clients, people, statuses, priorities, repeat rules) are at the top of that block. Adding a client or person is one entry, the UI picks it up.

Every read and write goes through the small `store` wrapper, never localStorage directly. That wrapper is the single seam for adding sync. Swapping its two functions for Supabase calls turns this into a synced app across devices without touching the rest of the code. Pratim already runs a Supabase project for his finance tracker, so the same setup applies. File attachments should move to Supabase Storage at that point rather than base64 in a row.

Brand tokens are CSS variables in the `:root` block. Fraunces for display, Inter for body, Space Mono for utility labels.
