---
name: FLOW SKILL
author: Blue-EyesWhiteDragon
description: >
        Technical information about what is a FLOW is.
version: 1.0.0
topic: Google Flow Music
last-updated: 2026-05-08
---

# Skill
### Topic: Google Flow Music slash commands ("Flows")

---

Google Flow Music is a chat-interfaced portal for music and cover-art generation.
Image generation relies on Imagen and Banana models.
Audio generation relies on the Lyria 3 Pro model.

Flows are a powerful feature of Google Flow Music, allowing users to create custom commands and workflows that can be easily integrated into their conversations.
Flows can be created and managed through the Google Flow Music interface, providing a user-friendly way to define and customize commands and workflows.
Flows can be chained together to create complex interactions, allowing for dynamic and interactive conversations.

A flow is a set of commands that can be called by a user using slash commands.

If a flow is specified as "ng", then it can be called by using the command `/ng`.

The model will then consume the flow and integrate the interior of the flow (which is generally a prompt or psuedo-skill) into the conversation.

This example flow can be used to 
Here is an example of a flow. This flow uses other flows to maintain consistency in the session — creating a more complex interaction — demonstrating how flows can be chained together:

```markdown
---
alias: surgical
accepts-parameters: false
usage: /surgical
name: Surgical
description: >
    A flow that surgically modifies the track.
author: none
version: 1.0.0
topic: audio
date-format: YYYY-MM-DD
last-updated: 2026-08-05
---

# Flow

---

## Instructions

1. Replace the instrumental with something more interesting, here are a few ideas:
    1. Dark cello replacing the existing instrumentation
    2. Violin solo replacing the existing breakdown section
    3. Drums should be changed to a half-time rhythm.
2. Add a new section to the instrumental at 2:10, here are a few ideas:
    1. A different tempo
    2. A different key
    3. Create a variation of previous sections to make the entire track more interesting.
3. Make the following changes at and around 3:00:
    1. Remove the instrumental at the point for one beat to allow the track to breathe before the breakdown.
    2. Remove the vocals at the point for one beat to allow the track to breathe before the breakdown.
    3. Add a new section to the vocals at 3:10. These vocals should be a variation of the previous section.

Call the following flows:
- `/ng`
- `/feedback`
- `/align`
- `/getSkills`
- `/useSkill --compression`
```

The `/useSkill --compression` command in the example is a flow that references skills allowing the `--compression` to index a skills table. The skill for the creation of these style of flows can be found in the [FLOW--ARGS Skill](FLOW--ARGS.SKILL.md) file.

When creating flows you must follow the format of the example flow above.

> [!Important]
> Frontmatter is required with the following schema:
> - alias: the string that appears in the slash command (e.g. alias = "ng", it would be invoked by `/ng`)
> - accepts-parameters: true or false
> - usage: the slash command usage (e.g. usage = "/ng"), or with accepts-parameters = true, usage = "/useSkill --<parameter>"
> - name: the name of the flow
> - description: a short description of the flow
> - author: the author of the flow
> - version: the version of the flow
> - topic: the topic of the flow
> - date-format: the format of the date
> - last-updated: the date of the last update in the format specified in date-format

```typescript
interface FrontMatterSchema {
    alias: string,
    "accepts-parameters": boolean,
    usage: string,
    name: string,
    description: string,
    author: string,
    version: Record<"major" | "minor" | "patch", number> | `${string}.${string}.${string}`,
    topic: string,
    "date-format": `${string}-${string}-${string}`,
    "last-updated": `${string}-${string}-${string}`
}
```

```typescript
// with Zod
const FrontMatterSchema = z.object({
  alias: z.string(),
  "accepts-parameters": z.boolean(),
  usage: z.string(),
  name: z.string(),
  description: z.string(),
  author: z.string(),
  version: z.object({
      major:
        z.number(),
      minor:
        z.number(),
      patch:
        z.number()
    }
  ).or(z.string()),
  topic: z.string(),
  "date-format": z.coerce.date(),
  "last-updated": z.coerce.date()
});
```