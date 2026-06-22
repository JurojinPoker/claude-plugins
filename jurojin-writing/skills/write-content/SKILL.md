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
     `https://raw.githubusercontent.com/JurojinPoker/claude-plugins/main/jurojin-writing/business.md`
   - If there is no network, fall back to the bundled `business.md` at this
     plugin's root (the directory two levels up from this SKILL.md).

2. **The piece template.** Read the format-neutral template for what you are
   writing, from the `templates/` folder next to this SKILL.md:
   - `faq.md` — FAQ entries
   - `news.md` — release / news posts
   - `guide.md` — how-to / help guides
   These describe **structure and voice only**, not how to render.

3. **The repo writing-profile.** Look for a repo-local profile that declares the
   output format and a **components cheat sheet** (standard + custom elements).
   Check, in order:
   - `.claude/writing-profile.md`
   - `docs/writing-profile.md`
   If found, emit in **that** format using **those** components/import rules, and
   actively use the available custom elements (preview cards, CTA banners, video
   embeds, feature tables…) to support the narrative — not just prose.
   **If the profile declares a publication pipeline or command for full articles**
   (a blog post, a help-center entry, etc.), **defer to that pipeline** for those
   pieces instead of drafting standalone — it owns metadata, validation and
   publishing, and will call back here for the body.
   If **not** found: tell the user no profile was detected, **offer to scaffold
   `.claude/writing-profile.md`** from the template
   (`https://raw.githubusercontent.com/JurojinPoker/claude-plugins/main/examples/writing-profile.template.md`),
   and meanwhile emit clean Markdown.

## Before drafting: set the brief

Settle these three with the user **up front** — they shape the whole piece. If the
user hasn't specified one, ask before writing:

1. **Objective** — what the piece is for (educate, rank for SEO, announce a
   feature, convert, onboard, etc.). One clear primary objective.
2. **Length** — approximate target:
   - **Short** ≈ 500 words
   - **Medium** ≈ 1000 words
   - **Long** ≈ 1500 words
   Treat as a guide, not a hard cap; serve the objective.
3. **CTA** — there is no default. Confirm the action it should drive (download,
   upgrade to a bundle, join Discord, read /pricing, etc.).

4. **Language** — default is **English**. If the user specifies a different
   language for the piece, write in that language throughout (including headings,
   CTAs, and any UI labels). Do not ask about language unless the user's request
   is ambiguous about it.

Restate the agreed objective / length / CTA back briefly before drafting, so the
brief is explicit.

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
