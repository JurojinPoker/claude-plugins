# jurojin-writing

A Claude Code plugin that writes on-brand Jurojin content — guides, FAQs, release
news and CTAs — grounded in shared brand knowledge, and renders to each repo's
own format.

## What's inside

- **Skill `write-content`** — orchestrates writing: sets the brief (objective /
  length / CTA) with the user, loads brand knowledge, picks a content template,
  and renders through the consuming repo's `writing-profile.md`.
- **`business.md`** — the single source of Jurojin brand/business context. Bundled
  here and also served at a raw URL for always-latest fetch.
- **`skills/write-content/templates/`** — format-neutral structures for `faq`,
  `news`, `guide`.

## How the skill runs

1. **Set the brief** with the user up front: objective, length
   (short ≈500 / medium ≈1000 / long ≈1300 words), and CTA.
2. **Load brand knowledge** (`business.md`, fetched or bundled).
3. **Load the piece template** (faq / news / guide).
4. **Read the repo's `.claude/writing-profile.md`** to know the output format and
   components; render accordingly. No profile → clean Markdown + a heads-up.

## Using it

After the plugin is installed/enabled (see the marketplace
[README](../README.md)), just ask in a consuming repo, e.g.:

> "Write a short FAQ entry about Action Required tiling."

The skill will confirm the brief, then draft in the repo's format.

## Separation of concerns

- This plugin owns **what to say** and **the structure**.
- `business.md` owns **the facts and the voice**.
- Each repo's `writing-profile.md` owns **how to render** (components/imports).

To change brand facts or voice, edit `business.md` here — not the output.
