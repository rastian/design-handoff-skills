---
name: design-handoff
description: Prepare a design for engineering, check whether it is ready, or review the finished build. Use when a product designer says a design is ready for development, asks for a handoff, a dev spec, a handoff checklist, "is this ready to hand off", acceptance criteria for a design, a handoff for an agency or contractor, or a design QA review of a build. Works for web, iOS, Android, and AI features. Works from a design file link, screenshots, or a plain description.
---

# Design Handoff

Help a product designer hand a design to engineering so that it gets built as intended.

Inspection tools already show developers the measurements, colors, and assets. Do not retype them. Write down what those tools cannot show: how the design behaves, what must not change, and why.

## Labels

Use these six labels. They are the core of this skill.

| Label | Meaning | Who may assign it |
|-------|---------|-------------------|
| `MUST` | Non-negotiable. The must-work outcome is always a MUST. | Only the designer. |
| `PREFER` | Wanted, but the developer has freedom. | Only the designer. |
| `STATED` | The designer said it or drew it, but did not rank it. | You. |
| `DEFAULT` | A standard component behaves as it does in the team's library. Nothing custom. | You. |
| `SUGGESTED` | Comes from your own knowledge (platform convention, accessibility standard, a known library limit). The designer confirms it. | You. |
| `OPEN` | Unknown. Needs an answer. | You. |

Rules for the labels:

1. **Never invent a value, a behavior, or a line of copy.** Everything comes from the design or from the designer's words. If it comes from you, it is `SUGGESTED`. If nobody knows, it is `OPEN`.
2. When there is no design file, the designer's description is the design.
3. Write each unknown once, as a question in the question list. Elsewhere, refer to it by number, as `OPEN Q3`. One question asks one thing. The exception is a whole section that is unknown (for example the build context): ask one question that names the section.
4. A question **blocks the build** when the developer cannot start without the answer, or would have to rebuild once it arrives. The must-work question always blocks. A question that engineering can answer alone does not block.

## Step 1: Pick the mode and the platform

Use the mode the designer names. If they name none, choose from the request and say which you chose.

| Mode | Use when | What you deliver | Length |
|------|----------|------------------|--------|
| `check` | "Is this ready?" The designer does not want a spec yet. | The readiness report from step 3. Stop there. | Under 50 lines |
| `quick` | A small change inside one team. | The header, sections 1, 3, 5, and 9. Three accessibility lines (keyboard, names, announcements). One acceptance criterion for the must-work outcome. | Under 70 lines |
| `full` | A new feature or flow. | The whole package. | As short as the content allows |
| `external` | An agency, a contractor, or another team builds it. | The whole package, plus the external additions in section 11. | Same |
| `qa` | The build exists. | Go straight to "QA mode" at the end of this file. Skip steps 2 to 5. | Under 80 lines |

Then note the platform: web, iOS, Android, or several. Adapt the vocabulary:

| Topic | Web | Native iOS or Android |
|-------|-----|-----------------------|
| States | Hover, focus, active | Pressed, focused (keyboard or switch control). Hover only if pointer devices are supported. |
| Layout | The team's breakpoints | Device sizes, orientation, safe areas, text scaling |
| Input | Mouse, keyboard, touch | Gestures and haptics. Every gesture needs a visible alternative. |
| Target size | 24 by 24 CSS pixels minimum | 44 points on iOS, 48 dp on Android |
| Assistive tech | Screen reader, keyboard | VoiceOver or TalkBack, text scaling, reduced motion |

## Step 2: Gather inputs

1. Read the design. If a design tool connector is available, read the frames, components, variables, and comments from the link. Otherwise use the screenshots or the description.
2. Note the team's stack, design system, and languages, if stated or reachable.
3. Ask only for what is still missing, in one message, at most five questions:
   - What is the one thing here that must work?
   - What is non-negotiable, and what is only a preference?
   - What did you try and reject, and why?
   - What are the data limits (required fields, maximum lengths, list sizes, plan limits)?
   - Who answers questions during the build, and who decides when the build cannot match the design?

