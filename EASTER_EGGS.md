# Hidden Features & Easter Eggs — Full Site Reference

Internal reference covering `landing.html`, `login.html`, `register.html`, and `library.html`. Not linked anywhere on the site — keep it that way so they stay secret.

## Quick Reference — All Secret Keywords/Codes

Type these anywhere on the page (not while focused in a text input):

| Keyword / Code | Page(s) | Effect |
|---|---|---|
| `lego` | landing.html | Secret Vault brick wall reveal |
| `batcave` | login.html, register.html | Batcomputer terminal overlay |
| `chaos` | register.html | LEGO playing cards rain down |
| `arkham` | register.html | Purple "Arkham Mode" screen filter |
| `brick` | library.html | Every jobsheet card explodes apart, then reassembles shuffled |
| ↑↑↓↓←→←→BA (Konami code) | login.html, register.html | Auto-fills Bruce Wayne + instant success |

Other non-keyword triggers: click the header logo 5× fast (landing.html, Brick Rain), click any empty area repeatedly (landing.html, Brick Graffiti), open the same page in 2 tabs (landing.html, Cross-Tab Ghost).

---

# landing.html

## Secret Vault
- **Trigger**: type `lego` anywhere on the page (not while focused in a text input).
- **Effect**: fullscreen red brick wall splits open left/right, reveals a "Secret Vault Unlocked" card.
- **Close**: X button on the card.
- Code: `setupSecretVault()` in landing.html, keyword buffer matched on `keydown`.

## Brick Rain
- **Trigger**: click the "OUR WORKSPACE" logo (top-left, header) 5 times within 2 seconds.
- **Effect**: 60 colored bricks fall from the top of the screen + "Brick Rain Unlocked!" toast.
- Code: `setupBrickRain()`.

## Brick Graffiti
- **Trigger**: click any empty (non-interactive) area of the page.
- **Effect**: stamps a small colored LEGO brick sticker at that spot. Persists in `localStorage` (`graffiti-bricks-v1`), capped at 150 bricks (oldest removed first). Survives reload.
- **Reset**: small dark circular eraser button, fixed bottom-left corner (low opacity until hover) — clears all stamped bricks.
- Code: `setupGraffiti()`, reset via `clearGraffiti()` wired to `#graffitiResetBtn`.

## Cross-Tab Builder Ghost
- **Trigger**: open `landing.html` in two tabs/windows of the same browser.
- **Effect**: each tab's mouse cursor shows up as a colored ring ("BUILDER") in the other tab, live, via `BroadcastChannel`. Ghost disappears 3s after the other tab stops moving/closes.
- Only works same-browser, same-origin (no server involved) — won't work across different browsers or devices.
- Code: `setupCrossTabGhosts()`.

## Minifigure Color Customizer + Reset
- **Trigger**: color swatches under the hero CTA (visible, not secret) — click a color to recolor the whole minifigure, click the white refresh circle to restore original per-part colors.
- Code: `setupMiniCustomizer()`.

## Sound-Reactive Stud Pulse
- Not a "trigger" — passive. Every click sound briefly pulses the hero's dot-grid background opacity in sync with the actual Web Audio `AnalyserNode` output of that click. Subtle, easy to miss without watching for it.
- Code: `runStudPulse()` inside `playClickSound()`.

## Mouse-Parallax Hero Depth
- Not secret — passive. Moving the mouse over the hero section shifts the grid pattern, headline block, and minifigure at different depths/speeds.
- Code: `setupHeroParallax()`.

## Wall-Crumble Transition
- Not secret — visible on scroll. The black strip between "Meet The Builders" and "Assembly Instructions" is a 40-tile brick wall that crumbles apart once scrolled into view.
- Code: `setupWallCrumble()`.

## Easter Egg Hunter Achievement
- Finding all 4 hidden secrets above (Secret Vault, Brick Rain, Brick Graffiti, Cross-Tab Ghost) unlocks the 🥚 "Easter Egg Hunter" badge on dashboard.html's Achievements wall.
- Each secret sets its own `localStorage` flag when triggered: `egg-found-vault`, `egg-found-brickrain`, `egg-found-graffiti`, `egg-found-ghost`. Same-origin, so dashboard.html reads them directly.
- Replaces the old "Detailed Feedback" (💬 commentator) achievement — removed per request.
- Check logic: `ACHIEVEMENT_DEFS` entry `id: 'egg_hunter'` in dashboard.html.

localStorage keys: `graffiti-bricks-v1`, `egg-found-vault`, `egg-found-brickrain`, `egg-found-graffiti`, `egg-found-ghost`.

---

# login.html

