# Editorial Portfolio Design System

## 1. Design intent

Create a portfolio that feels like a considered editorial publication with the practicality of a well-made product interface.

- Lead with the person's role and point of view.
- Make selected work scannable in seconds: title, category, year, role, and one clear outcome.
- Use large type, warm surfaces, quiet borders, and a small accent palette to create character without visual noise.
- Use interaction to clarify state or invite exploration, never to hide essential information.
- Keep the design credible for recruiters and useful for collaborators.

The style should feel human through small details: direct copy, imperfect-but-intentional labels, tactile buttons, real process notes, and imagery with context. Avoid random gradients, excessive glass effects, fake metrics, fake testimonials, and motion that exists only to demonstrate a library.

## 2. Visual foundations

### Color

Start with a warm, low-contrast neutral base and one confident accent. The following values are reference tokens, not mandatory brand colors:

```css
:root {
  --background: #f3f0e9;
  --surface: #fbfaf6;
  --surface-dark: #1e2c28;
  --foreground: #171817;
  --muted: #6c6b64;
  --line: #d9d4ca;
  --accent: #ec6d50;
  --positive: #5b9d76;
  --soft-green: #a9d29d;
}
```

Rules:

- Use `--background` for the page, `--surface` for cards, and `--surface-dark` for one or two high-contrast areas.
- Keep borders subtle but visible enough to separate cards and rows.
- Reserve the accent for emphasis, links, active states, and a small number of expressive words.
- Check text contrast whenever a reference token is changed.

### Typography

Use two complementary voices:

- A high-contrast serif or editorial display face for hero headlines, section statements, and project titles.
- A neutral sans-serif for navigation, labels, metadata, descriptions, and controls.

Define roles instead of styling each element independently:

```css
:root {
  --display: Georgia, "Times New Roman", serif;
  --body: Arial, Helvetica, sans-serif;
}

.display-heading {
  font-family: var(--display);
  letter-spacing: -0.06em;
  line-height: 0.9;
}

.eyebrow,
.metadata {
  font-family: var(--body);
  font-size: 0.7rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
```

Use italic display text selectively for a second tone, not as decoration on every heading. Keep body copy short, with a readable measure around 35–65 characters per line.

### Shape, border, and spacing

- Use rounded cards with one consistent radius family; let the radius reduce on small screens when space is tight.
- Prefer thin rules, generous whitespace, and alignment over shadows.
- Use a spacing scale based on `0.25rem` or `0.5rem`, then apply fluid values with `clamp()` for page-level gaps.
- Make interactive targets at least 44px on touch devices.

## 3. Page shell and layout

Use a centered shell with a maximum reading width. The background can extend edge-to-edge while content remains aligned:

```css
.site-shell {
  width: min(100%, 1440px);
  margin-inline: auto;
  padding-inline: clamp(1.25rem, 4vw, 4.5rem);
}
```

Recommended page rhythm:

1. Fixed or sticky navigation with a restrained scrolled state.
2. Full-viewport or near-viewport hero.
3. Short statement/about introduction.
4. Selected work list or grid.
5. Optional tools/stack marquee.
6. Experience or process section.
7. Contact CTA and quiet footer.

Every section should expose a clear `id` when it is a navigation destination. Keep section labels consistent, such as `01 / About`, `02 / Work`, and `03 / Experience`.

## 4. Section patterns

### Navigation

Desktop navigation is quiet and centered. Pair the brand at the start with primary links and a small availability/status indicator. On narrow screens:

- Replace the link row with a menu trigger.
- Open a full-viewport panel with a solid background and clear close control.
- Leave a generous dismissible area below the last link.
- Lock or manage focus appropriately if the panel behaves as a modal.
- Ensure the panel is usable with keyboard and touch; never depend on hover.

### Hero

Use one clear statement, one supporting sentence, one primary route to work, and one visual anchor. A portrait, project image, or quiet looping video may sit behind or beside the content.

- Put video backgrounds outside the content container when edge-to-edge media is needed, but keep text and controls inside the shell.
- Use `muted`, `playsInline`, and `preload="metadata"` for decorative video.
- Add a readable overlay and a static image/fallback for slow or reduced-motion contexts.
- Keep the heading to one memorable idea. Highlight only a phrase or two with the accent color.

### Work index

Treat work as proof, not a gallery of decoration. Each project card should expose title, category, year, role, and an image with meaningful alt text. Keep the whole card or a clear title action clickable, and provide a visible route to the complete work index.