If the designer cannot answer, or tells you to continue, record the gaps as `OPEN` and go to step 3.

If the must-work outcome cannot be observed or tested (for example "feels trustworthy"), ask what a tester would see when it works.

## Step 3: Check readiness

Mark each item **Yes**, **No**, or **Not verified**.

- **No:** the designer said it is not done, or it is absent from a design where it should be visible.
- **Not verified:** the input cannot show it (for example layer names or contrast, when you only have a description). This is not a failure.
- When an item is partly done, mark it "No" and name the missing part.

Items:

- **Intent:** The must-work outcome is known. MUST rules are known.
- **Flow:** Every step of the main flow is designed. The main flow is the path the user takes to reach the must-work outcome.
- **States:** Custom elements have every state that applies. Loading, error, and success exist where the server is involved.
- **Content:** Copy is real and final. Lists are shown with zero, one, and many items. Long text is shown.
- **Layout:** Behavior between the drawn sizes is defined.
- **Accessibility:** Focus order and focus style are defined. Contrast is checked. Icon-only controls have names.
- **Feasibility:** An engineer has seen the design. Data fields and limits are agreed.
- **File:** The version to build is marked. Old explorations are archived. Token names match code.
- **Process:** A contact and a decision-maker for deviations are named.

Give one status:

- **Not ready:** the must-work outcome is unknown, or a step of the main flow is not designed.
- **Ready with gaps:** anything else that has a "No". This includes a must-work outcome that is stated but cannot be tested yet. Ask for the testable form as a blocking question.
- **Ready:** no "No".

Report in this form. In `full` and `external` mode, put only the Status and Missing lines above the package. The questions go in section 9.

```markdown
**Status:** [Ready | Ready with gaps | Not ready]
**Missing:** [each "No" item, one line, with what exactly is missing]
**Not verified:** [one line]
**Questions:** [numbered, blocking ones first, each with who answers it]
**Next:** [the one action that moves this forward]
```

**If the status is "Not ready", stop here**, in every mode. Offer to write the package when the blocking questions are answered. Write it anyway only if the designer explicitly asks for a package despite the status.

## Step 4: Write the package

Rules for the whole package:

- Leave out a section that has nothing to say. Replace it with one line: "Motion: none." Leave out single lines that would only say "none stated".
- A section that is unknown as a whole becomes one line: "Build context: OPEN Q12."
- Standard components get one line with `DEFAULT`. Describe only what is new or changed.
- Do not restate a question in several sections. An edge case or a state with unknown behavior lives in section 9 only.
- Use the team's own names for tokens, components, and breakpoints.
- Write for a developer who was in no meeting. Plain language.