Main floating character: **Batman**. Occasional cameo: **Joker** (peeks in, Batman reacts and shoos him off).

## Batcave Terminal
- **Trigger**: type `batcave` anywhere on the page (not while focused in a text input).
- **Effect**: fullscreen green-on-black hacker terminal overlay with typed-in flavor lines. Close button to dismiss.
- Code: `setupBatcaveEasterEgg()`, keyword buffer matched on `keydown`.

## Konami Code Autofill
- **Trigger**: ↑ ↑ ↓ ↓ ← → ← → B A (standard Konami code, keyboard).
- **Effect**: auto-fills Staff ID "Bruce Wayne" / password "ImBatman1!", then instantly runs the success flow (green flash, confetti, redirect to dashboard.html).
- Code: `setupKonami()`.

## Batman Interactive Reaction
- **Trigger**: click the floating Batman.
- **Effect**: bounce/spin animation + random speech-bubble quip + a short synthesized "thump" sound.
- Code: `reactBatman()`.

## Joker Cameo
- **Trigger**: automatic — first fires ~4s after page load, then every ~28s.
- **Effect**: Joker peeks in from the left edge near the logo, Batman reacts ("Not today, Joker!"), Joker retreats.
- Code: `jokerCameo()`.

## Password Strength Brick Tower
- Not secret — visible. 5 small bricks under the password field fill/color as you type a stronger password.
- Code: `updatePasswordStrength()`.

## Sign-In Validation Feedback
- Not secret — visible. Empty fields on submit → card shakes + flashes red. Filled fields → green flash + confetti + redirect.
- Code: `signInAsInstructor()`.

## ID Badge Flash
- **Trigger**: focus the Staff ID field.
- **Effect**: small 🪪 badge icon slides in beside the field with a quick white flash.
- Code: `showIdBadge()` / `hideIdBadge()`.

## Grappling Hook Cursor, Bat-Signal Spotlight, Night Rain, Skybox, Typewriter Subtitle, Card Unfold Entrance
- Not secret — ambient/passive polish, active across the whole page. Bat-signal glow follows the mouse (hover the yellow area); rain only appears at night (device clock, 8pm–5am); skybox tints the yellow panel by time of day.

---

# register.html

Main floating character: **Joker** (swapped from login.html). Occasional cameo: **Batman** (peeks in, Joker reacts and shoos him off — roles reversed from login.html).

Everything from login.html's shared feature set is replicated here (nav underline, grappling cursor, bat-signal, night rain, skybox, typewriter subtitle, card entrance animation, Batcave terminal, Konami code) — see login.html section above for those. This section only covers what's different or register-specific.

## Batcave Terminal
- Same as login.html — type `batcave` anywhere on the page.

## Konami Code Autofill
- **Trigger**: ↑ ↑ ↓ ↓ ← → ← → B A.
- **Effect**: auto-fills Full Name "Bruce Wayne", Faculty "Applied Sciences", Email "bruce.wayne@wayneenterprises.com", Password "ImBatman1!", then instantly runs the register success flow (redirects to login.html).
- Code: `setupKonamiReg()`.

## Card Rain
- **Trigger**: type `chaos` anywhere on the page.
- **Effect**: 50 LEGO-style playing cards (♠♥♦♣) rain down and fade out, staggered.
- Code: `spawnCardRain()` / `setupCardRainEasterEgg()`.

## Arkham Mode
- **Trigger**: type `arkham` anywhere on the page.
- **Effect**: fullscreen purple radial-gradient filter + glowing "ARKHAM MODE" text for 3 seconds, then fades out.
- Code: `setupArkhamEasterEgg()`.

## Joker Interactive Reaction
- **Trigger**: click the floating Joker.
- **Effect**: bounce/spin animation + random speech-bubble quip + synthesized sound.
- Code: `reactJoker()`.

## Joker Success Flourish
- **Trigger**: automatic, on successful registration (all fields filled).
- **Effect**: Joker does a distinct 720° spin+scale flourish (different animation from the normal click reaction) with the line "Welcome to the family!", alongside the usual green flash + confetti.
- Code: flourish branch inside `registerInstructor()`.

## Batman Cameo (role-swapped)
- **Trigger**: automatic — first fires ~4s after page load, then every ~28s.
- **Effect**: Batman peeks in near the logo, Joker reacts ("Not now, Bat-Brain!"), Batman retreats.
- Code: `batmanCameoReg()`.

## Batman Interruption Counter
- Not secret — passive, subtle. Small low-contrast text bottom-left of the yellow panel ("Batman interruptions: N") that increments every time the Batman cameo fires. Persists in `localStorage` (`batman-interruptions-reg`).
- Code: `bumpBatInterruptCounter()`.

