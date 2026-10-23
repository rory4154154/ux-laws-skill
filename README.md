# UX Laws skill for Claude

A Claude skill that makes Claude follow five laws of UX whenever it builds an app, website, dashboard or any interface.

Left to its defaults, Claude invents layouts, adds a dozen buttons, uses tiny tap targets, waits on the server before showing anything, and pushes complexity onto the user. This skill turns five well-known UX laws into hard rules it builds against, plus a checklist it runs before handing anything back.

| Law | In one line |
|---|---|
| **Jakob's law** | People expect your app to work like the apps they already use. Put things where they expect them. |
| **Hick's law** | More choices means slower decisions. One primary action per screen, three or fewer in a group. |
| **Fitts's law** | Big targets close to the thumb get clicked. 44x44 px minimum, main action in reach. |
| **Doherty threshold** | Respond in under 400 ms or people feel the lag. Instant feedback, optimistic UI, skeletons. |
| **Tesler's law** | Some complexity can't be removed. The app absorbs it, not the user. Smart defaults, forgiving input. |

The full rules are in [SKILL.md](SKILL.md).

## Install

**Claude Code (all projects):**

```bash
git clone https://github.com/rory4154154/ux-laws-skill ~/.claude/skills/ux-laws
```

**Claude Code (one project):**

```bash
git clone https://github.com/rory4154154/ux-laws-skill .claude/skills/ux-laws
```

**Claude.ai / Claude desktop:** download this repo as a zip and upload it under Settings > Capabilities > Skills.

The skill activates automatically when you ask Claude to build or review a UI. You can also call it directly with `/ux-laws`.

## License

MIT