```markdown
# Handoff: [Feature or screen name]

Design: [link to the exact frame, or "description only"]   Version: [date, v1]   Platform: [web, iOS, Android]
Status: [Ready | Ready with gaps]   Target date: [if known]
Designer and contact: [name, channel]   Deviations decided by: [name]

## 1. Start here
- **What this is for:** [user, situation, one or two sentences]
- **The one thing that must work:** [single outcome a tester can observe]
- **MUST:** [list]
- **PREFER:** [list]
- **Stated, not ranked:** [STATED rules. Ask the designer to mark each as MUST or PREFER.]
- **Blocking questions:** [numbers and short form. If there are more than seven, show the seven most important and say how many more are in section 9.]
- **Rejected directions:** [two lines at most, with the reason]
- **Known compromises:** [what is not ideal, and why it was accepted]

## 2. Scope and flow
| Item | In | Deferred | Out | Owner or reason |
|------|----|----------|-----|-----------------|

Anything not listed is not expected in the build.

Flow: [numbered steps, entry and exit points, each linked to its frame]

## 3. Components and states
Existing and unchanged: [Component: DEFAULT], [Component: DEFAULT]

| Element (new or changed) | State | What the user sees | Label |
|--------------------------|-------|--------------------|-------|

One row per state that applies and is known. Do not list states that do not apply.

## 4. Content and data
**Field rules**
| Field | Required | Min | Max | Format | When empty | When too long |
|-------|----------|-----|-----|--------|------------|---------------|

**Data needs** (the designer's view, engineering confirms)
| Screen or action | Reads | Writes | Can fail how |
|------------------|-------|--------|--------------|

**Copy**
Source of truth: [design file or copy document link]
With a design file, list only what is not visible in it: errors, confirmations, empty states, screen reader text, variables, and plural forms. Without a design file, list all copy the designer gave. Add a column per language if there are several. Missing copy is `OPEN`. Never write placeholder copy. A name for assistive tech that you propose is allowed when it is labelled `SUGGESTED`.
| ID | Situation (when it appears) | Message |
|----|-----------------------------|---------|

## 5. Edge cases
Write one line per case whose behavior is known, in this form:
- **E1** Given [situation], when [action], then [what the user sees and can do]. [Label]

Go through this list. Cases that apply but have no known behavior become questions in section 9.
- Empty: nothing created yet. Empty: search or filter matched nothing.
- Loading: first load. Loading: refresh or background update.
- Error: network, server, validation, permission.
- Several items at once: partial success, duplicates, pasted input.
- Limits: plan or quota reached, and the upgrade path.
- Destructive actions: confirmation and undo.
- Roles: what each role sees (hidden, disabled, or explained).
- Offline, stale data, sync conflicts, two people editing.
- Slow response: what happens after a stated number of seconds.
- Long content: truncate, wrap, or scroll.
- Time and locale: time zones, day boundaries, currency, plural forms, text direction.
- Update model: show the change at once or wait for the server, and what happens on failure.
- Interplay with search, sort, pagination, and the URL.

## 6. Layout and motion
| Size or condition (team names) | What changes |
|--------------------------------|--------------|

- Between sizes: [what stretches, what stays fixed, what wraps]
- When space runs out: [what goes first, second, third]

| Element | Trigger | What animates | Duration | Easing | With reduced motion |
|---------|---------|---------------|----------|--------|---------------------|

## 7. Accessibility
Standard: [the team's standard. If none is stated, WCAG 2.2 AA as SUGGESTED.]
Write only what is specific to this design.
- **Focus order:** [numbered]
- **Focus style:** [visible on every interactive element, never hidden behind sticky elements]
- **Keyboard or gesture alternatives:** [per element]
- **Names and roles:** [name for each icon-only control, role for each custom element]
- **Announcements:** [what assistive tech says on each state change, errors in text]
- **Contrast at risk:** [pairs that were checked, or that look risky]
- **Not by color alone:** [status, errors, and selection have a second signal]
- **Zoom and text size:** [what happens at 200% text and 320px width, or with platform text scaling]

## 8. Build context
Answer each row, write "n/a", or write `OPEN Qn`.
| Topic | Answer |
|-------|--------|
| Analytics events | |
| Feature flag and rollout | |
| Browsers, devices, OS versions | |
| Languages and text direction | |
| Themes (light, dark, high contrast) | |
| State in the URL or deep links | |
| Performance expectation | |

## 9. Questions
Blocking questions first. Inside each group, sort by who answers: designer, engineering, product.
| # | Question | For | Blocks the build? | Answer |
|---|----------|-----|-------------------|--------|

## 10. Acceptance criteria
- **A1** Given [state], when [action], then [result].

Write one for the must-work outcome and one for each MUST rule. If part of a rule is still open, write the criterion for the known part and add "(see Q3)". Refer to edge cases by ID and do not repeat them.

## 11. Working agreement
- **Walkthrough:** [date, or link to a short recording]
- **Questions during the build:** [channel, expected response time, where answers are recorded]
- **When the build cannot match the design:** [who is told, how fast, who decides. The design file is updated after.]
- **Design QA before release:** [who, when, against section 1]

External builds only. Add:
- **Access:** [repository, design file, staging, test accounts, API credentials]
- **What the team normally leaves unsaid:** [where tokens and components live, naming, code conventions, supported browsers and devices]
- **Milestones:** [dates for first review, final review, and release]
- **Definition of done:** [what must be true before the work is accepted, and who checks accessibility]
- **Review rounds:** [how many, who reviews, how feedback is given]
- **Deviation agreement, in writing:** [same as above, with response times and sign-off]

Change log: [date, what changed]
```

