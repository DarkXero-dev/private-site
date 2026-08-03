# My Story Page Rewrite Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the hardship-focused, donation-heavy content of `src/components/tabs/TabMyStory.astro` with an uplifting "new chapter" narrative centered on the move to Thessaloniki, Greece, while keeping past hardship as a brief condensed backstory.

**Architecture:** Single-file content rewrite. No new components, no new CSS, no build/tooling changes. Reuses the existing `info-card` class and heading pattern already used by every other tab in `src/components/tabs/`.

**Tech Stack:** Astro 6, Tailwind CSS 4 (via `@tailwindcss/vite`), no test framework in this repo — verification is `astro build` (which type-checks `.astro` files) plus a visual check via `astro dev`.

## Global Constraints

- No job specifics in the copy — user explicitly asked not to describe the job, only that it's a "foot in the door" role.
- No hardcoded dates that will read as stale (e.g. do not write "training starts tomorrow" literally — phrase as a current/recent milestone).
- Keep the Ko-fi support ask, but lighter tone: "help me get fully established" framing, not "or I have to go back" framing.
- Keep the XeroLinux "project isn't slowing down" line, short.
- Keep the old "Life in Lebanon" video reference, but demoted to a small link-card in the backstory section (not a full click-to-embed feature).
- All new images are Wikimedia Commons free-license Thessaloniki landmark photos, loaded via `Special:FilePath?width=1200` (verified working, ~185-355KB each), each with `loading="lazy"` and descriptive `alt` text, and marked with `<!-- TODO: swap for real Thessaloniki photo -->` so they're easy to find and replace later.
- One video slot is a placeholder (no real Thessaloniki video exists yet), marked `<!-- TODO: swap in real Thessaloniki video -->`, showing a landmark photo with a "Video coming soon" label — no fake play button/click behavior.
- Reuse the `max-w-4xl mx-auto space-y-8` wrapper and `info-card p-5` card pattern already used in this file today.

---

### Task 1: Rewrite TabMyStory.astro content

**Files:**
- Modify: `src/components/tabs/TabMyStory.astro` (full content replacement, entire file)

