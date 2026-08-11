# Unclutter for Google Calendar™

When the same event sits on several of your Google Calendars, Google draws it once per
calendar. Unclutter draws it once, striped with each calendar's colour.

## What makes this fork different

Every extension in this family — the [2019 original][amy], [Cal Merge][hcawn], the
[MV3 fork][chizo] this one is built on — decides that two chips are "the same event" by
comparing their **titles**. That is wrong in a way that loses data: two genuinely
different meetings that happen to share a name get collapsed into one, and one of them
becomes invisible. It has been reported for years — [imightbeamy#70][i70] (closed as
"working as intended"), [HCAWN#25][h25] (open since 2023).

Unclutter matches on **event identity** instead. Google encodes each chip's
`data-eventid` as base64 of `"<eventId> <calendarId>"`; one event living on two
calendars keeps a single `eventId` and differs only in the calendar half — recurring
series included, since the per-instance `_<UTC stamp>` suffix matches across calendars
too. So identity is available in the DOM, and title matching was never necessary.

Result: real duplicates still merge, same-name-different-event stops merging. Chips with
no readable id (Google Tasks uses a plain `tasks_<id>` attribute) fall back to the old
title behaviour rather than dropping out of merging entirely.

## Install

Not yet on the Chrome Web Store. To run it now:

1. `git clone https://github.com/oNaiPs/unclutter-gcal.git`
2. `chrome://extensions` → enable **Developer mode** → **Load unpacked** → pick the folder.

The toolbar button toggles merging on and off.

## Build

    ./build

Writes `unclutter-gcal-v<version>.zip`, the artifact to upload to the Web Store.

## Credits and licence

GPL-3.0, inherited and preserved. This is a fork of [chizovation/gcal-multical-event-merge][chizo],
itself a fork of [imightbeamy/gcal-multical-event-merge][amy] by Amy Ciavolino, who wrote
the original. [HCAWN/gcal-multical-event-merge][hcawn] is a sibling fork whose gradient
fill styles are worth a look.

[amy]: https://github.com/imightbeamy/gcal-multical-event-merge
[hcawn]: https://github.com/HCAWN/gcal-multical-event-merge
[chizo]: https://github.com/chizovation/gcal-multical-event-merge
[i70]: https://github.com/imightbeamy/gcal-multical-event-merge/issues/70
[h25]: https://github.com/HCAWN/gcal-multical-event-merge/issues/25
