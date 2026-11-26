---
name: "slideworks-deck"
description: "Build consulting-grade PowerPoint slides and decks with the Slideworks connector, which picks curated layouts on the Slideworks master and renders them. Use whenever the user asks for a deck, presentation, slides, a board update, a SteerCo pack, an executive summary slide, or to add or replace a slide, and the Slideworks MCP tools (search_references, get_reference_slots, render_deck) are available."
---

# Slideworks deck building

Slideworks holds a library of real consulting slides on the Slideworks master and renders the file. You decide the argument, the evidence on each slide and every word. Never draw a slide yourself or with any other tool.

Follow these six steps in this exact order. Do not skip a step.

For one or two slides (adding or replacing a slide, one summary page), plan only that slide in step 1 and run steps 2 to 6 for it.

## Step 1: Storyline, no layouts yet

Read the whole source. State the one question the deck answers for a leadership audience, and the answer in one sentence. A deck from a report is a decision deck unless the user asks for a primer, a fact pack or an overview in those words.

Then write the slide titles in order. When the user names no length, a deck from a source is 12 to 15 slides including the cover. Slide 2 is the executive summary, titled with the answer. The deck ends on the recommendation and next steps. At most three back-up slides follow; if the source has data problems, one of them lists them. Add an agenda only when the user asks for one.

Every title is a full-sentence claim with the number or comparison that proves it, written without a full stop. Read the titles alone: they must make the whole case.

**Put several related facts on one slide, not one fact per slide.** Cover every part of the source that bears on the question by combining what belongs together: two measures for the same regions, a project's size with its stages and its buyers, a structure with each party's terms. A slide that shows one series of figures and nothing else is too thin: join it with the facts that explain it.

For each slide note three things only: the claim, the facts and figures from the source that prove it (exactly as the source gives them), and the kind of relationship that evidence shows, in a few words. Name what is related to what: two measures compared across segments, parties and what each one holds, stages with what happens and what comes out of each, sources feeding one system, items with their status and next step, options weighed against conditions, drivers each with a figure. "A ranking" alone is rarely the whole relationship.

At least half of the body slides carry figures from the source. Use every figure that bears on the argument. When a figure is doubtful, show it and flag the doubt on the slide; do not leave it out. With no source, invent one concrete illustrative case, say so, and mark its slides ILLUSTRATIVE.

Do not decide how any slide looks yet.

## Step 2: Browse the library for every slide

Call `browse_deck` once with the deck's type (`decision`, `proposal`, `primer`, `research_report`, `workshop` or `update`) and the relationship of every slide except the cover, in deck order. The call carries nothing of the deck's content.

Each relationship is written in general words. It contains no subject matter: no brand, product, industry or topic words. Use generic nouns such as players, options, criteria, segments, drivers, periods, stages, parties and figures. Good relationships:

- "two players compared across several criteria showing where one trails"
- "criteria that together define one target segment, leading to a result"
- "segments compared on two measures that point in opposite directions"
- "three parties, what each one holds and where their roles overlap"

Never describe the layout you want, and never write "no chart", "no icons" or similar. Leave out counts. Set `numeric: true` only when the slide's evidence is a series of figures to plot.

If nothing returned fits a slide, browse that slide once more with a different relationship. Only if that also fails, call `find_layout` with one sentence describing the structure with counts, and take its top hit. Use this fallback for at most three slides; for any others, take the closest browse result and shape the content to it. If `browse_deck` is not among your tools, call `search_references` once per slide with limit 6 and `min_quality` 4, all together. Do not call `route_deck`.

The cover is the layout `title-image-box`; read it with `get_layout_schema`.

**House layouts.** These slides have a fixed home among the core layouts. Use the layout by name, read it with `get_layout_schema`, and leave the slide out of the `browse_deck` call:

- The executive summary (slide 2): `executive-summary` for four messages, or `executive-summary-two-or-three-paragraphs-and-icons` for two or three claims with their support.
- A plan over time, when the source gives the dates or weeks: `project-plan-with-phases-and-workstreams-by-week` for phases with their workstreams, or `project-plan-with-workstreams-names-dates-and-weeks` for workstreams with owner, due date and status.
- Risks with their mitigation, rated on likelihood and impact: `risk-mitigation`.
- The team: `team-overview-with-pictures` for names and roles, or `team-profiles-with-square-pictures` for two to five people with a short profile.
- A strategy on one page, from the vision down to its elements: `project-vision-and-strategy-house`.
- Three to five equal points without figures: `icon-paragraph-columns`.
- An agenda, when the user asks for one: `agenda`, or `content-overview-circles` when each section needs a sentence. A section divider is `section-breaker`.

If the content does not fit the house layout's capacity, browse that slide like any other.

## Step 3: Pick one composition per slide

Choose from each candidate's name, description, capacity and "When filling" note, and from the thumbnails if you can see them.

- The structure must match the relationship the claim makes.
- Your content must fit the stated capacity: no padding to fill it, and no dropping a fact the claim needs.
- Reject a slide that holds clearly more items than you have, and any slide your content would fill less than half of. It will come out half empty.
- The slide needs a place for the "so what", unless the title already carries it. **A chart never stands alone:** take a chart composition with a text panel, a second exhibit or a takeaway beside it, not a full-width chart with nothing to read.
- Never use the same composition twice in the deck.
- The first candidate in a list is not the answer: read all of them and take the one that shows the most of what the slide has to say.

## Step 4: Write each slide to its slots

Call `get_reference_slots` once for all chosen reference slides (`get_layout_schema` for the cover and for any layout from `find_layout`). Follow each "How to fill this slide" note exactly and stay inside every character budget. If your text is too long, shorten the wording and keep every number.

**Fill the slide.** These slides were drawn full. Write each text box to at least half its character budget, with the source's figures, reasons and consequences. A label or a figure stays short; a box of body text with one short line reads as unfinished.

Figures: use only the source's figures, with their units, periods and qualifiers. Recompute every derived figure (growth, share, difference) and label it as calculated. Never invent a number, a date or a size. If a required slot cannot be filled from the source, go back to step 3 and pick another composition.

Slides that state your own judgement (options weighed, recommendations) carry the sticker TEAM ASSESSMENT and name the slides they rest on. Back-up slides carry BACK-UP.

## Step 5: Render once and review

Call `render_deck` once with every slide in order, starting with the cover. The cover carries the deck's name and a short subtitle, not a claim or a figure. Read the automatic checks for each slide. If you can see the preview images, look at every one. If you cannot see them, say so plainly and do not claim that you checked how a slide looks.

Fix any slide that is flagged, half empty or has text cut off, and re-render only the changed slides using `from` and `keep`. Re-render at most twice. If a slide says more than the source supports, correct it before you deliver.

## Step 6: Deliver and report back

Deliver the .pptx that `render_deck` returns, once. In the PowerPoint add-in, insert it once and keep source formatting. Never rebuild, move, resize or recolour anything afterwards; to change a slide, render it again.

Then list, one line per slide: the title, the name of the composition, and whether it is a reference slide or a core layout. After the list, say which slides are team judgement, every data problem you found in the source, the parts of the source the deck does not use, any slide you could not fix, and whether you could see the thumbnails and previews.

## When you need more

`references/handbook.md` holds the detail behind these steps: deck types, chart choice, numbers and sources, stickers and footnotes, themes and the PowerPoint add-in. Open it only for a question these steps do not answer. `references/worked-example.md` is a complete short run.
