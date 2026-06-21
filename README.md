# claude-plugins

Jurojin's Claude Code **plugin marketplace**. A marketplace is just a git repo
that lists plugins; this one hosts shared skills + brand knowledge so multiple
repos (JurojinWeb, the blog, …) consume one source instead of copying docs around.

## Plugins

| Plugin | Type | What it does |
|--------|------|--------------|
| `jurojin-writing` | Skill + knowledge | Writing skill (guides, FAQs, release news, CTAs) grounded in `business.md` brand knowledge; renders to each repo's format via a local `writing-profile.md`. |

## Layout

```
.claude-plugin/marketplace.json     ← marketplace manifest (name: "jurojin")
jurojin-writing/                     ← the writing plugin (installed unit)
  .claude-plugin/plugin.json
  business.md                        ← brand/business knowledge (single source, bundled)
  skills/write-content/
    SKILL.md                         ← orchestrates: brief + brand + template + repo profile
    templates/{faq,news,guide}.md    ← format-neutral content structures
examples/
  writing-profile.jurojinweb.md      ← copy into JurojinWeb as .claude/writing-profile.md
  writing-profile.strapi.md          ← copy into the blog repo as .claude/writing-profile.md
```

## How it works

- **Plugin = portable brain.** Ships the writing skill + brand knowledge; travels
  with any repo that enables it, including cloud/single-repo runs (no siblings).
- **Repo = local adapter.** Each consuming repo commits a `.claude/writing-profile.md`
  describing its output format and components (React/MDX in JurojinWeb, Strapi
  markdown/shortcodes in the blog). The skill reads that profile to render.
- **Brand content stays fresh two ways:** bundled in the plugin (offline /
  reproducible) **and** fetchable at the raw URL of `business.md` on `main`
  (always-latest). The skill prefers the fetch and falls back to the bundle:
  `https://raw.githubusercontent.com/JurojinPoker/claude-plugins/main/jurojin-writing/business.md`

## Resources & components (writer cheat sheet)

To support a piece and its narrative, the writer needs to know **what elements it
can use** in the current repo — not just prose. So each consuming repo provides a
**components cheat sheet** inside its `.claude/writing-profile.md`, split into:

- **Standard elements** — portable building blocks (headings, bold, links,
  images, lists, blockquotes, dividers…).
- **Custom elements** — repo/renderer-specific widgets that add real value
  (preview cards, highlight/CTA banners, video embeds, feature tables, playing
  cards, etc.).

The **same logical element renders differently per platform** — which is exactly
why this lives in each repo, not in the skill. Example, a "preview page" card:

| Platform | Syntax |
|----------|--------|
| Blog / Strapi (markdown CMS) | `[preview](https://jurojinpoker.com/en/solution/SLUG)` |
| JurojinWeb (React) | `<PagePreviewWidget href="https://jurojinpoker.com/en/solution/SLUG" />` |

The skill reads this cheat sheet and emits the correct syntax for the active repo,
so it can enrich the piece with the resources actually available. See the
filled-in examples in `examples/writing-profile.*.md`.

## Writing profile (per-repo contract)

Every consuming repo **must** provide a writing profile — the local adapter that
tells the skill *how to render*. It is created and committed **in the consumer
repo**, not here.

- **Canonical path:** `.claude/writing-profile.md` (fallback: `docs/writing-profile.md`).
  This is exactly where the skill looks.
- **Required sections:**
  1. **Output format** — target language/CMS and rendering notes.
  2. **Resources & components** — the cheat sheet (standard + custom elements).
  3. **Conventions** — imports, frontmatter/metadata, link schemes, limits.
  4. **Example** — a short rendered snippet.
- **How to create one:**
  - Start from `examples/writing-profile.template.md` (blank skeleton), or
  - copy the closest filled example: `examples/writing-profile.jurojinweb.md`
    (React/JSX) or `examples/writing-profile.strapi.md` (markdown CMS).
  - If the skill runs in a repo with no profile, it will offer to scaffold one
    from the template.

## Install (manual, once per machine)

```
/plugin marketplace add JurojinPoker/claude-plugins
/plugin install jurojin-writing@jurojin
```

Pull newer brand/skill changes into a local install:

```
/plugin marketplace update jurojin
```

## Auto-enable per repo (cloud runs included)

Declaring the marketplace + plugin in a repo's **committed** `.claude/settings.json`
makes Claude Code install it **automatically at session start — including cloud /
headless sessions, with no trust prompt** (the only requirement is network access
to reach GitHub). This is the supported way to make a single-repo cloud run pick
up the plugin without any sibling folder.

```jsonc
{
  "extraKnownMarketplaces": {
    "jurojin": {
      "source": { "source": "github", "repo": "JurojinPoker/claude-plugins" }
      // optional: pin a version with  "ref": "v0.1.0"  (branch, tag or commit)
    }
  },
  "enabledPlugins": {
    "jurojin-writing@jurojin": true
  }
}
```

Scope notes:
- Use `.claude/settings.json` (committed) so the team and cloud sessions inherit it.
- `.claude/settings.local.json` works but is gitignored (personal, not shared).
- User settings `~/.claude/settings.json` are **not** honored in cloud sessions.

Verified against the official docs (plugin-marketplaces, settings, claude-code-on-the-web).

## Per-repo setup checklist

1. Copy the matching `examples/writing-profile.*.md` into the repo as
   `.claude/writing-profile.md` and fill in the real components/imports.
2. Add the `settings.json` block above (committed).
3. Ask the writer skill to draft something and confirm it renders in the repo's
   format.

## Editing brand content

`jurojin-writing/business.md` is the single source. Edit it here, commit, and:
- the skill's runtime fetch (raw URL on `main`) picks it up immediately;
- cloud sessions reinstall fresh at startup;
- local installs get it on the next `/plugin marketplace update jurojin`.

## Security & trust

Plugins are executable, trusted code. Only enable marketplaces you control or
trust. This marketplace ships skills + a markdown knowledge file (no hooks/MCP
servers today); review `business.md` before publishing since it is fetched
publicly.

## Troubleshooting

- **Plugin doesn't auto-install in a session:** confirm the block is in the
  *committed* `.claude/settings.json`, the keys are exactly
  `extraKnownMarketplaces` / `enabledPlugins`, and the session has network access
  to GitHub.
- **Skill can't find `business.md`:** it should fetch the raw URL above; offline,
  it reads the bundled copy at the plugin root.
- **Stale brand content on a local install:** run `/plugin marketplace update jurojin`.

Remote: `JurojinPoker/claude-plugins`.
