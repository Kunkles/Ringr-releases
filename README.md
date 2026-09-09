# Ringr

**A Mac app for making Preston iris marking rings.** Type the millimetre
positions you measured, and it prints the ring — numerals turned a
quarter turn, ticks on the edge, cut lines at both ends — straight to a
Brother P-touch.

**[Download the latest release](../../releases/latest)** · macOS 14 or
later · free

---

## The problem it solves

Marking up an iris ring by hand goes like this. Print a ruler tape.
Stick it on the ring. Mark each stop with a Sharpie. Read the
millimetres off. Retype all of them into P-touch Editor, nudging every
numeral into place by eye. Drag the ruler object off the canvas so it
does not print. Print the ring.

Ringr removes the retyping and the nudging, and once a lens has a saved
ring it removes the measuring too — the next time that lens turns up on
a job, you print its ring and go.

**The part that makes it accurate is that Ringr prints the ruler as
well.** Both strips come off the same printer at the same scale, so
whatever the feed error is, it lands on each of them equally and cancels
out. A stop marked at 47 mm on the ruler prints at 47 mm on the ring,
calibrated or not.

---

## What it does

### Lenses

Every lens is a ring, and every ring belongs to a lens — a ring is only
ever the marks of one particular lens, so keeping two lists apart bought
nothing.

Give a lens as much or as little as you know: **make, model, type,
format, focal length, serial number**, and **which motor you marked it
against**. None of it is required. The list files itself as you fill it
in — make, then type, then model, with focal lengths sorted as numbers
so a set reads 21, 35, 100 rather than 100, 21, 35.

**Make is a menu** of manufacturers rather than free text, because a
sidebar that groups by make files "ARRI" and "Arri" as two makers and
splits a set in half. The list is editable, and renaming a manufacturer
rewrites every lens carrying it — which is how two spellings get merged
back into one.

**Search can be pointed at one field.** It matters when "Prime" is a
type on one lens and half the model name on another.

### Collections

Named sets of lenses — a DP's kit, a show, a day — built by dragging
lenses onto a folder. **Membership only:** a lens in a collection is the
same lens still sitting under its make, it can be in several at once,
and deleting the collection leaves every one of them where it was.

### Marks

One row per mark. Stops carry a number; the ticks between them do not.
Arrows on each row nudge a mark by half a millimetre for when the
reading was a hair off.

**Nothing is interpolated.** The thirds on a real lens are rarely evenly
spaced, so every intermediate tick is a reading you took, not a number
the app worked out.

### Labels and logos

Add text or an image to a ring and drag it where it belongs — the focal
length, a serial, the maker's logo. Resize it, and Ringr warns you if it
has landed on top of a stop.

Imported images are turned into the black and white a thermal head can
actually print: one threshold slider decides how much becomes ink, and
transparent stays paper. White-on-clear logos are brought in inverted so
they print at all. **Eleven manufacturers' logos are already included.**

### Printing

Ringr asks the printer what tape it is holding and **refuses the wrong
one**. It refuses a low battery too — a low-battery warning halts a job
part way through, which wastes the tape and the ring.

Print one **calibration strip**, measure it, type in what you measured,
and every ring after that is corrected for that printer.

Developed against a **PT-D610BT over Bluetooth**. There is a USB path
for models without Bluetooth; see the caveat below.

### Backup

**A `.ringr` file holds your lenses, the images they use, and the
collections they sit in.** Export the whole library, or any set of
collections. Double-click one and Ringr opens it.

It is an ordinary zip. Rename it and any Mac can open it — a backup only
its own app can read is not much of a backup.

**Nothing is imported until you have seen what it would do.** The
preview lists what is new, what is already in your library, what has
changed since the backup, and what looks like a lens you already have
under a different id — each with a tick box, so a set can be taken in
part. Images and collection membership follow the ticks. Merge adds,
Replace restores, and either is one ⌘Z.

A collection export carries its lenses and their images but **never the
printer calibration**: that is a correction measured for one particular
printer, and applying it to someone else's would scale their rings by
your feed error.

### Elsewhere

