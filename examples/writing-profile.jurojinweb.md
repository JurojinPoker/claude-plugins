# Writing profile — JurojinWeb (example)

Copy this into the **JurojinWeb** repo as `.claude/writing-profile.md` and adjust
to the real component library. The `jurojin-writing` skill reads this to know
*how to render* what it writes here.

## Output format

- Target: **React / MDX** (or `.tsx` pages, per the file the user is editing).
- FAQs and content are composed from imported components, not raw HTML.

## Available components

<!-- TODO: replace with the real components and import paths. -->

| Intent | Component | Import |
|--------|-----------|--------|
| FAQ list | `<FaqAccordion items={[...]} />` | `import { FaqAccordion } from "@/components/faq"` |
| Single Q&A | `<FaqItem question="" >...</FaqItem>` | `@/components/faq` |
| Callout / note | `<Callout type="info">...</Callout>` | `@/components/ui/callout` |
| CTA button | `<CtaButton href="">...</CtaButton>` | `@/components/ui/cta` |
| Step list | `<Steps>...<Step/>...</Steps>` | `@/components/ui/steps` |

## Conventions

- Put imports at the top of the file; group them.
- Deep links to the client use the `jurojin:store*` scheme — use the canonical
  CTA wording from the brand doc, not ad-hoc copy.
- Prefer components over raw markup so styling stays consistent.
<!-- TODO: note any MDX frontmatter the page needs (title, slug, seo). -->

## Example (FAQ entry rendered here)

```tsx
import { FaqItem } from "@/components/faq";

<FaqItem question="Do my room plugins update automatically?">
  Yes — your plugins update when you launch Jurojin. If one is missing, see{" "}
  <a href="/help/reinstalling-plugins">Reinstalling plugins</a>.
</FaqItem>
```
