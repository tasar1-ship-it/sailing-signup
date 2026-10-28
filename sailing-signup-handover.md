# Sailing sign-up - handover

Parents of the sailing group tick which days their child sails at the weekend (Viernes, Sábado, Domingo) by tapping the child's name, instead of copying and extending the list in the WhatsApp group. A "Copiar lista para WhatsApp" button produces the list in the old WhatsApp format, with the link at the end.

## Current version
- App 1.2.0 (28 Oct 2026): sailing design (navy sea header with sailboat and wave, a coloured pennant per day, white cards, sea-blue selected names, works in dark mode). 1.1.0: English button and laptop layout. 1.0.0: first build.
- Repo: tasar1-ship-it/sailing-signup, served at https://tasar1-ship-it.github.io/sailing-signup/
- Group link: `https://tasar1-ship-it.github.io/sailing-signup/#<group id>`. The group id (22 random characters) is NOT in this repo; Ronald holds the link. Without it the page shows "Abre la página con el enlace del grupo".
- Example view without the database: `.../sailing-signup/?demo` (in memory, made-up names, nothing saved).
- Review copy: a page that sets `window.SS_PREVIEW` to a list of names before the app script runs uses those names in memory instead of Firebase. Ronald's review file (Downloads/Sailing sign-up preview.html, 28 Oct 2026) was built that way, with the real names and the two share messages; it is not in the repo.
- Firebase project: sailing-signup (project number 1090198402941), Realtime Database sailing-signup-default-rtdb in europe-west1, Anonymous sign-in on, web app "Sailing Signup" registered. Gemini and Google Analytics switched off. Spark (free) plan.

## Files
- index.html - the whole app (inline CSS and JS, own code ES5 only). Spanish and English UI: the button top right switches; the choice is kept per device (localStorage key ss1_lang); a phone set to English opens in English. The text copied for WhatsApp is always Spanish. The Firebase web config is written into it; that config is public by design, access is decided by the rules.
- firebase-app-compat.js, firebase-auth-compat.js, firebase-database-compat.js - Firebase compat SDK 9.23.0, vendored, byte-identical to the copies in commitment-board.
- database.rules.json - the rules exactly as published.
- icon-180.png - home-screen icon.
- No service worker and no manifest, on purpose (same reasoning as commitment-board: it needs the network anyway and a stale cache is this family's usual failure). Nothing to bump on deploy.

## Data
- groups/<group id>/kids/<push id> {name (1-30 chars), at}
- groups/<group id>/picks/<Friday YYYY-MM-DD>/<day 0|1|2>/<kid id> {note (0-40 chars), at}
- Weekend shown: Monday-Friday shows the coming Friday-Sunday, Saturday/Sunday the current one. Arrows move a week.

## Rules (what a browser can do)
- Read a group only if it knows the group id; nobody can list groups; signed-out requests are refused.
- Add a child's name; cannot rename or delete one (do that in the Firebase console, Data tab).
- Tick, change the note of, or untick any child on any day of an existing child. Any parent can untick any child: deliberate, so parents can fix mistakes, but it means no protection against a mischievous member of the group.

## Tested (28 Oct 2026)
- Rules: 19 cases in targaryen, all pass.
- Demo UI: 12 checks in Chromium and WebKit (tick, note, remove, add name, duplicate refused, WhatsApp text, week switch).
- Live database: two separate parents in Chromium and in WebKit, on a weekend five weeks out: names load, a tick appears for the other parent within 2 s, notes sync, untick syncs. Test ticks were removed. Raw API: read without sign-in refused, listing groups refused.
- Not tested: a real iPhone or Android phone, WhatsApp's in-app browser.

## Tested (28 Oct 2026, 1.1.0)
- Own script parses as ES5. Demo checks 12 of 12 in Chromium and WebKit. Language checks 10 of 10 (switch, remembered after reload, English phone opens in English, WhatsApp text stays Spanish). Layout at 320 px (iPhone SE), 390 px (iPhone) and 1440 px (laptop): no sideways scrolling, smallest main text 15 px, three day cards side by side from 900 px.

## Tested (28 Oct 2026, 1.2.0)
- Own script parses as ES5. Demo 12/12, language and layout 17/17 (320, 390 and 1440 px; smallest main text 15 px), review copy 12/12 in WebKit at iPhone, laptop and iPhone dark mode. Dark-mode primary buttons were too dark and were changed to sea blue.

## Known limits
- No reminder or notification; parents still need the link posted in the group.
- Names cannot be removed from the page (console only).
- Old weekends stay in the database; harmless at this size.
