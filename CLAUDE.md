# Ridhi Malhotra Portfolio: working context

Portfolio site for **Ridhi Malhotra**, Content Designer & Strategist (14+ years, DGM – UX Copy & Strategy at Airtel).
This file records where things live, how to build and ship, the decisions made, and the rules to keep.

## Where it lives

| What | Where |
|---|---|
| Live site | https://ridhimalhotra-ux.github.io/ (GitHub Pages, repo `ridhimalhotra-ux/ridhimalhotra-ux.github.io`, branch `main`) |
| Local clone of the site (built output only) | `~/portfolio-code` on Ridhi's MacBook |
| Preview artifact (claude.ai) | https://claude.ai/artifact/VRhgv5pppuQ83qhDq4TuEM (comment threads: https://claude.ai/code/artifact/e632ced5-ce3b-4a79-a909-09e1646eb296) |
| Source code (React + TypeScript) | `/home/claude/portfolio` in the Claude cloud session. **Not in git and not on the Mac. It will be lost when the session ends unless copied.** |

The GitHub repo has only the built `index.html`, the CV PDF and a standalone `bill-simplification/` page. To change the site, edit the source, rebuild, then copy `dist/index.html` over `~/portfolio-code/index.html`.

## Build and ship

```bash
cd /home/claude/portfolio
npx tsc --noEmit                      # type check
node scripts/build.mjs                # → dist/index.html (site), dist/artifact.html (claude.ai preview)
PLAYWRIGHT_BROWSERS_PATH=/opt/pw-browsers python3 scripts/test-render.py   # smoke test: must print ALL CHECKS PASSED
```

- Images are embedded as base64 by generators: `scripts/gen-casestudy-images.py` (assets/casestudies → src/generated/caseImages.ts) and `scripts/gen-hero-images.py` (banner collage → src/generated/heroImages.ts).
- Ship: copy `dist/index.html` to `~/portfolio-code/index.html`, commit, then **Ridhi runs `git push` on her Mac**. The push uses her SSH key; Claude's sessions can't push.
- Don't overwrite `~/portfolio-code/Ridhi-Malhotra-CV.pdf` (the Content Design & Strategy CV) or `bill-simplification/`.
- Before shipping, check `git log` in `~/portfolio-code` for edits made directly to the site and carry them into the source first. That happened once already (see "Edits made on the site" below).

## Source map

- `src/data/home.ts`: intro and headline, nav, timeline roles, education, collaborators, places, impact tiles.
- `src/data/studies.ts`: case-study content (10-part framework). `FEATURED`, `MORE`, `BEYOND` and `HIDDEN` decide what shows.
- `src/data/projects.ts`: project metadata, covers, Figma prototype links.
- `src/data/caseStudies.ts`: Engage X and Bill Simplification. `sideProjects.ts`: F1 app and Insight Hub. `awards.ts`, `capabilities.ts`.
- `src/components/Home.tsx`: all home sections (banner collage, journey, skills, people, places, projects, impact, beyond, recognition, footer).
- `src/components/CaseStudy.tsx` and `Widgets.tsx`: the case-study page.
- `src/styles.css`: the base design system plus versioned blocks appended at the end. **Later blocks override earlier ones.** The current theme is "Theme v18" plus "Banner ground".

## Current state (5 Nov 2026)

**Page order:**
1. Banner
2. My content journey
3. Skills
4. People I work with
5. Places
6. My Projects
7. Impact
8. Beyond work
9. Recognition and awards (at the bottom)
10. Footer

**Nav:** Experience | Projects | Download CV.

**Banner:**
- A slow vertical collage of real work, with no hover effects: Help Home, Engage X, Ask Me Anything, the Airtel Finance category page, and 12 brand pieces from `Content Portfolio.pptx` (OLX, foodpanda, Medlife, Friendship Day).
- Background #F7F4EE.

**Headline (Ridhi's exact words):**
> AI-driven communications and experience strategist with 14+ years of expertise spanning content, brand, marketing, and product strategy, creating meaningful customer experiences and business impact.

**Palette:**

| Role | Colour |
|---|---|
| Background | White #FFFFFF |
| Primary | Burgundy #642D42 (headings, links, metrics, the "Strategy & leadership" phase) |
| Accent | Dusty blush #E8C9CE (tags, borders, highlights) |
| Secondary | Warm beige #F3EDE8 (alternate sections) |
| Text | Charcoal #333039 |
| Banner | #F7F4EE |

Typeface: Open Sans throughout.

**Journey:**
- The Writing phase runs 2012–2016.
- Marketing & campaigns runs 2015–2019. It starts halfway across the foodpanda card (Jun 2015) and is one solid colour.
- After those come UX & product content (2019–2020) and Strategy & leadership (2020–now).

**Projects:**
- Featured: Engage X, Help Home, AI-Powered Navigation: Ask Me Anything (Bot) & Next Best Action (Reminders), and Airtel Finance (cover: the personal loan screen).
- "View more" (5): Chatbot, Call Manager, Payments & UPI, Content Principles, Brand & Marketing.

**Hidden, not deleted:** Bill Simplification. It is listed in `HIDDEN` in `studies.ts`, along with its "1 rule" impact tile. On the live site, `#work-bill-simplification` redirects to `bill-simplification/`.

**Impact tiles:**
- 66% less setup time
- ₹30 Cr revenue in one quarter
- 2× click-through
- ~10% fewer Help drop-offs
- +15% loan applications
- +10% credit card applications
- 50+ stakeholders
- 3 writers

## Edits made on the site (kept)

These were made directly in the deployed `index.html` and have been ported into the source:
- Figma **prototype** links (`figma.com/proto/...&scaling=min-zoom`).
- LinkedIn: https://www.linkedin.com/in/ridmalhotra/
- Airtel Finance personal loan image (`finance-loan`).
- Engage X screen notes without the crossed-out original copy (`hideFrom: true`).
- Projects intro: "...a self-service redesign, AI navigation and a lending journey."

## Rules

- **Never invent facts or metrics.** Keep personal, team and product results, and targets, separate. Every result shows its scope.
- **Metrics left out on purpose:** the voicebot 7%, the 40–55% attribution range, ₹16 CPC vs CAC, the Medlife push CTR and the Valentine's campaign numbers. Don't re-add the "20M+ MAUs" banner fact either. 3× conversions has no baseline or period.
- **No email address anywhere on the page.** Ridhi asked for it removed.
- Don't add images of other people's characters or likenesses (the Joey post, the Game of Foods parody, book covers).
- Use Ridhi's wording exactly when she gives it.
- Keep text readable: colour contrast at least 4.5:1, and check light mode, dark mode and phone width.
- Feature names: "Ask Me Anything (Bot)" and "Next Best Action (Reminders)". "Ask Anything" stays only where it is the label shown in the app.

## Source files Ridhi supplied

- `Portfolio_26.pdf`
- The Engage X, Bill Simplification, Insight Hub and F1 Saudi GP case-study PDFs
- Help Home and Ask Anything screenshots
- On her Mac, in `~/Downloads`: `Content Portfolio.pptx` (brand work, the same file as the Drive link `1UsPA0cMwbByuJ3BPa06CPmOqX4wCbC5w`), `Case Study - Airtel Finance.pdf` and the CVs

## Open items

- **Push the latest commit:** `cd ~/portfolio-code && git push`.
- **Save the source code before this session expires:** copy it to the Mac or a git repo.
- **Download CV on the claude.ai preview doesn't work.** The preview needs the downloads permission, which hasn't been approved. On the live site the link works.
- **Not done yet:** a downloadable PDF of the whole portfolio.
