@AGENTS.md

# Rules for working in this project

This project is run by a designer with no technical background. They build screens from Figma with Claude's help.

## Communication
- Explain every action in plain words, without jargon. If a technical term can't be avoided, briefly explain what it means.
- Before a big change, briefly say what you are going to do and in which files.
- After every successful step (a section is built, a component is created, a bug is fixed), suggest committing the changes and offer a ready-made commit message.
- Commit and push only after the designer agrees. If the current branch is `master`, create a new branch first.

## Design system (required, overrides the rules below if they conflict)
- Always build layouts **only from `DESIGN.md`**. Read it before creating or changing any page or component.
- Use only the tokens and components it describes. Don't invent new colors, sizes, variants or states.
- If the task or a Figma design needs something `DESIGN.md` doesn't cover, or contradicts it, stop and ask the designer.
- When the designer approves an addition or change, update all of these together: `DESIGN.md`, `tokens.json`, `src/styles/tokens.css`, the component in `src/components/ui/`, and the `/components` page.

## Building from Figma
- Build from Figma only through the Figma MCP: take the design context, screenshot and variables from the file instead of guessing.
- After building, compare the result with the Figma screenshot.
- Save images and icons from the design in `src/assets/` and render them with `<Image />` from `astro:assets`. Put only the favicon, fonts and files that don't need processing in `public/`.

## Tokens (required)
- Take colors, fonts, text sizes, spacing and radii **only** from `src/styles/tokens.css` via `var(--...)`.
- No hardcoded values: `#hex`, `rgb()`, `16px` for spacing and the like are not allowed in components.
- If Figma has a value that isn't in `tokens.css`, don't make one up. Tell the designer and suggest adding a new token to `tokens.css`, named the same as the Figma variable.
- If Figma variables differ from `tokens.css`, tell the designer before changing tokens (use `get_variable_defs` to compare).

## Components and folders
- Make every new element a separate `.astro` component in the right folder:
  - `src/components/ui/`: small repeated elements (Button, Input, Card, Badge, Icon).
  - `src/components/sections/`: large page blocks (HeroSection, FeaturesSection, Footer, Header).
  - `src/layouts/`: page skeletons (BaseLayout).
  - `src/pages/`: the pages themselves. Each file here is a separate site address.
- Name files in PascalCase: `Button.astro`, `HeroSection.astro`.
- Before creating a new component, check whether something similar already exists in `ui/`. Reuse and extend it through props instead of duplicating.
- Pass text that changes through props or `<slot />`.
- Write styles in a `<style>` block inside the component. They automatically apply only to that component.

## Responsive layout
- Build mobile-first: write the base styles for mobile and add larger screens with `@media (min-width: ...)`.
- Breakpoints: 768px (tablet), 1024px (desktop), 1440px (wide screen). They are defined in `tokens.css`.
- Check that there is no horizontal scrolling at 375px.
- Use flex/grid and relative units. Don't give blocks a fixed width.

## Checks
- Run the dev server in the background: `astro dev --background`.
- Before committing, check that `npm run build` finishes without errors.
