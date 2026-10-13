# Motion spec — [Project]

**Version:**  
**Target platforms:**  

## Principles (this project)

1.
2.

## Global tokens

| Token | Value | Notes |
| --- | --- | --- |
| `duration.fast` | 150ms | Micro feedback |
| `duration.medium` | 250ms | Panel transitions |
| `duration.slow` | 400ms | Page-level (use sparingly) |
| `easing.standard` | cubic-bezier(0.4, 0, 0.2, 1) | |
| `easing.enter` | | |
| `easing.exit` | | |

## Animations

| ID | Trigger | Elements | Properties | Duration | Easing | Reduced motion |
| --- | --- | --- | --- | --- | --- | --- |
| `onboarding.step-advance` | Next click | Step indicator, content | opacity, translateY | 250ms | standard | Instant swap, no translate |
| | | | | | | |

## Prototype links (Figma)

-

## Open questions

-