Reference for contrast (WCAG 2.2 AA): text 4.5:1. Large text (24px, or 18.66px bold) 3:1. Interface elements, focus indicators, and meaningful graphics 3:1. Placeholder text counts as text. Disabled controls are exempt.

## If the feature uses generated AI output

Go through this list for sections 3, 5, and 8. Write what the designer has decided. Everything else becomes questions in section 9.

- **States:** waiting before the first output, streaming, complete, stopped by the user, failed, refused or no answer, empty or poor output, output that is out of date because the source changed.
- **Controls:** stop, regenerate (replace or keep the earlier version), edit, copy, feedback.
- **Disclosure:** the exact wording that tells the user the content is generated, and where it sits.
- **Trust:** whether the output links to its sources, and what language it is written in.
- **Latency:** what the user sees at each stage of a long wait, and when the wait is treated as a failure.
- **Limits:** input length, rate limits, and what the user sees when one is reached.
- **Data:** what content is sent to the model, whether the output is saved, and what the feedback buttons record. These are questions for engineering and product.
- **Acceptance criteria** test the behavior around the output, never the generated text itself.

## Step 5: Check your work

- Nothing is invented. Everything from you is `SUGGESTED`. Every unknown is in section 9, once.
- No measurement is copied from the inspection tool unless it is a rule.
- Section 1 fits on one screen.
- The output is inside the length target for the mode.

Then, in your reply and not in the document, tell the designer three things: the status, the number of blocking questions, and the next action.

## If connectors are available

- **Design tool:** Read frames, components, variables, and comments directly.
- **Code or component library:** Check whether each component and token exists. Replace `OPEN` with the result.
- **Project tracker, chat, docs:** Offer to link the package, create tickets per buildable slice or per blocking question, or draft the handoff message. Ask before you create, change, or send anything.

## QA mode

Use this when the build exists. Compare the build with the intent, not with pixel values.

1. Get the must-work outcome and the MUST rules, from the handoff package or from the designer.
2. Review the build yourself if you can reach it. Otherwise use the designer's observations, and do not add observations of your own.
3. Sort each finding:
   - **Blocker:** the must-work outcome fails, or a user cannot complete the task (this includes accessibility barriers), or the problem can lose data, repeat an action, or cause a wrong charge.
   - **Major:** a MUST rule is broken, a needed state or edge case is missing, or there is an accessibility failure that does not stop the task.
   - **Minor:** a PREFER rule or a visual detail, such as spacing.
   - Add **(unconfirmed)** when the finding is not measured or is second-hand. Say what would confirm it. A possible accessibility failure stays Major (unconfirmed).
4. Give a verdict: **Do not ship** with any Blocker. **Ship after fixes** with any Major. **Ship** with only Minor findings.

```markdown
# Design QA: [Feature], [build], [date]

**Verdict:** [Ship | Ship after fixes | Do not ship]
**Intent:** [the must-work outcome, and "met", "not met", or "not measured"]
**Tested on:** [browsers, devices]   **Not checked:** [what the review did not cover]

| # | Where (screen, browser or device) | Expected | Actual | Severity | Rule |
|---|-----------------------------------|----------|--------|----------|------|

**Passed:** [MUST rules that hold]
**Agreed deviations:** [what, who agreed, where it is written. If it is only hearsay, say "confirm in writing".]
**Design file needs updating:** [list]
**Next:** [who fixes what, and when the re-test happens. Write OPEN if unknown.]
```

Offer to turn each Blocker and Major finding into a ticket. Ask first.
