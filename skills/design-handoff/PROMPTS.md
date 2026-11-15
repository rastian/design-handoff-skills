# Design Handoff: prompt guide

Copy a prompt, replace the parts in [brackets], and send it together with the skill.
In Codex, write `$design-handoff` in place of `/design-handoff`. In ChatGPT and other tools without slash commands, start with "Use the design-handoff skill".

## What to give it

The more of these you give, the fewer open questions you get back.

1. The exact frame link, or screenshots, or a clear description.
2. Platform and stack ("web, React, Tailwind, shadcn" or "iOS, SwiftUI").
3. The one thing that must work.
4. What is non-negotiable, and what is only a preference.
5. What you tried and rejected.
6. Data limits you know (maximum lengths, list sizes, plan limits, roles).
7. Who answers questions, and who decides when the build cannot match the design.

If you only have a description, expect a list of questions first. That is the skill working as intended.

## 1. Am I ready? (check)

Use this before you invest in a full handoff.

```
/design-handoff check
Is this design ready to hand off? I do not want the spec yet. Tell me what is missing.
[Describe the screen or paste the frame link.]
[Say what you have designed so far: which sizes, which states.]
[Say whether engineering has seen it.]
```

## 2. Small change (quick)

Use this for one component or one screen inside your own team.

```
/design-handoff quick
[What changed, in two or three sentences.]
Stack: [stack and design system].
Must work: [the one outcome].
[Anything non-negotiable.]
Goes to: [developer name], questions to me in [channel].
```

## 3. New feature (full)

```
/design-handoff full
Feature: [name], [platform].
Flow: [the steps the user takes, from entry to done].
Stack: [stack]. Tokens: [where they live or how they are named]. Breakpoints: [names and values].
Must work: [the one outcome].
Non-negotiable: [list].
Preference: [list].
Rejected: [what you tried, and why you dropped it].
Data: [limits, roles, plan rules, expiry].
Copy I have: [strings]. 
Questions go to [name] in [channel]. [Name] decides on deviations. [Engineer] has seen [what].
```

## 4. Agency or contractor (external)

```
/design-handoff external
[Who builds it, and whether you have worked with them before.]
[What the page or feature contains.]
[Where data comes from, and anything that must never be hard-coded.]
Our stack: [stack]. They do not know our [tokens, components, conventions].
Must work: [the one outcome].
Non-negotiable: [list, including the accessibility standard].
Contact: [name, email]. [Name] decides on deviations. Deadline: [date].
```

## 5. Review the build (qa)

```
/design-handoff qa
[Feature] is on [staging, build number]. I need to review it before [date].
Intent: [the one outcome].
MUST rules: [numbered list].
PREFER: [list].
What I see, tested on [browsers and devices]:
- [Observation]
- [Observation]
- [Anything that was agreed to be dropped, and who agreed.]
```

## 6. Native mobile screen

```
/design-handoff full
Native [iOS or Android] app ([SwiftUI, Compose, React Native]). Screen: [name].
[What the screen shows.]
[Gestures: tap, swipe, long-press, pull to refresh. Haptics.]
[Light and dark mode, text scaling, languages, offline behavior.]
Must work: [the one outcome].
Non-negotiable: [list].
Questions in [place]. [Name] decides on deviations.
```

## 7. AI feature

```
/design-handoff full
Feature: [name], [platform]. It shows AI-generated output.
[What the user does to start it, and where the output appears.]
[How the output arrives: all at once or streamed. Typical wait time.]
[Controls: stop, regenerate, copy, insert, feedback.]
Must work: [the one outcome, as something a tester can observe].
Non-negotiable: [for example the disclosure wording, or that the source stays visible].
Questions in [channel]. [Name] decides on deviations.
```

## Follow-up prompts

After the first result, these keep the work moving.

```
Here are my answers: Q1 [answer]. Q4 [answer]. Q7 is for engineering. Update the handoff.
```

```
Rank these for me as a list I can answer in one line each: which UNRANKED rules are MUST and which are PREFER?
```

```
Write a short message to [engineer] with only the blocking questions that are for engineering.
```

```
Turn the acceptance criteria and the blocking questions into tickets. Show me the list before you create anything.
```

```
The design changed: [what changed]. Update the handoff and add a line to the change log.
```
