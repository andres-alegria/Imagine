# Blueprint — The Stadium Debate

*A high-level, participatory and transparent political debate, measured live by the people in the room.*

Status: raw idea, written down 2026-08-08. Not started.

---

## 1. The idea in one paragraph

Two or more presidential candidates share a stage inside a large stadium. A moderator
works through a short list of key topics, all published well in advance. At the end of
each topic, every candidate must state a concrete plan — not a position, a plan. Then the
stadium answers. Each of the tens of thousands of attendees finds a set of cards under
their seat: two large cardboard panels, each printed a different colour on each side, four
colours in total. On the moderator's count, everyone raises one card, one colour facing the
stage. The stadium becomes a live, physical, human-scale readout: yes/no, or a choice among
four options. The result is visible instantly to the candidates, to the audience, and to the
cameras — no polling firm, no black box, no delay.

The core move: **the audience stops being scenery and becomes the instrument.**

---

## 2. Why it could matter

- **Immediate accountability.** A candidate hears the room's answer to their own proposal
  seconds after making it, in front of everyone. There is no spin window.
- **Transparency by construction.** The vote is physical and public. Anybody with a camera
  can recount it. There is no server to trust.
- **It measures policy, not personality.** Traditional debates produce a winner-loser
  narrative. This produces a per-question distribution.
- **It is legible.** A stadium of colour is an image anyone understands without a chart.
  (It is also, incidentally, one of the most striking data graphics imaginable.)

---

## 3. Format

### 3.1 Elements

| Element | Description |
|---|---|
| Venue | Large stadium; seats grouped into numbered sectors |
| Participants | 2+ candidates (works with 3–4; needs rethinking above ~5) |
| Moderator | Neutral; runs time, reads questions, calls the raise |
| Topics | 4–6, published weeks in advance with their exact framings |
| Question panel | Independent body that drafts the vote questions; not the campaigns |
| Audience | Voluntary attendance, seated by sector, each seat pre-stocked with cards |

### 3.2 Round structure (repeat per topic)

1. **Framing** — moderator states the topic and the agreed problem definition (30 s).
2. **Plans** — each candidate presents a concrete plan to implement (2–3 min each,
   hard-stopped). The requirement is mechanism: what, who pays, by when.
3. **Cross-question** — one short rebuttal round (optional, 1 min each).
4. **The question** — moderator reads the pre-registered question aloud and the four
   options are displayed on the big screens.
5. **The raise** — a countdown (*"three… two… one… raise"*) so all cards go up at once.
   Simultaneity is essential: it stops people copying their neighbours.
6. **The hold** — cards stay up ~10 seconds while overhead cameras capture the count.
7. **The readout** — the tally appears on screen, broken down by sector.
8. **The response** — each candidate gets 45 seconds to react to what the room just said.

Step 8 is where the format earns its keep. It forces candidates to engage with a fact about
the public that they did not choose and cannot deny.

---

## 4. The card system

Two double-sided cardboard panels per seat = **four colours**, so each raise can express:

- a **binary** (yes / no — using two of the four colours), or
- a **four-way choice** (four ranked or unranked options), or
- a **four-point agreement scale** (strongly agree → strongly disagree), or
- a **priority pick** (which of four sub-policies should come first).

### Card design notes

- **Colours must survive stadium conditions**: floodlights, distance, camera white balance,
  and colour-vision deficiency. Pick four hues that are separable in both hue *and*
  lightness, and verified under deuteranopia/protanopia simulation. Rough starting set:
  a warm yellow, a deep blue, a strong red-orange, a mid green — but this needs real
  testing under the actual lighting rig.
- **Redundant encoding**: print a bold shape or pattern (circle / cross / stripes / dots)
  on each colour face. This helps colourblind participants, helps the counting algorithm,
  and makes the photographs readable in greyscale.
- **Back-of-card labelling**: the option text printed large on the side facing the *holder*,
  so people know what they are raising without looking at the screen.
- **Size**: large enough to be resolved by a camera 100 m away, small enough to hold above
  the head for 10 seconds. A2-ish, lightweight card.
- **Neutral by design**: no candidate colours, no party colours. This is non-negotiable —
  if a card colour maps to a party's brand, the whole instrument is compromised.

---

## 5. Reading the stadium

The counting layer is where this becomes data rather than theatre.

- **Fixed overhead / high-angle cameras**, each assigned to a seating sector, calibrated
  before the event against a known pattern (e.g. a test raise during the warm-up).
- **Per-sector colour classification** — this is a well-bounded computer vision problem:
  fixed cameras, fixed geometry, four high-contrast targets, known seat count as a
  denominator. Abstentions (no card raised) are a real and meaningful category — count them.
- **Redundancy**: two independent camera sets and two independent counting teams, plus the
  raw footage released publicly so anyone can recount. Publishing the raw frames is what
  makes the "transparent" in the title true.
- **Sector-level output** is the key data structure: `topic × question × sector × colour`.
  From this you get the stadium heat map, the sector breakdowns, and — if attendees
  optionally register a district on entry — a geographic readout of the city or country
  projected onto the bowl of the stadium.

---

## 6. What kind of sample is this, honestly

This is the part that needs the most careful thinking, and the part most likely to be
attacked.

**It is not a representative sample.** Attendance is voluntary and mobilised, so the crowd
is self-selected on exactly the variables that matter: political engagement, candidate
loyalty, ability to travel, free time, age, income. A 60/40 split in the stadium says
nothing reliable about a 60/40 split in the country. Reporting it as if it did would hand
critics an easy and correct objection.

