# My Story Page Rewrite — Design Spec

Date: 2026-08-03
File touched: `src/components/tabs/TabMyStory.astro`

## Goal

Rewrite the "My Story" tab from a hardship-focused, donation-heavy narrative into an
uplifting "new chapter" story centered on the recent move to Thessaloniki, Greece: new
job (foot-in-the-door role), own rented apartment, admin/training in progress, and an
optimistic outlook. Past hardship (Lebanon, Ireland/Apple, Beirut explosion, Serbia) is
kept but condensed into a brief "Where I've Been" backstory instead of being the
emotional center of the page.

## Content facts (from user, verbatim intent)

- Kept applying to jobs after Serbia until landing one in Thessaloniki.
- Now has own rented apartment in Thessaloniki.
- Currently handling admin/paperwork; training starts "tomorrow" relative to the post
  date — phrase this as a recent/current milestone, not tied to a hardcoded date that
  will go stale.
- Job is explicitly a "foot-in-the-door" role, not the end goal — actively looking for
  better-paid work. Do not describe job specifics (per user instruction).
- Tone: cheerful, uplifting, "how I battled through to get here," beginning of a new
  adventure — not dwelling on the struggle.

## Section structure

1. **Intro card** — reframed. Short, forward-looking opener: life took you from Lebanon
   through hardship to a fresh start in Thessaloniki, Greece. Sets uplifting tone
   immediately (no "no filter, no sugarcoating" hardship framing as the lead).

2. **"Where I've Been" card (condensed backstory)** — 2-3 sentences covering Ireland/Apple,
   the Beirut explosion (Aug 4 2020), return to Lebanon, and the move to Serbia via
   community support. Ends with a small inline link to the full XeroBytes post
   (`https://bytes.xerolinux.xyz/posts/the-move/`) and a compact link-card (not full
   embed) to the old "Life in Lebanon" YouTube video (id `wlk_NLJO3lM`) for anyone who
   wants the full story. This replaces the multiple full hardship chapters in the old
   version.

3. **"New Chapter: Thessaloniki" section** — the emotional core of the page, multiple
   info-cards:
   - Arrival/new start card with a Thessaloniki landmark photo (White Tower).
   - "Own place, own start" card (apartment, admin/training) with a second landmark
     photo (Aristotelous Square).
   - "Foot in the Door" card about the job — framed as a stepping stone, optimistic,
     no job specifics — with a third photo (Thessaloniki waterfront / Nea Paralia).
   - A video-embed slot styled like the existing `yt-thumb`/`video-wrap` pattern, but
     as a clearly marked placeholder (HTML comment `<!-- TODO: swap in real Thessaloniki
     video -->`) since no real video exists yet. Placeholder shows a static Thessaloniki
     photo (waterfront) with a "Video coming soon" label instead of a fake play button
     that goes nowhere.

4. **"What's Next" card** — short, forward-looking: building stability, still job
   hunting for something better-paid, XeroLinux work continuing unaffected (short
   paragraph, same as before but trimmed).

5. **Support card (Ko-fi)** — kept, lighter tone: framed as "help me get fully
   established in this new chapter" rather than "or I have to go back." Same Ko-fi
   button/link (`https://ko-fi.com/XeroLinux`).

6. **Thank you card** — kept, tone adjusted to match the uplifting arc (gratitude for
   getting this far, not "hardest stretch of my life" framing as the emotional peak).

7. **XeroBytes footer link** — kept as-is.

## Images

No personal Thessaloniki photos exist in the repo yet. Use free-license Wikimedia
Commons landmark photos as scene-setting placeholders, sized via Wikimedia's
`Special:FilePath` thumbnail redirect (confirmed working, ~200-350KB each vs multi-MB
originals):

- White Tower: `https://commons.wikimedia.org/wiki/Special:FilePath/White_Tower_of_Thessaloniki_by_Joy_of_Museums_-_3.jpg?width=1200` (CC BY-SA 4.0)
- Aristotelous Square: `https://commons.wikimedia.org/wiki/Special:FilePath/Aristotelous_Plateia_2006_(cropped).jpg?width=1200` (Public Domain)
- Waterfront (Nea Paralia): `https://commons.wikimedia.org/wiki/Special:FilePath/Thessaloniki_-_Paralia_-_1.JPG?width=1200` (CC BY-SA)

All three get `loading="lazy"` and descriptive `alt` text, matching the existing pattern
used for the Reuters photo in the current page. Each image sits in a comment-marked
placeholder so they're easy to find and swap for real photos later:
`<!-- TODO: swap for real Thessaloniki photo -->`.

## Video

- Old "Life in Lebanon" video (`wlk_NLJO3lM`): kept as a small link-style card in the
  backstory section (thumbnail + link out to YouTube), not a full lazy-loaded embed.
  Reuses the existing thumbnail-image approach but without the click-to-embed script
  behavior — simpler since it's no longer the featured video.
- New Thessaloniki video: no real video exists. One placeholder slot in the new-chapter
  section, visually consistent with `.video-wrap`/`.yt-thumb` styling, labeled "Video
  coming soon," no click behavior (nothing to embed yet). Marked with a TODO comment.

## Technical notes

- Reuse existing `info-card` CSS class and heading pattern
  (`font-[family-name:var(--font-heading)] text-sm text-[var(--color-accent)]
  uppercase tracking-widest`) for section headers — no new CSS needed.
- Keep the existing inline `<script>` only for the backstory video thumbnail if it stays
  interactive; if downgraded to a plain link-card, the click-to-embed script can be
  removed entirely (simplifies the file, no dead code left behind).
- No new Astro components — this stays a single-file content rewrite of
  `TabMyStory.astro`, consistent with how the other tabs are structured.
- No build/tooling changes required.

## Out of scope

- No changes to `TabAbout.astro` or other tabs.
- No real Thessaloniki personal photos/video — those are TODO placeholders for the user
  to swap in later.
- No changes to Ko-fi/XeroLinux links themselves, only surrounding copy tone.
