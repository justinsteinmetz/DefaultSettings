# Default Settings

**An identity instrument for Grades 11–12.**  
Examining what was installed in you — and what you run on others.

> You did not write the original code. But you execute parts of it every day.

---

## Concept

Default Settings examines two movements simultaneously:

**Input** — inherited norms from family, culture, media, and institutions. The expectations, permissions, and constraints absorbed before awareness.

**Output** — the categories students apply automatically to others. Who they trust more readily. What registers as threatening, authoritative, or legitimate. The gap between stated beliefs and instinctive judgements.

The central insight is structural: inherited norms do not stay internal. They become enacted judgements — ordinary acts of perception, expectation, and categorisation directed at other people. Students are not only shaped by social scripts. They also help keep them running.

This is not a lesson about gender or intersectionality. It is a machine for exposing how invisible social structures become ordinary acts of perception and judgement.

---

## Architecture

### Four phases

| Phase | Axis | What it examines |
|---|---|---|
| Installation | Input | Gender expectations, class, inherited beliefs, internalised permissions and constraints |
| Execution | Output | Snap judgements about dress, accent, threat, authority |
| The loop | Both | Where input becomes output — how inherited norms become enacted categories |
| Confrontation | Both | The gap between stated values and instinctive behaviour |

### SNAP questions

Four questions are timed — students write their first instinct before they can revise it. These are the instrument's most reliable data. The snap overlay captures the answer; when it closes, students are asked: *"What surprised you about what you wrote?"* (not "what does this reveal?" — that reframe shifts them from defendant to analyst of their own data).

SNAP mode is configurable on the intro screen: Hard (auto-locks at time limit), Soft (visible timer, student submits when ready), or Off.

### The diagnostic contract

Before entering, students see three statements:

- *This instrument has no correct answers.*
- *What you write is data, not confession.*
- *The portrait it generates is a reading, not a verdict.*

This framing is not decorative. Without it, the instrument risks feeling accusatory. With it, students are positioned as investigators of their own data rather than defendants.

---

## The result

After all questions, the instrument generates:

**A portrait** — 200–280 words, specific to their answers. Names inherited norms, projected categories, and the gap between stated and instinctive. Does not resolve. Does not end hopefully.

**A headline** — 3–6 words. Names the central structural gap or pattern.

**A signature line** — one sentence naming the specific "parts of it that continue through you" as applied to this student, not the generic project line.

**Three discussion questions** — generated from this student's specific record. Not generic reflection prompts. Each points to a concrete contradiction, evasion, or gap in what they wrote. Labelled *"for teacher use"* and visible only after the portrait arrives.

### On performance

The AI prompt is explicitly instructed to flag performed answers. If a student's responses read as managed or constructed to avoid self-incrimination, the portrait names the performance directly rather than treating polished self-awareness as evidence of real honesty. Deflection is data. Performance is data.

---

## Design

The visual language argues conceptually. The intro screen splits pink and blue — familiar gender coding — in both the background gradient and the title treatment. As the instrument progresses through the Loop and Confrontation phases, the palette dissolves into violet. Categories which appear natural become unstable under examination.

**Palette** — dusty rose (Input), desaturated cyan (Output), violet (Loop/Confrontation). Phase-aware: CSS variables update as the student moves through phases.

**Typography** — IBM Plex Sans and IBM Plex Mono. The aesthetic of a diagnostic system.

**Progress bar** — dual: rose fills from the left (input questions), cyan fills from the right (output questions). Visually represents the two-axis structure.

**Session ID** — generated on load (`DS-XXX-XXX`), carried through to the result header. The record feels like a file.

---

## Pedagogical warnings

**This instrument cannot be deployed casually.** It requires careful framing around privacy, trust, and ownership of results. Without that framing, the experience risks feeling accusatory rather than investigative.

**Performance is the primary risk, not controversy.** Many students will understand exactly what socially acceptable answers look like. The snap questions are the best defence. The portrait prompt's performance-flagging instruction is the second line of defence. Neither eliminates the problem.

**Emotional readiness varies.** Some portraits will be genuinely revelatory. Others will be built from evasions and carefully curated responses. The instrument acknowledges this but cannot eliminate it. Teacher facilitation determines whether the experience is educational or merely uncomfortable.

**The result is private by default.** Students choose what, if anything, leaves the room.

---

## Classroom use

**Time:** 35–50 minutes for the questionnaire. Discussion duration is the teacher's choice.

**Prerequisites:** the class needs enough established trust that students believe the result is genuinely private and that the teacher will not read results aloud without consent. The diagnostic contract helps but does not replace this.

**Discussion entry points** (generic — the instrument also generates three specific ones per student):
- "What was the hardest question to answer honestly — and why that one?"
- "The instrument separates 'what was installed' from 'what you run'. Do you experience those as separate?"
- "What would it mean for a snap judgement to be innocent?"
- "Where do you recognise the loop — input becoming output — in your own behaviour?"

---

## Abitur Themenfeld relevance

| Themenfeld | Angle |
|---|---|
| The Individual & Society | Identity formation, inherited norms, social construction, gender, conformity, the gap between belief and behaviour |
| Politics, Culture & Society — UK/USA | Race, class, accent, institutional authority; postcolonial dimensions of who is perceived as trustworthy or threatening |
| Science & Technology | Algorithmic bias as structural default; machine learning as a model for how humans classify and categorise |

---

## Planned facilitation extensions

These are not yet built but are worth developing:

**A staged deployment option** — Installation and Execution in session one; Loop and Confrontation in session two, after discussion has opened the conceptual territory. Changes the emotional stakes considerably.

**A pre-instrument primer** — a short text establishing what social scripts are and what it means for norms to be "installed", before students touch the diagnostic. Makes the experience investigative rather than accusatory from the first question.

**A teacher aggregate mode** — surfaces patterns across a class session without exposing individual records. Useful for understanding where the class is before discussion opens.

---

## Technical architecture

Uses a Cloudflare Worker as a server-side proxy to the Anthropic API. The API key is stored as a Cloudflare environment secret and never exposed in the browser.

The Worker URL is hardcoded in `index.html` as the `PROXY` constant:

```javascript
const PROXY = "https://anthropic-proxy.justin-steinmetz.workers.dev";
```

See the *Who Are You, Really* README for full Worker deployment instructions. The same Worker handles all instruments in this suite.

### Deployment

Single HTML file. No dependencies, no build step. Rename `default-settings.html` to `index.html` and push to a GitHub Pages repository.
