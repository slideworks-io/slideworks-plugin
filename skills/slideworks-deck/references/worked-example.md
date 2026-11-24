# Worked example: a thin prompt turned into an argued deck

User request, verbatim: *"Make a 4-slide board deck on a growth move."*

This is here to show the **method**, not a deck to reproduce. Another case needs a different storyline, different evidence and different compositions.

## 1. Invent the case, then the argument

The prompt names no company, so invent one and say so in the reply:

> Illustrative case: Fjordvik, a Nordic facilities-services group (cleaning and maintenance, core growing 1–2% a year), considering a move into energy-efficiency retrofits. All figures are fictional.

Then decide what the Board must believe to say yes, one claim per slide, the evidence that proves each one, and the kind of relationship that evidence shows. No layouts yet.

| # | Claim | Evidence | Relationship |
| - | --- | --- | --- |
| 1 | Retrofits are the growth move that uses our base; pilot in 2027 | The argument in three or four points | the governing message supported by a few topics, each with its key points |
| 2 | The market grows 2.5x because both retrofit volume and project value rise | Market value = retrofits per year × average project value, 2019 and 2025F | a market value broken into drivers that multiply out, over time |
| 3 | Retrofits fit our capabilities better than the other growth options | Eight capabilities in three areas, scored for four options (team judgment) | options scored against the capabilities they need |
| 4 | Five decisions are needed today | Decisions, each with an owner and a date | decisions needed now, each with an owner |

The cover is `title-image-box` and is not browsed. Two of the three body slides carry data.

## 2. Browse (one `search_references` call per slide, all in one turn)

Each query is the relationship only: no Fjordvik, no "facilities", no "energy", no counts and no layout words. Slide 2 is numeric, so it also passes `with_chart: true`; every call passes `min_quality: 4`.

| # | Query | What came back (names) |
| - | --- | --- |
| 2 | `a market value broken into drivers that multiply out over time` | Two models compared on productivity drivers; **Gap decomposed into two multiplying drivers (254-7)**; Metric decomposition with paired bar charts; Total and two segments over time; Two related trends with CAGR summary tables |
| 3 | `options scored against the capabilities they need` | **Capability matrix scored against strategic options (157-2)**; Capabilities scored across build, partner, acquire; … |

## 3. Pick

- **Slide 2 → 254-7.** It shows exactly the claim: a total for two periods, broken into two drivers that multiply, with a formula caption for the multiples. Capacity is two categories per chart, which is what we have (2019, 2025F). "Total and two segments over time" was the runner-up, but segments add up; ours multiply.
- **Slide 3 → 157-2.** Eight capability rows in three groups against four options with harvey balls, and a shaded block over the options not pursued. Our content has exactly that shape, so nothing is padded. It is team judgment, so it carries the TEAM ASSESSMENT sticker.

## 4. Write to the slots

`get_reference_slots` for both, in one turn. Each returns a skeleton, character budgets and a "How to fill this slide" note, which is followed to the letter: for 254-7, all three charts take the same two categories in the same order, driver 1 × driver 2 must equal the total, and the multiples live in the formula caption. The illustrative figures multiply out: 4.4k × €180k = €792m (2019) and 8.3k × €235k = €1,951m (2025F); 8.3 / 4.4 = 1.9x and 235 / 180 = 1.3x, and 1,951 / 792 = 2.5x. No `number_format` is sent: the labels follow the data (1,951 and 4.4).

