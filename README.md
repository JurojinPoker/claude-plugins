# claude-plugins

Jurojin's Claude Code **plugin marketplace**. A marketplace is just a git repo
that lists plugins; this one hosts shared skills + brand knowledge so multiple
repos (JurojinWeb, the blog, …) consume one source instead of copying docs around.

## Layout

```
.claude-plugin/marketplace.json   ← marketplace manifest (name: "jurojin")
business.md                       ← brand/business knowledge (single source)
jurojin-writing/                  ← the writing plugin
  .claude-plugin/plugin.json
  skills/write-content/
    SKILL.md                      ← orchestrates: brand + template + repo profile
    templates/{faq,news,guide}.md ← format-neutral content structures
examples/
  writing-profile.jurojinweb.md   ← copy into JurojinWeb as .claude/writing-profile.md
  writing-profile.strapi.md       ← copy into the blog repo as .claude/writing-profile.md
```

## How it works

- **Plugin = portable brain.** Ships the writing skill + brand knowledge.
- **Repo = local adapter.** Each consuming repo commits a `.claude/writing-profile.md`
  describing its output format and components (React/MDX in JurojinWeb, Strapi
  markdown/shortcodes in the blog). The skill reads that profile to render.
- **Brand content stays fresh two ways:** bundled in the plugin (offline /
  reproducible) **and** fetchable at the raw URL of `business.md` on `main`
  (always-latest). The skill prefers the fetch and falls back to the bundle.

## Install (manual, once per machine)

```
/plugin marketplace add JurojinPoker/claude-plugins
/plugin install jurojin-writing@jurojin
```

To pull newer brand/skill changes into a local install:

```
/plugin marketplace update jurojin
```

> Cloud / ephemeral sessions resolve a fresh install at startup, so they get the
> latest automatically. The runtime fetch of `business.md` keeps brand content
> latest in both local and cloud.

## Auto-enable per repo (so cloud runs just work)

In each consuming repo's `.claude/settings.json`, declare the marketplace and
enable the plugin so a session installs it on startup:

```jsonc
{
  "extraKnownMarketplaces": {
    "jurojin": {
      "source": { "source": "github", "repo": "JurojinPoker/claude-plugins" }
    }
  },
  "enabledPlugins": {
    "jurojin-writing@jurojin": true
  }
}
```

> ⚠️ Verify these exact settings keys against your Claude Code version before
> committing — a silent typo here just means no auto-install. (Ask Claude to
> confirm with the claude-code-guide.)

## Per-repo setup checklist

1. Copy the matching `examples/writing-profile.*.md` into the repo as
   `.claude/writing-profile.md` and fill it in with the real components/imports.
2. Add the `settings.json` block above.
3. Ask the writer skill to draft something and confirm it renders in the repo's
   format.

## Editing brand content

`business.md` is the single source. Edit it here, commit, and:
- cloud runs + the skill's runtime fetch pick it up immediately;
- local installs get it on the next `/plugin marketplace update jurojin`.

Remote: `JurojinPoker/claude-plugins`. The raw URL the skill fetches is
`https://raw.githubusercontent.com/JurojinPoker/claude-plugins/main/business.md`.
