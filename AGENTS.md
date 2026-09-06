# Agent Guidelines: Editorial Portfolio Design

These rules apply when using this skill to create or refine another frontend portfolio.

## Before implementation

- Read `design.md` completely before making visual or layout decisions.
- Confirm the audience, role, primary conversion action, content language, and available assets.
- Inspect the existing app structure, routing, styling system, and data model before adding components.
- Preserve the host project's framework conventions. Do not replace an existing styling system only to reproduce this design direction.

## Architecture

- Keep page composition in focused section components.
- Keep project and experience content in typed data files, not inside presentational markup.
- Prefer stable IDs/slugs and explicit image metadata.
- Keep client-side code limited to interactions that need state, pointer events, keyboard events, or browser APIs.
- Use progressive enhancement: the page must still communicate its content if animation or JavaScript is unavailable.

## Visual implementation

- Establish color, type, spacing, radius, and container tokens before styling individual cards.
- Use a display font for expressive headings and a neutral sans for interface text; do not use display styling for every element.
- Build the mobile one-column composition first, then add desktop grid areas and asymmetric spans.
- Give cards a single purpose and a clear internal hierarchy.
- Keep the content shell aligned while allowing selected media or background video to extend edge-to-edge.
- Do not copy reference websites literally. Adapt the principles to the new project's identity.

## Interaction rules

- Every hover effect needs a touch/static equivalent.
- Every carousel needs drag or tap navigation, left/right keyboard controls, visible state, and a one-image fallback.
- Interactive controls inside a draggable surface must be excluded from the parent drag gesture.
- Lightboxes need an accessible name, close control, Escape support, focus return, and swipe/arrow navigation when there are multiple images.
- Scroll-driven state must be derived from measured positions and throttled with `requestAnimationFrame`.
- Use `prefers-reduced-motion` to disable autoplay and nonessential motion.

## Responsive verification

For every UI change, inspect at least one small mobile, tablet, and desktop viewport. Check:

- menu background, close area, and focus order;
- fixed navigation overlap;
- bento gaps, card order, and image crops;
- typography wrapping and readable line length;
- carousel hit areas, drag behavior, and lightbox fit;
- marquee clipping and page-level horizontal overflow;
- reduced-motion behavior.

## Performance and accessibility

- Use optimized responsive images with accurate `alt` text and sensible loading priorities.
- Keep decorative images and icons out of the accessibility tree when they duplicate nearby text.
- Prefer CSS transitions and small utilities over adding animation dependencies.
- Avoid large autoplay media unless it materially supports the concept; provide a fallback.
- Preserve visible focus styles and semantic headings, landmarks, buttons, and links.

## Verification checklist

- Run the project's lint command.
- Run its tests or add a focused test for new interaction logic.
- Run a production build before claiming completion.
- Check the changed flow manually at mobile, tablet, and desktop widths.
- Report pre-existing failures separately from regressions introduced by the change.