## Wanted Poster Live Preview
- **Trigger**: type into the Full Name field.
- **Effect**: a small western "WANTED" poster card pops up on the register card's top-right corner showing the typed name live.
- Code: `updateWantedPoster()`.

## Villain Alias Generator
- **Trigger**: click the "Feeling chaotic? Generate villain name" link under Full Name.
- **Effect**: fills Full Name with a random joke villain alias (e.g. "Miss Mayhem") and updates the Wanted Poster.
- Code: `generateVillainName()`.

## Joker Faculty Quip
- **Trigger**: focus the Faculty/Department field (fires once per page load).
- **Effect**: Joker reacts with a random sarcastic one-liner about faculty/bureaucracy.
- Code: `jokerFacultyQuip()`.

## Chaos Meter Password Bar
- Not secret — visible. Purple-to-green gradient bar under the password field labeled "Chaos Level: Low/Rising/Unstable/Chaotic/MAXIMUM" as you type a stronger password. Register's equivalent of login.html's brick tower.
- Code: `updateChaosMeter()`.

## Register Card Flip Entrance
- Not secret — visible on load. The register card flies in from the right like a thrown playing card (540° spin), instead of login.html's box-unfold.
- Code: `cardFlipInReg` keyframes.

localStorage keys added: `batman-interruptions-reg`.

---

## Achievement Tie-In (dashboard.html)
- 🥚 "Easter Egg Hunter" badge unlocks after finding landing.html's 4 secrets (Secret Vault, Brick Rain, Brick Graffiti, Cross-Tab Ghost) — see landing.html section above. login.html/register.html/library.html secrets are not currently wired into this achievement.

---

# library.html

Redesigned to match dashboard.html's visual language (Anton font, lego-border/has-studs brick styling, blue-gradient body). Jobsheet cards render live from the same `uploaded-jobsheets-v3` localStorage data dashboard.html uses.

## Card Explode & Reassemble
- **Trigger**: type `brick` anywhere on the page.
- **Effect**: every visible jobsheet card flies apart (random translate/rotate/scale, fades out), then re-renders in shuffled display order with a staggered pop-in animation. Display order only — doesn't touch the underlying stored data.
- Code: `explodeAndReassembleCards()` / `setupBrickExplodeEasterEgg()`.

## Rarity Badges
- Not secret — passive, computed from real data. A small ribbon appears on a card's top-left corner:
  - 🥇 **First Brick** — the very first jobsheet ever uploaded (chronological, by id).
  - 🏆 **Milestone #N** — every 5th upload (5th, 10th, 15th...).
  - ⭐ **Golden Brick** — any reviewed jobsheet with a mark ≥ 90 (takes priority over the other two).
- Badge position is computed against the full chronological upload order, so it never shifts as you search/filter.
- Code: `computeRarityBadge()`.

## Featured Build Spotlight
- Not secret — passive. One random Reviewed jobsheet with mark ≥ 80 gets a gold glowing border + "★ Featured Build" ribbon. Re-picked whenever the current featured job is deleted or the page reloads; stays stable across searches/filters otherwise.
- Code: `pickFeaturedJob()`.

## Card Flip-Reveal
- **Trigger**: click the small 🔄 icon bottom-right of any card (not a hover — hovering would fight with clicking the View button underneath).
- **Effect**: 3D flip reveals the back face — title, mark, and a truncated instructor comment. Click ↩️ on the back to flip back.
- Code: `.jc-flip-outer` / `.flipped` class toggle, inline `onclick` in `renderJobsheets()`.

## Drag Card to Trash to Delete
- **Trigger**: drag any jobsheet card onto the red trash-bin circle that appears bottom-right while dragging.
- **Effect**: same deletion as the modal's 🗑 Delete Jobsheet button (updates progress count, activity-log, upload-log). Confirms first.
- Code: `setupDragToTrash()`.

## Drag-and-Drop Upload Zone
- Not secret — visible. Drop a file directly onto the "Drop file or click" box in the upload panel instead of using the native file picker. A small brick tower preview stacks up taller for bigger files.
- Code: `setupUploadDropzone()` / `handleFileSelected()`.

## Brick-Snap Hover Sound
- Not secret — passive. A soft, short "tick" plays when the cursor first moves over a card (throttled to at most once per 250ms so sweeping across the grid doesn't spam it).
- Code: `playHoverTick()`, delegated via `setupHoverSound()`.

## Delete Jobsheet (modal)
- Not secret — visible, 🗑 Delete Jobsheet button inside the detail modal. Same underlying `deleteJobsheet()` as the drag-to-trash version above.
