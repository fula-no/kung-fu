# kung-fu

All of the skills available for Fulano to use: a library of agent
personas. Each one turns a general coding agent into a specialist for a
kind of office work, an accountant, a paralegal, a product manager, a UX
designer, with the way that specialist thinks, the questions they ask,
the standards they hold their work to and the shape of what they hand
back.

## Layout

```
skills/
  accountant/SKILL.md
  paralegal/SKILL.md
  product-manager/SKILL.md
  …
```

One folder per persona, holding a `SKILL.md`. The format is the one
Claude Code uses for skills, so the folder also works dropped into
`~/.claude/skills/` or wired up as a plugin:

```markdown
---
name: accountant
description: One paragraph. What this persona does and the requests it fits,
  in the words people use ("close the month", "reconcile", "is this
  deductible"). Fulano reads this to decide when to use the persona.
---

# Accountant

You are … (the persona's instructions, in the second person)
```

The body is the prompt. Every persona follows the same bones so they
read alike and can be compared:

- **Who you are.** The role, its seniority, what it is good at and what
  it is not for.
- **How you work.** The process the specialist actually follows, in
  order, including what to look at first and what to check before
  calling something done.
- **What you deliver.** The deliverables, with their shape (a
  reconciliation table, a PRD with these sections, a brief of this
  length), so the output is the thing a colleague would hand over, not
  an essay about it.
- **Standards.** The rules of the trade the work is held to, and the
  common mistakes to avoid.
- **Ask first / never.** The few things worth a question before
  starting, and the lines not crossed (a licensed professional's
  judgement, money moved, a message sent in the user's name).

The personas are written for an agent that has a folder to work in, can
run commands, read and write files, and is expected to finish the job
rather than hand steps back: questions are for what only the user
knows, not for what can be found out.

## The personas

Finance and legal: `accountant`, `bookkeeper`, `financial-analyst`,
`attorney`, `paralegal`, `compliance-officer`.

People and the office: `hr-business-partner`, `recruiter`,
`executive-assistant`, `office-manager`, `procurement-specialist`.

Marketing and communications: `marketing-manager`, `copywriter`,
`social-media-manager`, `seo-specialist`, `pr-communications-manager`,
`technical-writer`.

Product, design and data: `product-manager`, `project-manager`,
`business-analyst`, `ux-designer`, `ux-researcher`, `data-analyst`.

Engineering: `software-engineer`, `code-reviewer`, `qa-engineer`,
`it-support-specialist`.

Sales and customers: `account-executive`, `customer-success-manager`,
`customer-support-agent`.

## How Fulano uses them

Fulano keeps a clone of this repository and pulls it at launch and
every so often, so the personas are always the current ones. It reads
each `SKILL.md`'s frontmatter into an index the model sees. When a
request fits one ("can you look over this contract", "draft the launch
email", "reconcile the card statement against the ledger"), Fulano
fires its agent with that persona's body added to the agent's system
prompt, and the agent does the job as that specialist would: in the
project's folder, with the user's files, writing the result back as a
file and a summary.

The personas never override Fulano's own rules for its agents: nothing
leaves the Mac, nothing is deleted or sent in the user's name without
being asked, and the step that is the user's alone (a signature, a
payment, a password) is set up and handed over.

## Writing a new one

Copy the closest existing persona, keep the headings, and write what
that specialist would want a sharp new colleague to know on day one:
the process, the deliverable, the standards, the traps. Concrete beats
general: "a three-column reconciliation: ledger, statement, difference,
with every difference explained" is a persona; "be thorough" is not.
