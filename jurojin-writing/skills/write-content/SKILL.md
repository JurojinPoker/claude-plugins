---
name: write-content
description: Write Jurojin content (guides, FAQs, release news, CTAs) grounded in brand knowledge. Use when asked to draft, write, or edit user-facing copy — a FAQ, a help/guide article, release/news notes, or a call-to-action — for the marketing site, the blog, or the help center.
---

# Jurojin content writer

Produce on-brand content that reads with precision about the Jurojin product.
The skill is **portable** (the brand brain) and **adapts to the repo it runs in**
(the rendering target). Never hardcode component syntax here — that lives in each
repo's writing-profile.

## Always do these three loads first

1. **Brand knowledge.** Load the brand doc so the copy is accurate and on-voice.
   - Prefer the latest published copy (fetch):
     `https://raw.githubusercontent.com/JurojinPoker/claude-plugins/main/business.md`
   - If there is no network, fall back to the bundled copy at
     `${CLAUDE_PLUGIN_ROOT}/business.md`.

2. **The piece template.** Read the format-neutral template for what you are
   writing, from `${CLAUDE_PLUGIN_ROOT}/jurojin-writing/skills/write-content/templates/`:
   - `faq.md` — FAQ entries
   - `news.md` — release / news posts
   - `guide.md` — how-to / help guides
   These describe **structure and voice only**, not how to render.

3. **The repo writing-profile.** Look for a repo-local profile that declares the
   output format and available components. Check, in order:
   - `.claude/writing-profile.md`
   - `docs/writing-profile.md`
   If found, emit in **that** format using **those** components and import rules.
   If not found, emit clean Markdown and tell the user no profile was detected.

## Before drafting: clarify the goal and CTA

There is no default CTA. **Confirm with the user, up front, what this piece is
for and what action it should drive** (download, upgrade to a bundle, join
Discord, read /pricing, etc.). Settle the goal/CTA before writing — it shapes the
whole piece. If the user hasn't said, ask.

## Then

- Draft the piece following the template's structure and the brand voice.
- Never quote prices or bundle amounts — link to `/pricing` instead.
- Frame poker as gaming, not gambling; don't position against trackers (they
  complement Jurojin); don't imply casino partnership or guarantee account safety.
- Render it through the repo profile (e.g. Strapi markdown shortcodes vs
  JurojinWeb React/MDX component imports).
- Keep claims grounded in the brand doc. If something required isn't covered
  there (a price, a hard fact, a feature detail), flag it as `TODO:` rather than
  inventing it.

## Boundaries

- This skill owns *what to say* and *the structure*. The repo profile owns *how
  to render*. The brand doc owns *the facts and the voice*. Don't blur them.
- If asked to change brand facts or voice, that's an edit to `business.md` in the
  marketplace repo, not a one-off in the output.
