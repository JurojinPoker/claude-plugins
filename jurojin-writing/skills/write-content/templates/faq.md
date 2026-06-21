# Template: FAQ entry (format-neutral)

Describes the *structure and voice* of an FAQ entry. Rendering (accordion,
shortcode, React component) comes from the repo's writing-profile — not here.

## Shape of a single entry

- **Question** — phrased the way a user would actually ask it, in their words
  (not internal/product jargon). One concrete question per entry.
- **Answer (concise)** — lead with the direct answer in 1–2 sentences. The user
  should get unblocked without reading further.
- **Expansion (optional)** — steps, caveats, or context, only if needed. Use a
  list when there are discrete steps.
- **Related links (optional)** — point to the relevant guide or another FAQ.

## Voice

- Plain, reassuring, second person ("you / tú" per the brand doc's language).
- No hype, no filler. Answer first, explain second.
- Use the canonical product terms from the brand glossary; don't invent synonyms.

## A good vs weak answer

- Weak: "Our system architecture allows for plugin synchronization." (vague,
  internal framing)
- Good: "Yes — your room plugins update automatically when you launch Jurojin.
  If one is missing, see [Reinstalling plugins]." (direct, user framing, linked)

## When grouping entries

- Order by what the most users hit first (install / access / billing usually top).
- Group under clear sections only when there are enough entries to warrant it.