Twenty-five steps of undo on ⌘Z. A delete confirmation that says how
many measured marks are about to go. A preview that stands on end and
zooms from the whole strip to 3×. And a walkthrough of all of it in the
Help menu.

---

## Installing

Download the zip from **[Releases](../../releases/latest)**, unzip it,
drag **Ringr** to your Applications folder, and open it. macOS will ask
for Bluetooth the first time; that is the printer.

The app is signed with a Developer ID certificate and notarised by
Apple, so it opens without warnings and without a network connection.

---

## Before you spend tape

**Use 18 mm TZe tape.** Not a preference. It matches the ring face
exactly — 24 mm hangs over the edges, and 12 mm leaves bare metal and
costs you numeral height you want on a dark stage. The layout, the
numeral sizes and the printable band are all worked out for 18 mm.

**Tooth pitch differs between motor makers.** A ring marked up against
one brand of motor reads a little off against another, even though both
are driven from the same Preston MDR — a Heden motor on a Preston MDR is
a common enough pairing. They more or less interchange, but not exactly.
Mark up on the motor you will actually be using, and note which one it
was; there is a field for it.

**Make one permanent measuring ring.** Print a ruler, stick it on a
spare ring, and keep it. Mark your stops on it in Sharpie, then when you
are done draw over the marks with a dry-erase pen and lift the lot with
the felt eraser — the dry-erase ink releases the permanent, and the
ruler is clean for the next lens.

---

## Known gaps

- **USB printing is untested.** It is written from Brother's raster
  reference and has never had a cable through it. It is also write-only,
  so it cannot do the tape check, the low-battery refusal, or confirm
  that a job finished. Bluetooth is the tested path.
- **No update check.** New versions appear here and nowhere else.

---

## Trademarks

Ringr ships a handful of lens manufacturers' logos so you can put one on
a ring. Those marks belong to their owners and are included only so a
ring can say whose glass it is. No affiliation or endorsement.

## Beer

