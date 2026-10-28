# Sailing sign-up - handover

Parents of the sailing group tick which days their child sails at the weekend (Viernes, Sábado, Domingo) by tapping the child's name, instead of copying and extending the list in the WhatsApp group. Since 1.5.4 there is no copy-to-WhatsApp button: everyone reads the list on the page.

## Current version
- App 1.6.10 (28 Oct 2026): summary columns: weekdays left (Wednesday above Friday), weekend right (Saturday above Sunday). 1.6.9 (28 Oct 2026): summary in two columns (Wednesday | Friday, Saturday | Sunday), names as bullet lists, notes in grey. 1.6.8 (28 Oct 2026): space between logo and headline doubled (h1 margin-top 18 -> 36 px, parents' page). 1.6.7 (28 Oct 2026): language button half size (11 px text) on both pages; an invisible ::after keeps a finger-sized tap area. 1.6.6 (28 Oct 2026): Wednesday and Friday in one green family: Wednesday #EAF6EE / #B3DEC0, Friday #D9F0E0 / #8FCBA3, pennants #2E9A5C; dark #10261A/#2A573C, #13301F/#33694A. 1.6.5 (28 Oct 2026): weekend in one colour family, ocean blue (option C of three samples): Saturday #DCEBF8 / #93BFE6, Sunday #C6DDF3 / #78ABDA, both pennants #2F7FC8; dark #12263D/#2E5785, #16304F/#3A6A9E. 1.6.4 (28 Oct 2026): weekend cards stand out: Saturday #FBE7BF / border #E6BD6E, Sunday #CDEDE5 / border #86CBBC, 1.5 px borders (dark: #37291A/#7A5A26, #0F3631/#2E7468). 1.6.3 (28 Oct 2026): each day card tinted in its pennant colour (--d0..--d3 background, --d0l..--d3l border; dark-mode variants), name buttons stay white. 1.6.2 (28 Oct 2026): line under the heading lighter orange (--sun-soft #FFCB80) at normal weight; heading "¿Quién navega?" orange (--sun, large bold text, 7.7 contrast on the navy); logo without its blue block: cna-logo-white.png, white lettering on transparent (from cna-logo.png, blue (39,39,89) mapped to transparency, faint noise under 12% cleared, trimmed to the lettering, 164x75), shown 80x37 so the lettering keeps its 1.6.1 size. 1.6.1 (28 Oct 2026): logo 30% larger (57 px tall). 1.6.0 (28 Oct 2026): Club Nàutic Arenal logo (cna-logo.png, the blue block cropped from the club's image, 242x117, shown 44 px tall) top left on both pages, replacing the sailboat and the "Vela · Esta semana" / "Vela · Guía" text; those strings now only name the browser tab. 1.5.5 (28 Oct 2026): week label text orange (--sun; about 4.0 contrast where it sits on the week box, as Ronald chose). 1.5.4 (28 Oct 2026): "Copy final list for WhatsApp" removed (the page is the one list; a pasted copy goes stale); its mention in the coaches' manual removed too. Bring it back on a coach-only link if a coach misses it. 1.5.3 (28 Oct 2026): the line under the heading is orange (--sun #F5A83A, semibold; contrast 7.7 to 5.2 on the header where it sits). 1.5.2 (28 Oct 2026): How-it-works box has three lines and no button; it closes only from the link. 1.5.1 (28 Oct 2026): the "¿Cómo funciona?" link opens and closes the box (aria-expanded). 1.5.0 (28 Oct 2026): parents' "¿Cómo funciona?" box (open on a first visit until "Entendido", ss1_help; reopened from the link under the intro); the coach guide is now the coaches' manual for three coaches (how-it-works flow, "all three see the same list", steps 1-2 tagged one coach only, step 3 all three). 1.4.0: Wednesday added as a fourth day (shown first); the summary is called Resumen / Summary; the week label reads "Semana 28 oct – 1 nov". 1.3.0: Monday reminder, coach summary, coach guide page; the copied list marks empty days and follows the page language. 1.2.0: sailing design (navy sea header with sailboat and wave, a coloured pennant per day, white cards, sea-blue selected names, works in dark mode). 1.1.0: English button and laptop layout. 1.0.0: first build.
- Repo: tasar1-ship-it/sailing-signup, served at https://tasar1-ship-it.github.io/sailing-signup/
- Group link: `https://tasar1-ship-it.github.io/sailing-signup/#<group id>`. Coach guide: `.../sailing-signup/coach.html#<group id>` (same key; the guide builds the parents' WhatsApp message from it). The group id (22 random characters) is NOT in this repo; Ronald holds the link. Without it the page shows "Abre la página con el enlace del grupo".
- Example view without the database: `.../sailing-signup/?demo` (in memory, made-up names, nothing saved).
- Review copy: a page that sets `window.SS_PREVIEW` to a list of names before the app script runs uses those names in memory instead of Firebase. Ronald's review file (Downloads/Sailing sign-up preview.html, 28 Oct 2026) was built that way, with the real names and the two share messages; it is not in the repo.
- Firebase project: sailing-signup (project number 1090198402941), Realtime Database sailing-signup-default-rtdb in europe-west1, Anonymous sign-in on, web app "Sailing Signup" registered. Gemini and Google Analytics switched off. Spark (free) plan.

## Files
- index.html - the whole app (inline CSS and JS, own code ES5 only). Spanish and English UI: the button top right switches; the choice is kept per device (localStorage key ss1_lang); a phone set to English opens in English. The text copied for WhatsApp is always Spanish. The Firebase web config is written into it; that config is public by design, access is decided by the rules.
- firebase-app-compat.js, firebase-auth-compat.js, firebase-database-compat.js - Firebase compat SDK 9.23.0, vendored, byte-identical to the copies in commitment-board.
- coach.html - the coach's guide (ES5, Spanish/English): 1 send to the parents' group (wa.me button with the message filled in, copy as fallback), 2 pin it, 3 save the sign-up page; then "every week" and "if something goes wrong". Holds no group link; it reads the #part.
- database.rules.json - the rules exactly as published.
- icon-180.png - home-screen icon.
- cna-logo-white.png - club logo lettering (white, transparent) in the header of both pages.
- No service worker and no manifest, on purpose (same reasoning as commitment-board: it needs the network anyway and a stale cache is this family's usual failure). Nothing to bump on deploy.

## Monday reminder (1.3.0)
- A card at the top of the sign-up page adds a weekly calendar event: every Monday 17:00 local time (floating time, no time zone), 15 minutes, alert at the start, title "⛵ Apuntar a vela (fin de semana)" or the English one, the group link in URL and description. Nothing is stored on a server and no personal data is collected.
- iPhone/iPad: opens the .ics as a blob: page so iOS shows "Add to Calendar" (WebKit refuses top-level data: links, checked 28 Oct 2026). Other desktops: downloads recordatorio-vela.ics. Android: Google Calendar "add event" link (recur=RRULE:FREQ=WEEKLY;BYDAY=MO, ctz Europe/Madrid). The other route is offered as a small link under the button.
- After a tap the card collapses (localStorage ss1_rem); "Otra vez" brings it back. The page cannot know whether the parent really saved the event.
- A parent who never taps it gets no reminder. Truly automatic reminders (push notifications, a WhatsApp bot, e-mail) were set aside: they need a paid plan or service, phone numbers or e-mail addresses, and on iPhone push needs a home-screen install first.

## Data
- groups/<group id>/kids/<push id> {name (1-30 chars), at}
- groups/<group id>/picks/<Friday YYYY-MM-DD>/<day 0|1|2|3>/<kid id> {note (0-40 chars), at}. Day 0 Friday, 1 Saturday, 2 Sunday, 3 Wednesday (two days before that Friday; added 1.4.0 so older sign-ups keep their place). The rules allow days 0-3; published 28 Oct 2026, checked live (day 3 accepted, day 4 refused).
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

## Tested (28 Oct 2026, 1.3.0)
- ES5 parse of index.html, coach.html and the review copy. WebKit 32/32 new checks: calendar file (Monday 17:00, weekly, alert, link, lines within 75 bytes), card collapse and "again", Google link, Android shows Google first, iPhone user agent opens the blob without being blocked, summary and "nadie apuntado", copied list (empty days, real link, English), coach guide (no key, 3 steps, WhatsApp text with link, copy, English, 320 and 1440 px), review copy. Chromium the same except the iPhone-user-agent check (irrelevant: every iPhone browser is WebKit). Earlier suites still pass.
- Not tested: a real iPhone adding the event (from Safari and from inside WhatsApp), a real Android phone.

## Tested (28 Oct 2026, 1.4.0)
- Rules 21 cases (19 + Wednesday allowed, day 4 refused). Demo 12/12, language and layout 17/17 (four days side by side from 1200 px, two from 900 px, day headings never wrap), features 32/32 in WebKit (Chromium 31/32: the iPhone-user-agent check, irrelevant), review copy 12/12.

## Tested (28 Oct 2026, 1.5.0)
- help-test 16/16 in Chromium and WebKit (parents' box: first visit, close, stays closed, reopen, English; coaches' manual: flow, same-list note, tags, 7 tips, 320 and 1440 px). Earlier suites unchanged: demo 12, language 17, features 32 (WebKit), review copy 12.

## Known limits
- No reminder or notification; parents still need the link posted in the group.
- Names cannot be removed from the page (console only).
- Old weekends stay in the database; harmless at this size.
