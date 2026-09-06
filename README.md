# Editorial Portfolio Design Skill

`editorial-portfolio-design` is a reusable Codex skill for creating frontend portfolios with an editorial, minimal, human, and recruiter-friendly feel.

It is based on the design direction of this portfolio, but it is intentionally written as a flexible system rather than a clone. Use it as a starting point, then adapt the colors, typography, content, imagery, and interactions to each project's identity.

## What it covers

- Editorial visual direction and content hierarchy
- Warm neutral color system and display/sans typography pairing
- Responsive containers, grids, and bento layouts
- Hero, work index, project detail, experience, and contact patterns
- Coverflow galleries, lightboxes, marquees, and scroll reveal
- Mobile-first interaction and keyboard accessibility
- Reduced-motion behavior and performance considerations
- Data-driven project and experience content

## Package contents

```text
editorial-portfolio-design/
├── SKILL.md      # Skill entrypoint and usage boundaries
├── design.md     # Reusable design system and layout patterns
├── AGENTS.md     # Implementation rules for coding agents
└── README.md     # This overview and setup guide
```

## How to use it

1. Copy the `editorial-portfolio-design` folder into the target project's skill directory or into your personal Codex skills directory.
2. Invoke the skill by its name: `editorial-portfolio-design`.
3. Provide the project's role, audience, content, assets, framework, and primary goal.
4. Ask the agent to read `design.md` for visual decisions and `AGENTS.md` for implementation constraints.

Example prompt:

```text
Use the editorial-portfolio-design skill to create a responsive portfolio for a frontend developer.
Prioritize recruiter scanning, use the provided projects as the source of truth, and adapt the visual system to the brand colors.
```

## Recommended placement

For a single project, keep the skill beside the project while designing. For reuse across projects, copy it to a shared skills directory such as `~/.codex/skills/` or `.agents/skills/`.

The skill only provides design and implementation guidance. It does not include a starter application, project data, fonts, images, or a fixed framework.

## Important boundaries

- Do not reproduce another website's code, branding, content, or distinctive assets.
- Do not preserve the reference layout when it conflicts with the new project's content or accessibility needs.
- Do not add animation, autoplay media, fake metrics, or decorative UI without a clear communication purpose.
- The user's brief and real project data always take priority over the reference system.
