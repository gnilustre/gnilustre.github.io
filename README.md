# Gabriel | CV Website

A modern, single-page CV website with a liquid glass navigation bar, smooth scroll animations and light/dark themes. Built with plain HTML, CSS and JavaScript. No frameworks, no build step, no dependencies.

<!-- Add a screenshot: save it as screenshot.png in this folder, then uncomment the line below -->
<!-- ![Screenshot of the CV website](screenshot.png) -->

## Features

- **Liquid glass navigation:** a floating, frosted-glass nav with a glowing rim, a highlight that follows your cursor, and a selection bubble that stretches as it glides between sections
- **Smooth animations:** the name rises in letter by letter on load, content fades up as you scroll, and a progress bar fills along the top of the screen
- **Light and dark mode:** follows the visitor's system setting, with a toggle that remembers their choice
- **Responsive:** the section links move to a floating bar at the bottom of the screen on phones
- **Print-friendly:** "Print or save as PDF" produces a clean, ink-friendly CV
- **Accessible:** skip link, keyboard focus styles, semantic HTML, and respect for the "reduce motion" and "reduce transparency" system settings
- **Handy details:** live local-time chip, copy-email button, downloadable CV link

## Project structure

```
.
├── index.html    # page structure, content and the small script
├── style.css     # all styling, animation and theming
├── cv.pdf        # your CV (add this yourself)
└── photo.jpg     # optional portrait (add this yourself)
```

## Run it locally

No install needed. Open `index.html` in a browser.

For a local server instead:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Make it yours

Every place to edit is marked with an `EDIT` comment in `index.html`. The main ones:

1. **Name and role:** the `<h1>`, the role line, and the page `<title>`. Each letter of the name is its own `<span class="l" style="--i:N">`, so keep one per letter, with `N` counting up from 0.
2. **Intro sentence:** replace the bracketed text. The highlighted words are the `.key` spans.
3. **Quick facts:** the four tiles under the hero (currently, based in, experience, available).
4. **About, Experience, Education, Skills:** replace the placeholder text. Copy a `<li class="entry">` block to add another job or course.
5. **Contact:** your email (in both the link and the `data-copy` attribute), LinkedIn and GitHub links.
6. **Files:** put `cv.pdf` next to `index.html`. For a photo, add `photo.jpg` and swap `<span>G</span>` for `<img src="photo.jpg" alt="Photo of Gabriel">`.
7. **Structured data:** update the `application/ld+json` block near the top so search engines understand the page.

### Colours and fonts

All colours live in two blocks at the top of `style.css` (`:root` for light, `:root[data-theme="dark"]` for dark). Change `--accent` to recolour the whole site. The font is [Geist](https://fonts.google.com/specimen/Geist) from Google Fonts, with a system font fallback.

## How the liquid glass works

It is an imitation of Apple's liquid glass effect, built from standard browser features:

| Language | What it does |
| --- | --- |
| **CSS** | `backdrop-filter` blurs and saturates what is behind the nav. A semi-transparent gradient tints it. Layered `box-shadow` values add the shine. A masked `::before` layer draws the rim, and a radial-gradient `::after` layer is the pointer highlight. The selection bubble moves with a spring-style `cubic-bezier` curve. |
| **SVG** | An inline `<filter>` uses `feImage` and `feDisplacementMap` to bend the page behind the edges of the glass like a lens. It is applied with `backdrop-filter: url(#lg-wide)`. |
| **JavaScript** | Detects Chromium to switch the lens effect on, passes the cursor position to CSS as `--mx` and `--my`, and briefly adds a `moving` class so the bubble stretches while it travels. |
| **HTML** | A few class names (`glass`, `glass-wide`, `glass-round`) and the inline SVG filter. |

Most of the visual work is CSS. JavaScript only handles decisions, like which section you are in and remembering your theme.

## Browser support

- **Chromium browsers (Chrome, Edge, Brave):** full effect, including the lens distortion at the glass edges.
- **Safari and Firefox:** the nav falls back to frosted glass without the lens distortion. Everything else works the same.
- **Reduced motion or reduced transparency:** animations are switched off, and the nav becomes solid.

## Deploy with GitHub Pages

1. Push these files to a GitHub repository.
2. Go to **Settings > Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose the `main` branch and the `/ (root)` folder, then save.
5. After a minute or two your site is live at `https://[your-username].github.io/[repository-name]/`.

## License

Choose a license for your repository, such as [MIT](https://choosealicense.com/licenses/mit/), and add it as a `LICENSE` file. Replace this section with the name of the license you pick.