**Interfaces:**
- Consumes: existing global CSS classes `info-card`, CSS vars `--font-heading`, `--color-accent`, `--color-accent-light`, `--color-accent-dark`, `--color-accent-dim`, `--color-text-primary`, `--color-text-secondary` (all already defined elsewhere in the project's global styles — confirmed in use by the current version of this same file).
- Produces: nothing consumed by other files — this tab is rendered standalone by whatever parent includes `TabMyStory.astro` (unchanged include point, unchanged component name/path).

- [ ] **Step 1: Replace the full file content**

Replace the entire contents of `src/components/tabs/TabMyStory.astro` with:

```astro
---
// My Story tab — personal narrative
---

<div class="max-w-4xl mx-auto space-y-8">
  <h2 class="font-[family-name:var(--font-heading)] text-lg text-[var(--color-accent)]">My Story</h2>

  <!-- Intro -->
  <div class="info-card p-5">
    <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
      Life's taken some unexpected turns - <strong class="text-[var(--color-text-primary)]">Lebanon</strong>,
      <strong class="text-[var(--color-text-primary)]">Ireland</strong>,
      <strong class="text-[var(--color-text-primary)]">Serbia</strong>, and now
      <strong class="text-[var(--color-text-primary)]">Greece</strong>. This is where that road led:
      a fresh start in Thessaloniki, and the beginning of a new chapter.
    </p>
  </div>

  <!-- Where I've Been (condensed backstory) -->
  <div class="space-y-3">
    <h3 class="font-[family-name:var(--font-heading)] text-sm text-[var(--color-accent)] uppercase tracking-widest">
      Where I've Been
    </h3>
    <div class="info-card p-5 space-y-4">
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
        In 2019 I took a job at <strong class="text-[var(--color-text-primary)]">Apple</strong> in
        <strong class="text-[var(--color-text-primary)]">Cork, Ireland</strong> - the dream on paper, a lot
        harder in practice, and I came back home worn out. On
        <strong class="text-[var(--color-text-primary)]">August 4, 2020</strong>, I was on the phone with my
        father when the Beirut port explosion happened - I heard it live. I went back to Lebanon anyway,
        straight into a currency collapse and years of grinding it out with no real way forward. Thanks to
        the incredible generosity of the <strong class="text-[var(--color-text-primary)]">Linux community</strong>,
        I was able to leave and make it to <strong class="text-[var(--color-text-primary)]">Serbia</strong>,
        which bought me the time and stability to keep looking for the next step.
      </p>
      <div class="flex flex-wrap items-center gap-3">
        <a href="https://bytes.xerolinux.xyz/posts/the-move/" target="_blank" rel="noopener noreferrer"
           class="inline-flex items-center gap-2 text-xs font-medium text-[var(--color-accent)] hover:text-[var(--color-accent-light)] transition-colors hover:underline">
          <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13.5 6H5.25A2.25 2.25 0 003 8.25v10.5A2.25 2.25 0 005.25 21h10.5A2.25 2.25 0 0018 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25"/></svg>
          Read the full story on XeroBytes
        </a>
        <a href="https://www.youtube.com/watch?v=wlk_NLJO3lM" target="_blank" rel="noopener noreferrer"
           class="inline-flex items-center gap-2 rounded-lg overflow-hidden border border-[var(--color-accent-dim)] hover:border-[var(--color-accent)] transition-colors">
          <img src="https://img.youtube.com/vi/wlk_NLJO3lM/hqdefault.jpg" alt="Life in Lebanon video thumbnail"
               class="w-24 h-14 object-cover" loading="lazy" />
          <span class="text-xs font-medium text-[var(--color-text-secondary)] pr-3">Watch: Life in Lebanon</span>
        </a>
      </div>
    </div>
  </div>

  <!-- New Chapter: Thessaloniki -->
  <div class="space-y-3">
    <h3 class="font-[family-name:var(--font-heading)] text-sm text-[var(--color-accent)] uppercase tracking-widest">
      New Chapter: Thessaloniki
    </h3>

    <div class="info-card p-5 space-y-4">
      <!-- TODO: swap for real Thessaloniki photo -->
      <div class="rounded-lg overflow-hidden">
        <img src="https://commons.wikimedia.org/wiki/Special:FilePath/White_Tower_of_Thessaloniki_by_Joy_of_Museums_-_3.jpg?width=1200"
             alt="The White Tower of Thessaloniki, Greece"
             class="w-full h-auto"
             loading="lazy" />
      </div>
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
        That search finally paid off: I landed a job in <strong class="text-[var(--color-text-primary)]">Thessaloniki, Greece</strong>,
        and made the move. New city, new country, new page. It's still early days, but for the first time
        in a long time the direction feels right.
      </p>
    </div>

    <div class="info-card p-5 space-y-4">
      <!-- TODO: swap for real Thessaloniki photo -->
      <div class="rounded-lg overflow-hidden">
        <img src="https://commons.wikimedia.org/wiki/Special:FilePath/Aristotelous_Plateia_2006_(cropped).jpg?width=1200"
             alt="Aristotelous Square, Thessaloniki"
             class="w-full h-auto"
             loading="lazy" />
      </div>
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
        I've got my own rented apartment here now - first real foothold in ages. Between admin paperwork
        and getting everything set up, it's been a lot, but every box ticked is one step further into
        building an actual life here.
      </p>
    </div>

    <div class="info-card p-5 space-y-4">
      <!-- TODO: swap for real Thessaloniki photo -->
      <div class="rounded-lg overflow-hidden">
        <img src="https://commons.wikimedia.org/wiki/Special:FilePath/Thessaloniki_-_Paralia_-_1.JPG?width=1200"
             alt="Thessaloniki waterfront (Nea Paralia)"
             class="w-full h-auto"
             loading="lazy" />
      </div>
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
        The job itself isn't the end goal - it's a foot in the door while I keep looking for something
        better paid. Training's starting soon, and I'm going in ready to make the most of it. One step
        at a time.
      </p>
    </div>

    <!-- TODO: swap in real Thessaloniki video -->
    <div class="info-card p-5 space-y-3">
      <div class="relative rounded-lg overflow-hidden">
        <img src="https://commons.wikimedia.org/wiki/Special:FilePath/Rotunda_of_Galerius.jpg?width=1200"
             alt="The Rotunda of Galerius, Thessaloniki"
             class="w-full h-56 object-cover" loading="lazy" />
        <div class="absolute inset-0 bg-black/50 flex items-center justify-center">
          <span class="text-white text-sm font-medium tracking-wide uppercase">Video coming soon</span>
        </div>
      </div>
      <p class="text-xs text-[var(--color-text-secondary)] text-center">
        Working on a proper video about this new chapter - stay tuned.
      </p>
    </div>
  </div>

  <!-- What's Next -->
  <div class="space-y-3">
    <h3 class="font-[family-name:var(--font-heading)] text-sm text-[var(--color-accent)] uppercase tracking-widest">
      What's Next
    </h3>
    <div class="info-card p-5 space-y-4">
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
        The plan now: get settled, build up some real stability, and keep an eye out for a better
        opportunity here in <strong class="text-[var(--color-text-primary)]">Greece</strong>. And no matter
        what changes, <a href="https://xerolinux.xyz" target="_blank" rel="noopener noreferrer"
           class="text-[var(--color-accent)] hover:text-[var(--color-accent-light)] transition-colors hover:underline">XeroLinux</a>
        keeps moving - being in a steadier place if anything means more energy to put into it, not less.
      </p>
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed italic">
        Do or do not. There is no try.
      </p>
    </div>
  </div>

  <!-- Support -->
  <div class="space-y-3">
    <h3 class="font-[family-name:var(--font-heading)] text-sm text-[var(--color-accent)] uppercase tracking-widest">
      Help Me Build On This
    </h3>
    <div class="info-card p-5 space-y-4">
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
        If you want to help me get fully on my feet in this new chapter, joining a
        <strong class="text-[var(--color-text-primary)]">monthly tier on Ko-fi</strong> goes a long way.
        It's not about survival anymore - it's about building something solid, and every bit of support
        speeds that up.
      </p>
      <div class="flex justify-center pt-2">
        <a href="https://ko-fi.com/XeroLinux" target="_blank" rel="noopener noreferrer"
           class="inline-flex items-center gap-2 px-5 py-2.5 text-sm font-medium text-white bg-[var(--color-accent-dark)] hover:bg-[var(--color-accent)] transition-colors rounded-lg shadow-lg shadow-[var(--color-accent-dim)]">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round"><path d="M17 8h1a4 4 0 0 1 0 8h-1"/><path d="M3 8h14v9a4 4 0 0 1-4 4H7a4 4 0 0 1-4-4Z"/><line x1="6" y1="2" x2="6" y2="4"/><line x1="10" y1="2" x2="10" y2="4"/><line x1="14" y1="2" x2="14" y2="4"/></svg>
          Support on Ko-fi
        </a>
      </div>
    </div>
  </div>

  <!-- Thank You -->
  <div class="space-y-3">
    <h3 class="font-[family-name:var(--font-heading)] text-sm text-[var(--color-accent)] uppercase tracking-widest">
      Thank You!
    </h3>
    <div class="info-card p-5 space-y-4">
      <p class="text-sm text-[var(--color-text-secondary)] leading-relaxed">
        To everyone who's helped along the way, whether with money, a share, or just a kind word - thank
        you. Getting here took a long road, and none of it would've been possible without people showing
        up for me. Here's to the next chapter.
      </p>
    </div>
  </div>

  <!-- XeroBytes link -->
  <div class="flex justify-end">
    <a href="https://bytes.xerolinux.xyz/posts/the-move/" target="_blank" rel="noopener noreferrer"
       class="inline-flex items-center gap-2 text-xs font-medium text-[var(--color-accent)] hover:text-[var(--color-accent-light)] transition-colors hover:underline">
      <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13.5 6H5.25A2.25 2.25 0 003 8.25v10.5A2.25 2.25 0 005.25 21h10.5A2.25 2.25 0 0018 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25"/></svg>
      Read the full post on XeroBytes
    </a>
  </div>
</div>
```

Note: the old file's `<script>` block (click-to-embed for the YouTube video) is intentionally dropped — the video is now a plain link-card (`<a href="https://www.youtube.com/watch?v=...">`), so there's no embed to trigger and no dead script left behind.

- [ ] **Step 2: Run the Astro build to verify the file is valid**

Run: `npm run build`
Expected: build completes with no errors or warnings referencing `TabMyStory.astro`.

- [ ] **Step 3: Visually verify in the dev server**

Run: `npm run dev`, open the site, navigate to the "My Story" tab.

Check:
- All 4 Wikimedia images load (White Tower, Aristotelous Square, waterfront, Rotunda).
- "Video coming soon" overlay renders correctly on the placeholder card.
- The "Watch: Life in Lebanon" link-card shows the YouTube thumbnail and opens the video in a new tab when clicked.
- The "Read the full story on XeroBytes" links (both the one in the backstory card and the footer one) point to `https://bytes.xerolinux.xyz/posts/the-move/`.
- The Ko-fi button opens `https://ko-fi.com/XeroLinux` in a new tab.
- No leftover references to the old dropped script (browser console has no errors about `getElementById('yt-player')` or similar).

- [ ] **Step 4: Commit**

Do not run `git commit` — hand the exact command to the user to run themselves:

```bash
git add src/components/tabs/TabMyStory.astro
git commit -m "Rewrite My Story page: uplifting Thessaloniki new-chapter narrative"
```

---

## Self-Review Notes

- **Spec coverage:** all 7 sections from the spec (intro, backstory, new-chapter with 3 cards + video placeholder, what's next, support, thank you, footer link) are present in Task 1's file content. All 3 required Wikimedia photo URLs plus the extra Rotunda photo for the video placeholder are included, each with `loading="lazy"`, `alt` text, and a `TODO` comment. The old video is demoted to a link-card per spec. No job specifics are described anywhere in the copy. No hardcoded "tomorrow" date — phrased as "training's starting soon."
- **Placeholder scan:** no TBD/TODO-without-content; the two `TODO` HTML comments are intentional markers called out explicitly in the spec, not unfinished work — they point at concrete swap-later assets, not vague future work.
- **Type consistency:** N/A (single Astro template file, no shared functions/types across tasks).