Made by a DIT who got tired of retyping numbers into P-touch Editor.
Ringr is free and always will be. If it saved you an hour at the bench,
and you feel like it, the next one's on you —
[venmo.com/u/Ryan-Kunkleman-1](https://venmo.com/u/Ryan-Kunkleman-1).

---

## Changelog

Ringr prints marking rings for Preston iris hand units.

Versions are dated from the work, not from releases — this has been in
daily use since the first one. The build number is the commit count.

### 0.13.1 — 2026-09-08

#### Fixed
- **The walkthrough stays where it is put.** On one machine the whole
  first-run panel drifted around under an animation meant for a drawing
  inside it — "like the dvd player screen saver bouncing on the corners".
  The illustrations loop by sweeping a value from nought to one, and that
  sweep was animated into place with `withAnimation` from `onAppear`.
  `withAnimation` sets the animation for the entire update, not the part
  that asked for it, and `onAppear` arrives while the sheet is still
  working out where its own contents go. Lose that race and the panel's
  layout is caught by the same animation — which, being set to repeat for
  ever, never finishes. The content spent the whole time travelling
  toward where it belonged and never got there. Whether you lose the race
  is a matter of timing, which is why it appeared for one person and
  never on the machine it was written on. The sweep is read off a clock
  now, so there is no animation to be caught by.
- Illustrations are clipped to their card, so nothing one of them draws
  can end up outside the box it belongs in.

### 0.13.0 — 2026-09-08

#### Fixed
- **The logo printed.** It appeared in the preview and came off the
  machine blank: the printer built its own renderer and left the overlay
  images out of it. Text overlays were fine, which is what made it look
  like an image problem rather than a missing argument. There is one
  renderer now, and the preview and the printer both use it — two call
  sites building the same thing are two chances to leave something out,
  and only one of them tells you.
- **A second label prints without power-cycling the printer.** After
  sending a job the app slept a second and then asked "have you
  finished?" every couple of seconds for twenty seconds. Measured on a
  nine-millimetre label: fifteen requests, no reply to any, and the
  printer would not answer the *next* job either. Being talked at while
  it feeds and cuts leaves it deaf. It now waits out the tape and the
  cutter and asks twice, quietly.
- The link is handed back properly when a job ends, and the app waits for
  it to be gone rather than assuming. If the channel still refuses, the
  link underneath is rebuilt rather than the channel retried on top of
  it.
- **A whole row in the lens list is clickable.** The tree was built from
  nested disclosure groups, so every lens sat inside a container that
  indented it, and the row highlighted was not the view being clicked.
  The tree is flat rows now, with the indent drawn inside them.
- The marks table follows you to the bottom instead of leaving a new mark
  off the end of the list.
- Angénieux has its accent back in the image library. Its file had to
  lose one — a non-ASCII name inside a signed bundle breaks the
  signature — but what an image is called is not what it is named on
  disk.

#### Added
- **Add Next in Set.** Entering a set is the same five fields over and
  over with two changing: make, model, type, format, motor and the ring's
  style come across, and focal length, serial and marks do not.
  Deliberately not a duplicate — a set of rings all carrying the first
  lens's measurements would look right and be wrong on every lens but
  one.
- The Caldwell logo.
- A record of what the Bluetooth link does, written to
  `~/Library/Caches/ringr-bluetooth.log`. Five fixes went in on argument
  alone before this existed and none of them were the fault; one made it
  worse.

### 0.12.0 — 2026-09-08

#### Added
- **Images can be turned**, in eighths of a turn, on a slider beside the
  size. Anything finer is a nudge nobody asked for on a strip 15.8 mm
  across, where a logo three degrees off reads as a mistake rather than a
  choice.
- **A shared lens keeps its type.** Every shared ring had been filing
  itself under a folder called "—", because the payload never carried
  one. Type and format travel now.
- **A standard for sharing, not for existing.** A ring goes up with
  marks, make, model, focal length, type and motor, or not at all —
  somebody downloading it cannot ask you what it was. Motor is on the
  list because it is the one field that changes what the numbers mean.
  Serial is not: plenty of lenses turn up without a legible one, and
  losing real measurements to a formality is the wrong trade. Your own
  list stays exactly as forgiving as it was.
- **A shared lens says when the copy up there has fallen behind** the one
  here. A shared ring is a signed snapshot and cannot follow later edits,
  which was right and also invisible.

#### Fixed
- **A turned image was being cut off.** The box was sized from the
  unrotated picture and the picture turned inside it, so at anything but
  a quarter turn the corners went outside it. The turn also now happens
  in millimetres before anything maps to dots — dots are not square at
  180 × 360, so turning in dot space sheared a logo on the way round.
- A grouping level nobody filled in is no longer a level. Where every
  lens at a step leaves the field blank, the step is skipped rather than
  showing an empty folder — but only when *all* of them are blank, or an
  unmarked lens would appear to be a prime.

### 0.11.0 — 2026-09-08

#### Added
- **The shared database is kept on this Mac.** A signed ring is about
  three hundred bytes, so the whole thing fits locally with room to
  spare. It is fetched on launch and whenever you press refresh, which
  says how old the copy is.
- **Shared lenses are listed, not searched for.** Filed by make, then
  type, then model, exactly like your own — the box at the top narrows
  the tree rather than being a search you have to run. Nothing to wait
  for; it is a copy on this Mac, so it works on a cart with no signal.
- **A lens you own says when somebody else has measured it**, right in
  the list. That is the difference between a feature you have to remember
  and one that tells you.
- Taking a shared ring asks the server about that ring first. A local
  copy cannot know about a withdrawal — a retraction is an absence, not a
  record — so a stale copy would otherwise go on offering exactly the
  ring somebody had already pulled.

#### Changed
- Groups start collapsed, in both lists, and open again while you are
  searching. A search that leaves its answer inside a closed folder is
  worse than a list that was too long.
- **The walkthrough opens once, on the first run**, and then only from
  the Help menu. It used to open every launch until somebody ticked a box
  to stop it.
- New icon: a hand unit with a marked ring on the motor. It keeps a
  silhouette at the sizes the Dock actually uses, which the wordmark
  never did.

### 0.10.4 — 2026-09-07

#### Fixed
- **"Ringr is damaged and can't be opened", the other cause.** Found by
  the same person who spotted the first one, still seeing it after that
  was fixed — because this was a second, unrelated fault behind it.

  One bundled logo was named `Angénieux.png`. macOS stores that name
  decomposed — `e` plus a combining acute — while the zip carried it
  composed, as a single `é`. Archive Utility, which is what double-clicking
  a download uses, writes it back decomposed. The signature had sealed the
  composed form, so codesign reported the same file both added and
  missing, and the seal broke. Same name on screen; different bytes.

  The file is plain ASCII now. It is still called Angénieux in the image
  library, because what an image is *called* is data, while what it is
  *named on disk* has to survive being unzipped by four different tools.
  Accents are folded when matching starter images, so anybody who already
  had it keeps the one they have rather than acquiring a second.

  Releasing now refuses to publish if any name inside the bundle is not
  plain ASCII.

### 0.10.3 — 2026-09-07

#### Changed
- New icon, drawn larger in its frame so it holds together at the sizes
  the Dock and Finder actually use.

#### Added
- **Every release is now checked after it is published**, not only after
  it is built. The file GitHub serves is downloaded, extracted with plain
  `unzip`, and refused if a stray file lands inside the bundle, the
  signature stops verifying, Gatekeeper says no, the ticket is missing,
  either architecture is absent, or the version inside disagrees with the
  tag. A local archive that passes proves the build, not what came back
  down the wire.

### 0.10.2 — 2026-09-07

#### Fixed
- **"Ringr is damaged and can't be opened."** Reported by somebody who
  had seen it before and knew why, which is the only reason it was found.

  macOS stores extended attributes, and a zip carries them as AppleDouble
  side files — `._Ringr`, `._CodeResources`. Every release so far wrote
  those *inside* the bundle's own paths. `ditto -x` puts them back where
  they belong and everything is fine; Finder's Archive Utility, The
  Unarchiver, Keka and plain `unzip` write them out as real files inside
  the app, and a file the signature does not know about breaks the seal.
  What the downloader sees is that the app is damaged and should be
  binned.

  Downloads are now zipped from a staged copy with its attributes
  stripped and the rest sequestered beside the bundle rather than in it.

  Every check before this used `ditto` to extract, which reassembles
  those files and so passes on an archive that breaks for anybody using
  anything else. Releasing now extracts with plain `unzip` and refuses to
  publish if a single stray file lands inside the bundle or the
  signature stops verifying. Testing with the friendliest possible tool
  is how this shipped four times while every check said it was fine.

### 0.10.1 — 2026-09-07

#### Added
- **Ringr asks what to call you** on the first launch that has no name.
  The name beside a shared ring is the one part of this app other people
  read, and it was set in a panel nobody had a reason to open — so the
  likely outcome was a database full of Anonymous. Never on top of the
  walkthrough, and "Not now" means this launch, not never.
- **Your name is in the toolbar**, reading "Set a name" until there is
  one. Clicking it opens the identity panel either way.

### 0.10.0 — 2026-09-07

#### Added
- **"This ring printed and matched."** The strongest thing anybody can
  say about a measurement they did not take, and the only claim in the
  shared database that is not itself another measurement. Signed, one per
  person per ring, and never your own — vouching for your own
  contribution is a claim about a ring by the only person already known
  to believe it.
- Confirmed counts show wherever a ring is being judged: a column in the
  browse window and a line on the ring itself.

- **Shared collections.** A set somebody assembled — "the Cooke S4s at
  Panavision Woodland Hills" is a day of work that should not have to be
  repeated by the next person on that stage. Sharing one puts its lenses
  up as rings in their own right first, because a collection is
  membership and nothing else. Browse them under Collections in the
  browse window; taking one brings its rings in and makes a collection of
  your own holding them.
- Membership stays a **reference, not a copy**. A ring belongs to whoever
  measured it: withdraw it and it leaves every collection naming it,
  rather than living on where nobody can take it down.
- A shared collection is **marked in the sidebar** — coloured, badged and
  labelled "(shared)" — because being public is worth seeing without
  opening a menu.
- **Add Lens** is a proper button at the top of the sidebar rather than a
  small one at the bottom.

#### Changed
- Deliberately **not** a rating. An average over two people means very
  little, and a low score would be ambiguous in the way that matters
  here: a ring that does not match your lens may be a bad ring, or your
  32 mm may simply not be their 32 mm. So there is no negative, and a
  ring nobody has confirmed shows a dash rather than a zero — nobody has
  said it is right yet, which is not the same as somebody saying it is
  wrong.

### 0.9.1 — 2026-09-07

#### Fixed
- The two buttons in the Online Lens Database header jumped as the
  pointer arrived. A sidebar section header carries a collapse control
  that AppKit draws on hover at the trailing edge — exactly where they
  were — and it reflows the header rather than overlaying it, so holding
  its width open moved them twice instead of not at all. The title is an
  ordinary row now, and there is no section header for anything to
  appear in.
- "Measured by" printed a bare "1" beside "3 people", so the one number
  that says whether a ring has been corroborated read as a different
  kind of number. One person, three people.

### 0.9.0 — 2026-09-07

#### Added
- **The online lens database.** A section under the lens list that looks
  up rings other people have measured — by serial first, because rental
  houses re-rent the same glass and a ring off *this* lens is worth far
  more than one off another copy of the model.
- **Nothing arrives without being asked for, and nothing of yours leaves
  unless you go and share it.** No upload on save, no prompt after
  measuring. Sharing is its own action, and it is the claim that the ring
  is right.
- **A shared ring is never pasted in at its own numbers.** Where zero sits
  depends on where that person stuck their tape and what they lined the
  end line up against; the spacing between stops is what belongs to the
  iris. So you pick a stop, say where it sits on your ring, and the rest
  follows at the spacing they measured.
- **A ring you already own gets a comparison instead**, lined up on the
  first stop you both have and shown stop by stop. Not averaged — that
  would invent a third ring nobody measured.
- **An adopted ring is yours immediately**: its own id, edited freely, and
  resharing it replaces *your* contribution rather than theirs. It keeps
  a credit line saying whose measurement it began as, and the credit
  stays with whoever measured it however many hands it passes through.
- **An identity, not an account.** A key made on this Mac signs
  everything you share, so a ring cannot be posted under somebody else's
  name. Your display name sits beside its fingerprint — two people are
  allowed to choose the same name — and changing it re-labels everything
  you have ever shared, because a contribution records the key and not
  the name.
- **Unshare.** A ring shared before it was tested, or found wrong since,
  can be taken back down. Signed, so only the identity that put one up
  can remove it. Copies anybody already took stay where they are: that
  ring became theirs when they adopted it, and reaching into somebody's
  library to remove a lens they may be working with today would be worse
  than leaving a bad one up.
- **A ring knows which shared ring it is a version of** — the reference,
  not a credit line, since a name can change and two people are allowed
  to pick the same one. Recorded when a ring is adopted, when a working
  copy is made of one already shared, and kept pointing at the original
  through however many hands it passes.
- Notes, overlays, style and printer calibration do not travel. A serial
  plus a rental house plus a date says which lenses were on which job,
  and a calibration is one machine's feed error.

### 0.8.1 — 2026-09-07

#### Fixed
- **Ringr now runs on Intel Macs.** Every release until this one was
  built for Apple silicon only, because that is what it was built on and
  nothing said otherwise. On an Intel Mac such an app does not merely
  refuse to start — macOS reports it as *damaged, move it to the Trash*,
  which reads as a broken download rather than the wrong architecture.
  Builds are universal now, and a release that is missing either slice
  is refused before it can be published.

### 0.8.0 — 2026-09-07

#### Added
- **Ringr checks for a newer release.** Once when it opens, and every
  couple of days after that if it is left running — it lives on a cart
  for a week at a time. Until now a copy downloaded in September would
  have stayed on that version forever, because the only place a new one
  is announced is a page nobody revisits.
- The notice appears **only when there is something newer**: no
  interruption to say nothing has changed, and a failed check on a
  location with no signal is silence rather than an alert. *Check for
  Updates* in the Ringr menu answers either way, since a check you asked
  for should say something.
- **Skip This Version** stops it mentioning that release again while
  still offering later ones, and *Check Automatically* turns the whole
  thing off. The check sends nothing but the request — no identifier,
  nothing about the library or the machine.
- Ringr does not install anything. It opens the release page; you drag
  the new one into Applications over the old, and your lenses, images
  and collections are untouched.

### 0.7.0 — 2026-09-07

#### Added
- **Backup and restore.** A `.ringr` file holds the lenses, the images
  they use and the collections they sit in. It is an ordinary zip, so it
  can be renamed and opened by anything — the point of a backup is that
  it outlives the app that wrote it. Double-clicking one opens Ringr.
- **Collections export on their own** — one, several, or the whole
  library, chosen in the export sheet. They carry their rings rather than
  just naming them, so a collection arrives on somebody else's Mac as a
  working set of lenses, and a lens in two of the chosen collections
  travels once with both folders still naming it. Deliberately *without* the printer calibration: that is
  a correction measured for one particular printer, and applying it to
  someone else's would scale their rings by our feed error.
- **Nothing is imported until you have seen what it would do.** The
  preview says what is new, what is already there, what has changed since
  the backup and what looks like a lens you already have — and each one
  has a tick box, so a set can be taken in part. Images and collection
  membership follow the ticks. Merge adds, Replace restores, both are one
  Cmd-Z.
- Images are matched by content rather than by id, so the same logo
  arriving in two collections does not become two logos, each with its
  own threshold.
- **Make is a menu** of manufacturers, with the list editable. Renaming
  one rewrites every lens carrying it, which is how "ARRI" and "Arri" —
  two folders in a sidebar that groups by make — get merged back into one.

### 0.6.0 — 2026-09-07

#### Added
- **The walkthrough covers the whole app**, not just the core job. Six
  new steps: the grouped, field-searchable list; collections; the
  half-millimetre nudges, twenty-five undo steps and the delete
  confirmation; placing text and logos on a ring; what the threshold
  slider does to an imported logo; and what the printer is asked before
  a job goes near it. Still drawn rather than screenshotted, so it
  cannot go stale when a control moves.

#### Changed
- The package, the executable and the source folder are called Ringr
  too. The Application Support folder and the bundle identifier
  deliberately keep the old name: one holds every measured lens, the
  other holds the Bluetooth permission.
- Builds now happen outside iCloud. The file provider re-stamped
  `com.apple.FinderInfo` onto the bundle moments after it was cleared,
  and codesign will not sign over it.

#### Fixed
- **The test suite had not run in full for some time.** It aborted four
  tests in, and the abort read as a pass. Behind it, ninety-nine tests
  had not been running, and the accuracy tests that had been running
  were measuring nothing: they scanned the edge of the tape the ticks
  used to be on, found no ink, and every assertion that counted or
  zipped its way through the empty result passed. The bands are derived
  from the style now. The renderer was correct throughout — measured
  directly, the ruler's numerals sit within 0.12 mm of their ticks.
- **Releases were signed with the wrong certificate.** The identity was
  picked by a regex alternation, which is not precedence: it took
  whichever certificate the keychain listed first, and so ignored the
  Developer ID one. codesign also ran with its output discarded, so a
  failure left the linker's ad-hoc signature in place and looked built.
- Ringr is notarised and stapled, so a download opens without warnings
  and without a network.

### 0.5.0 — 2026-09-06

Named **Ringr**, with an icon.

#### Added
- **Collections.** Named sets of lenses — a DP's kit, a job — built by
  dragging lenses onto a folder. Membership only: a lens in a collection
  is the same lens as the one still grouped under its make, can be in
  several at once, and is untouched when a collection is deleted.
- **Motor** field, recording which motor a ring's marks were taken
  against, since tooth pitch differs a little between makers.
- **Grouped, searchable lens list.** Make, then Type, then Model, with
  focal lengths sorted as numbers so a set reads 21, 35, 100. Search can
  be aimed at one field, which matters when "Prime" is a type on one lens
  and part of a model name on another.
- **Undo and redo**, 25 steps, on Cmd-Z and in the toolbar.
- **Delete confirmation**, saying how many measured marks are about to go.
- **Animated walkthrough**, in the Help menu and on launch until told
  otherwise. Opens with the two things that cost tape if missed: 18 mm
  tape, and that a ring marked against one motor reads slightly off
  against another.
- **Model** and **Format** fields, and Type as a dropdown.
- Half-millimetre nudge arrows on each mark.
- Version and build number, from one place in the source.

#### Changed
- Lenses and rings merged into one list. A ring is only ever the marks of
  one lens, so keeping two lists let a ring point at the wrong lens or at
  none.
- Preview stands on end, so the numerals — which are turned a quarter
  turn on the tape — read the right way up.
- Preview zoom runs from the whole strip to 3x, opening a third along.
- Ticks and numerals moved to the far edge of the tape.
- Ring circumference is one remembered number, 207 mm, sizing both the
  ruler and the ring strip.
- Fine mode (180 x 360 dpi) by default, with a check that catches a
  printer ignoring it.

#### Fixed
- **Crash** when a text field finished editing after its row was deleted.
  Marks were addressed by array position; they are addressed by identity
  now, which also stops an edit landing on the wrong mark after a sort.
- **Undo appearing to do nothing** after adding a mark and deleting it.
  Both were named the same and folded into one step, which restored the
  state already on screen.
- **Cmd-Z ignored** immediately after a change — a focused text field
  keeps its own undo, and menu items validate lazily.
- The Bluetooth permission prompt returning on every launch: the app is
  signed with a development certificate rather than ad-hoc, so its
  identity survives a rebuild.

### 0.4.0 — 2026-09-05

#### Added
- **The ruler is printed by the app.** Both strips now come off the same
  printer at the same scale, so the printer's feed error lands on each
  equally and cancels — a stop marked at 47 on the ruler prints at 47 on
  the ring, calibrated or not.
- Full-width datum line at each end of both strips, to register and cut
  against.
- Calibration strip and per-printer feed correction.
- Printers panel: what is here, what tape it holds, and remove.
- Low battery is refused before tape is spent, with the option to go
  ahead. A low battery warning halts the printer mid-job, which is why a
  ring once printed without cutting.

#### Fixed
- **Jobs hanging on "Receiving, please wait".** The whole job went out in
  ninety milliseconds while the tape takes eight seconds; anything past
  the printer's buffer was lost and it waited forever for lines it had
  been promised. Raster is now fed at the speed it prints.
- **A silent printer reported as a successful print.** Writes to a paired
  but sleeping printer are accepted and discarded, and the status read was
  wrapped in `try?`, so the job vanished and the app said it had printed.
- Completion is confirmed by polling the phase byte, since this printer
  sends no automatic status at all.

### 0.3.0 — 2026-09-05

#### Changed
- **Bluetooth goes over IOBluetooth RFCOMM.** The `/dev/cu.*` serial node
  never carried a byte to this printer — it exists for any paired device,
  accepts writes and discards them, connected or not. Tested directly:
  still discarded after the baseband link was up and the device reported
  connected.
- Replies are waited for where they arrive. IOBluetooth delivers channel
  data on the main run loop, not the thread that opened the channel: the
  same request that timed out after 26 s came back in 1.3 s once the main
  loop was kept turning.

### 0.2.0 — 2026-09-04

#### Added
- macOS app: lens list, marks table, live preview, printing.
- USB support by way of a raw CUPS queue — untested, and write-only, so
  it loses the tape check and the battery guard. See `Docs/usb-testing.md`.

### 0.1.0 — 2026-09-04

#### Added
- RingKit: marks, layout, and the Brother raster protocol.
- **Ticks are stamped at whole-dot positions.** A 0.8 mm tick is 5.67
  dots at 180 dpi, and anti-aliasing a fractional-width bar then
  thresholding it leaned every mark 0.088 mm the same way — far too small
  to see, quite large enough to matter.
- 18 mm tape geometry from Brother's raster reference: 128 pins, 16 bytes
  a line, 8 dots of offset and 112 printable, on exact byte boundaries.
- PackBits verified against the manual's own worked example.