**But it does measure several things that are genuinely valuable:**

1. **Mobilisation.** Who can fill their share of the seats is itself a real, fair signal —
   as noted in the original sketch: if few people care enough to come, that is information.
2. **Cross-over agreement.** The most interesting number is not the total. It is:
   *how many of Candidate A's supporters raised the colour endorsing Candidate B's plan?*
   That is a measurement of where actual policy consensus exists beneath partisan
   identity — and almost nothing in public life currently measures it live.
3. **Within-bloc disagreement.** Where a candidate's own crowd splits on their own proposal.

### Two fixes worth designing in

- **A reserved probability panel.** Set aside one or two sectors (say 500–1,000 seats) for
  attendees recruited by *random* sampling from the electoral roll, invited and
  travel-compensated, seated together and counted separately. Their tally is a genuine
  probability sample and can be reported alongside the crowd tally. The contrast between
  the two — "the stadium said 70%, the random panel said 48%" — is itself a public lesson
  in what mobilisation does to perception. Closely related to James Fishkin's
  *Deliberative Polling*; worth reading properly before designing this.
- **Optional entry declaration.** Voluntary, anonymous, at the door: district, age band,
  candidate preference. Enables post-stratification weighting and the cross-over analysis
  above, without requiring anyone to identify themselves.

**Framing rule:** report the stadium as *"what this assembly said"*, never as *"what the
country thinks"*. The honesty is not a weakness of the format — it is the format's main
credibility asset.

---

## 7. Transparency commitments

These should be published as rules before the event, not decided afterwards:

- Topics and question wordings published in advance; questions drafted by an independent
  panel, with campaign veto limited to a documented, public objection process.
- Seat allocation method published (how sectors were divided among campaigns / open ballot
  / random panel).
- Raw camera footage and per-sector counts released as open data within 48 hours.
- Counting method and code published; independent recount invited.
- No editing of the live feed's wide shots during the hold — the whole point is the image.

---

## 8. Failure modes to design against

| Risk | Mitigation to explore |
|---|---|
| Herd effect (people copy neighbours) | Simultaneous countdown raise; short hold |
| Coordinated bloc sabotage (organised wrong-answer raises) | Sector-level reporting exposes anomalous blocs; random panel is unaffected |
| Cards used as projectiles / litter | Lightweight card, rounded corners, collection incentive, no hard edges |
| Camera miscount, glare, occlusion | Dual camera sets, calibration raise, published footage |
| Colour ambiguity under floodlights | Pre-event lighting test; redundant shape coding |
| Candidates gaming the questions | Independent question panel; questions sealed until read |
| Low participation in the raise | Count abstentions explicitly and report them; treat as data, not failure |
| Crowd asymmetry read as a poll result | Reserved random panel + explicit framing rules (§6) |
| Safety in a charged partisan crowd | Sector separation, standard stadium event protocols, no bloc adjacency |

---

## 9. Prior art to read before developing this

- **Deliberative Polling** — James Fishkin, Stanford CDD. Random sample + briefing +
  deliberation + pre/post measurement. The closest serious methodological ancestor.
- **Participatory budgeting** — Porto Alegre and successors; mass in-person prioritisation.
- **pol.is / vTaiwan** — digital cousin; finds cross-partisan consensus statements. Its
  central output (agreement across opinion clusters) is exactly the §6.2 metric, done online.
- **Dial testing / "the worm"** in televised debates — continuous audience response, but
  small panels and opaque methodology. This format is the transparent, physical inverse.
- **Icelandic and Chilean constitutional processes** — mass participatory drafting.
- Town halls, citizens' assemblies, and Irish Citizens' Assembly practice.

---

## 10. Pilot path

Do not start at national scale.

1. **Bench test** — 50 people, a school hall, four colours, one camera. Test colour
   separability and the counting pipeline. Cheap, one afternoon.
2. **Local pilot** — a mayoral or city council debate in a 1,000–2,000 seat venue. Full
   round structure, real questions, real counting, published data.
3. **Regional** — 10,000-seat arena, with the reserved random panel introduced.
4. **National stadium event** — only once the counting, framing, and safety protocols have
   survived the smaller runs.

---

## 11. Open questions

- What happens with more than 3 candidates — does the four-colour vocabulary still fit?
- Who convenes this? A broadcaster, an electoral authority, a university, an NGO coalition?
  The convener determines whether candidates show up at all.
- What is the incentive for a front-runner to participate, given the risk?
- Should the audience also be able to vote *before* the plans are presented, to measure
  movement rather than level? (Pre/post per topic is much more informative than post only —
  probably worth the extra 20 seconds per round.)
- Cost per seat for cards; recyclable material; what happens to 50,000 cards afterwards.
- Is there a version of this for a legislature, a shareholder meeting, a COP plenary?
- Names: *The Stadium Vote*, *Show of Colours*, *The Room Answers*, *Cuatro Colores*.

---

## 12. The visual products this generates

Worth listing separately, because they are half the reason to build it:

- The live stadium heat map — sectors coloured by majority answer, updated per round.
- The cross-over flow diagram — supporters of A endorsing B's plan, per topic.
- The pre/post movement chart — how many minds each plan actually changed.
- The consensus ranking — the policies the whole stadium agreed on, regardless of side.
- The single wide photograph of 50,000 raised cards, which is the thing people remember.