```json
{
 "reference_id": "254-7",
 "props": {
  "title": "The Nordic retrofit market grows 2.5x by 2025 as both retrofits and project values rise",
  "legend_1": "2019",
  "legend_2": "2025F",
  "total_title": "Nordic retrofit market\n2019 vs 2025F, EUR m",
  "total_chart": {
   "categories": [
    "2019",
    "2025F"
   ],
   "series": [
    {
     "name": "Market",
     "values": [
      792,
      1951
     ]
    }
   ],
   "show_values": true
  },
  "driver1_title": "Retrofits per year\n2019 vs 2025F, '000",
  "driver1_chart": {
   "categories": [
    "2019",
    "2025F"
   ],
   "series": [
    {
     "name": "Retrofits",
     "values": [
      4.4,
      8.3
     ]
    }
   ],
   "show_values": true
  },
  "driver2_title": "Average project value\n2019 vs 2025F, EUR k",
  "driver2_chart": {
   "categories": [
    "2019",
    "2025F"
   ],
   "series": [
    {
     "name": "Value",
     "values": [
      180,
      235
     ]
    }
   ],
   "show_values": true
  },
  "formula": "1.9x more retrofits × 1.3x higher value = 2.5x the market",
  "sticker": "Illustrative",
  "source": "Source: Illustrative; all figures fictional; multiples calculated"
 }
}
```

For 157-2 the note says each body row is six cells with the four option cells left empty, ratings run row by row (4 = strong, 2 = partial, 0 = empty ring), and the note under the shaded block says what it means. The title's count ("five of eight, against four") was checked against the ratings before rendering.

```json
{
 "reference_id": "157-2",
 "props": {
  "title": "Retrofits fit our capabilities best: strong on five of eight, against four for the next option",
  "sticker": "Team assessment",
  "rows_header": "Capability",
  "options_header": "Growth option",
  "legend_high": "Strong fit",
  "legend_potential": "Partial fit",
  "legend_marks": [
   4,
   2
  ],
  "matrix": {
   "header": [
    "Area",
    "Capability",
    "Retrofits",
    "Integrated FM",
    "Security",
    "Waste"
   ],
   "rows": [
    [
     "Customers",
     "Building-owner access",
     "",
     "",
     "",
     ""
    ],
    [
     "",
     "Multi-site contracts",
     "",
     "",
     "",
     ""
    ],
    [
     "Delivery",
     "Technician network",
     "",
     "",
     "",
     ""
    ],
    [
     "",
     "Energy know-how",
     "",
     "",
     "",
     ""
    ],
    [
     "",
     "Project management",
     "",
     "",
     "",
     ""
    ],
    [
     "",
     "Procurement scale",
     "",
     "",
     "",
     ""
    ],
    [
     "Finance",
     "Balance sheet",
     "",
     "",
     "",
     ""
    ],
    [
     "",
     "Recurring billing",
     "",
     "",
     "",
     ""
    ]
   ]
  },
  "ratings": [
   4,
   4,
   2,
   0,
   4,
   4,
   2,
   2,
   4,
   2,
   2,
   0,
   4,
   0,
   0,
   0,
   4,
   2,
   0,
   2,
   2,
   4,
   0,
   2,
   2,
   2,
   2,
   0,
   0,
   4,
   4,
   2
  ],
  "note": "Not pursued in this plan period"
 }
}
```

## 5. Render, review, insert

One call: `render_deck` with the cover and the four slides in order. Both reference slides passed the automatic checks; the images were checked anyway (the sticker sits under the title rule, the multiples read correctly). Then the file is inserted once, with no reordering and no shape edits.

## 6. Reply

> Illustrative case: Fjordvik, a Nordic facilities-services group weighing a move into energy retrofits; all figures are fictional.
> 1. Retrofits are the growth move that uses our base (reference, browsed)
> 2. Market grows 2.5x on volume and project value (reference 254-7, three native charts)
> 3. Retrofits fit five of eight capabilities (reference 157-2, team assessment)
> 4. Board decisions needed today (reference, browsed)
> No slide fell back to `find_layout`.

## The failures this example replaces

An earlier version of this file used a fixed storyline, and the add-in agent reproduced it almost word for word, so every strategy deck came out as the same five layouts. The version after it planned each slide's layout on paper and then routed it, which found the nearest match to that plan and rarely more: generic tables and three-column pages. Build the storyline from the case, then let the library propose each slide's composition.
