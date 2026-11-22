# Design: <Project name>

Read before any frontend work. Status: draft | locked (<date>). Locked only after the user approves a mockup or says "apply directly".

## Direction
Style: <minimal | editorial | bold | playful | premium dark | native mobile | from the user's references>
<!-- 3 to 5 lines: mood, references the user gave, what to avoid. -->

## Design system (picked per project)
- Base: <shadcn on Base UI | shadcn on Radix | Astryx (theme: <name>) | none>
- Add-ons allowed when a task needs them: 
- Decorative (opt-in per screen): 
- Tools: 
- Never: Vaul (unmaintained).

## Tokens
<!-- name = value, light and dark. Defined once as CSS variables. -->
| Token | Light | Dark | Use |
|---|---|---|---|
| `--bg` | | | page background |
| `--fg` | | | body text |
| `--accent` | | | primary action |

Type scale: 
Spacing scale: 
Radius: 
Motion: durations, easing (ease-out for enter), reduced-motion behavior.

## Layout and ergonomics
<!-- mobile-first? primary actions bottom-anchored? breakpoints? navigation pattern? -->

## Components
<!-- one line each: name, when to use, which base component it wraps. -->

## Accessibility floors
- Contrast: WCAG AA in light and dark
- Touch targets: at least 44 to 48 px
- Every motion respects `prefers-reduced-motion`
- Real states: loading, empty, error

## Approved mockups
| Task | Path | Approved |
|---|---|---|