### Project detail

Use a repeatable story structure:

- project title and concise summary;
- role, year, category, and technology tags;
- image gallery or cover image;
- problem/context;
- contribution and implementation decisions;
- highlights and relevant links;
- next project navigation.

For multi-image projects, a central-image coverflow can create personality:

- central card is largest and fully readable;
- adjacent cards are visible as navigable previews;
- dragging and left/right keys move one item at a time;
- side previews can be tapped/clicked as previous/next controls;
- the central image can open a lightbox with close, swipe, and arrow-key support;
- a one-image project renders one static image without carousel controls;
- preserve the previous page when returning from detail.

### About bento

Use a bento grid to turn context into a visual scan. Give the largest tile to a portrait or defining statement and place smaller cards around it. Useful card roles include education, awards, stack, collaboration, craft, visual systems, process, and contact.

- Give each card one idea and one visual hierarchy.
- Use color blocks sparingly: one dark craft card, one soft accent card, and mostly neutral cards is enough.
- Keep education and awards list-like, with dates aligned and supporting organizations subordinate.
- Use CSS grid areas or explicit spans so the composition remains intentional at every breakpoint.
- On mobile, collapse to a logical reading order rather than preserving desktop gaps.

### Experience

Present experience as chapters or a compact timeline. A scroll-driven detail panel can be used when it helps the visitor understand progression:

- keep chapter labels visible;
- derive the active chapter from the nearest visible position, not a fragile scroll-count assumption;
- throttle scroll work with `requestAnimationFrame`;
- allow direct button selection and keyboard focus;
- make the static stacked/timeline view complete when motion is reduced or JavaScript is unavailable.

### Marquees

Use marquees for tools, stack, or a short collaboration CTA only when they add atmosphere without blocking reading.

- Render two identical groups for seamless looping; translate exactly one group width.
- Keep rows clipped inside their section and prevent page-level horizontal overflow.
- Use different directions or datasets only when that improves scanning.
- Do not pause essential information on hover; touch devices have no hover.
- Disable or simplify animation under `prefers-reduced-motion: reduce`.

### Contact

End with one direct invitation, an email or primary contact action, and a small set of social links. Keep the CTA concrete and avoid invented availability claims. A resume link is useful when the portfolio is for job applications.

## 5. Responsive composition

Design the mobile structure first, then expand it for larger screens.

| Viewport | Composition | Interaction focus |
| --- | --- | --- |
| Small mobile | one column, stacked cards, compact hero, full-width controls | tap targets, menu close area, no horizontal overflow |
| Tablet | two-column bento where it helps, reduced display scale | preserve reading order and card proportions |
| Desktop | split hero, asymmetric grid, visible previews, wider type | hover polish plus keyboard alternatives |

Use CSS media queries and fluid values before JavaScript viewport detection. At every breakpoint check:

- text wrapping and heading overflow;
- image crop and aspect ratio;
- grid gutters and empty tracks;
- fixed nav overlap;
- menu background and dismiss behavior;
- touch targets and focus rings;
- marquee clipping and page width;
- lightbox viewport fit.

## 6. Motion language

Motion should feel slow enough to read and fast enough to respond.

- Use opacity and short vertical translation for section reveal.
- Use transform/opacity for card feedback; avoid animating layout-heavy properties when possible.
- Use `requestAnimationFrame` for scroll-derived state.
- Stop scroll-driven animation when scrolling stops; do not use timers to fake continuous scroll progress.
- Keep carousel movement to one predictable step per gesture.
- Respect `prefers-reduced-motion` by removing autoplay, scroll-driven effects, and nonessential transitions.

## 7. Content and asset rules

- Store projects and experience in typed JSON or a small data module separate from presentation.
- Make image fields explicit: source, alt text, optional cover image, and optional gallery.
- Keep mock content replaceable and label it honestly.
- Never invent client names, metrics, awards, testimonials, or employment history.
- Use real project decisions and constraints as the strongest proof of skill.
- Prefer optimized images, responsive `sizes`, lazy loading for below-the-fold media, and metadata-preloaded video.

## 8. Quality bar

Before shipping, verify that a visitor can answer these questions quickly:

1. Who is this person and what role are they pursuing?
2. What work did they build and what did they contribute?
3. How can I inspect the details or contact them?

Then verify keyboard navigation, focus visibility, reduced motion, narrow mobile layout, tablet layout, desktop layout, image loading, missing/empty data, and no unintended horizontal scrolling.
