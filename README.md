# Design Handoff Skill for Claude and other AI tools

An AI skill for product designers, UX designers, and UI designers. It helps you hand a design to engineering so that it gets built as intended.

Use it to check whether a design is ready for development, to write the developer handoff, and to run design QA on the finished build.

It works in Claude, in Claude Code, and in other AI tools that read `SKILL.md` agent skills. It works with Figma links, screenshots, or a plain description.

## Who it is for

- Product designers in product teams who hand work to engineers every week.
- Design leads who want one shared handoff standard for their team.
- Designers who work with an agency or a contractor.
- Designers who build with AI tools and want a clear spec before they start.

## What it does

Inspection tools already show developers the measurements and colors. This skill covers what those tools cannot show: how the design behaves, what must not change, and why.

It has five modes.

| Mode | Use it when | What you get |
|------|-------------|--------------|
| `check` | You want to know if the design is ready. | A short readiness report and a list of questions. |
| `quick` | You made a small change inside your own team. | A one-page handoff. |
| `full` | You designed a new feature or flow. | The whole handoff package. |
| `external` | An agency or contractor builds it. | The whole package, plus a written working agreement. |
| `qa` | The build exists and you want to review it. | A design QA report with a ship verdict. |

The skill never invents a value, a behavior, or a line of copy. Anything it does not know becomes a numbered question, marked as blocking or not blocking. Anything it adds from its own knowledge is labelled `SUGGESTED`, so you can confirm it or remove it.

It works for web, iOS, Android, and features with AI-generated output. It works from a design file link, from screenshots, or from a plain description.

## Install

### Claude app (web or desktop)

1. Download this repository. On GitHub, choose **Code**, then **Download ZIP**. Unzip it.
2. Open the `skills` folder. Compress the `design-handoff` folder into a ZIP file. The folder itself must be the top level of the ZIP.
3. In Claude, open your skills settings and upload the ZIP. Anthropic's guide shows the current steps: [Use skills in Claude](https://support.claude.com/en/articles/12512180).

### Claude Code

For all your projects:

```bash
git clone https://github.com/rastian/design-handoff-skills
mkdir -p ~/.claude/skills
cp -r design-handoff-skills/skills/design-handoff ~/.claude/skills/
```

For one project only, copy the folder into `.claude/skills/` inside that project.

### Other AI tools

If your tool supports skills, put the `design-handoff` folder where the tool reads skills.

If it does not, open `skills/design-handoff/SKILL.md`, paste its content into the chat or into the tool's custom instructions, and then write your request.

## Use it

Start with a check. It is the fastest way to see what is missing.

```
/design-handoff check
Is this design ready to hand off? Tell me what is missing.
[Describe the screen, or paste the frame link.]
```

In tools without slash commands, write "Use the design-handoff skill" at the start.

The [prompt guide](skills/design-handoff/PROMPTS.md) has a ready prompt for each mode, for native mobile screens, for AI features, and for follow-ups.

## Get better results

Give the skill as many of these as you can. Each one removes open questions.

1. The exact frame link, screenshots, or a clear description.
2. The platform and the stack.
3. The one thing that must work.
4. What is non-negotiable, and what is only a preference.
5. What you tried and rejected.
6. The data limits you know.
7. Who answers questions, and who decides when the build cannot match the design.

## How it was tested

The skill was run on seven written scenarios: a small change, a new feature, an agency build, a build review, a native iOS screen, a readiness check, and an AI feature. Each run used a fresh AI agent that had only the skill and the designer's message.

It has not yet been tested on a live design file through a design tool connector. If you try that, please open an issue and share what happened.

## License

MIT. See [LICENSE](LICENSE).
