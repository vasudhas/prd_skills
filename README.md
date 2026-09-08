# PRD Skills Toolkit

Three companion skills for writing and evaluating Product Requirements Documents (PRDs), built around a 14-section template, a five-question core, a seven-anti-pattern checklist, and a problem-statement quality bar.

| Skill | What it does | Use when |
|---|---|---|
| `write-spec` | Drafts a full PRD with you, from an idea or problem statement | You want AI to help write the document |
| `write-spec-template` | Hands you a blank template + the prompting questions, writes none of your content | You want to write the PRD yourself, just need structure |
| `write-spec-evaluator` | Scores an existing PRD and returns a Must-fix / Quick-fix / Okay-to-have report | You have a draft (yours or someone else's) and want it critiqued |

Each skill lives in its own folder under `skills/` as a single `SKILL.md` file — plain markdown with a small YAML header (`name`, `description`, `argument-hint`). That format is native to Claude's Skills system, but the content is just instructions, so any AI tool that can read a long system prompt can use it — see [Using this outside Claude](#using-this-outside-claude) below.

```
prd-skills-toolkit/
├── README.md
├── LICENSE
└── skills/
    ├── write-spec/SKILL.md
    ├── write-spec-template/SKILL.md
    └── write-spec-evaluator/SKILL.md
```

---

## Using this with Claude

**Claude.ai / Claude Desktop / Claude Cowork (personal skills):**
1. Go to Settings → Capabilities (or the Skills section of Settings — the exact path varies by platform and may move).
2. Upload each `SKILL.md` as a new custom skill (each one becomes its own skill — do not merge them into one upload).
3. Once added, invoke by name in chat, e.g. "use write-spec to draft a PRD for X" — or just describe the task; the description field is written to trigger automatically for matching requests.

**Claude Code:**
- Drop each folder (`write-spec/`, `write-spec-template/`, `write-spec-evaluator/`) into your project's or user-level skills directory per Claude Code's skill-loading convention. Check `docs.claude.com` for the current path, since this can change between releases.

If you're not sure of the current menu path or feature name, search Anthropic's docs at the time you set this up — product surfaces move faster than this README will be updated.

## Using this outside Claude

The `SKILL.md` files are not special file formats — they're markdown instructions. Any tool that lets you set a persistent system prompt, custom instructions, or just paste a long message at the start of a conversation can use them. The YAML header at the top (between the `---` lines) is metadata for Claude's skill loader specifically; other tools will just ignore it or read it as ordinary text — you don't need to strip it, but you can if you want a cleaner prompt.

### ChatGPT

**Option A — Custom GPT (best for repeated use):**
1. Go to **Explore GPTs → Create**.
2. In the **Instructions** field, paste the skill's content. `write-spec-template.md` fits under the ~8,000-character instructions limit as-is; `write-spec.md` and `write-spec-evaluator.md` are longer, so for those:
   - Either trim the instructions field to the core workflow steps and upload the full `SKILL.md` as a **Knowledge** file, with a line in Instructions like "Before responding, consult the attached SKILL.md for the full process and templates."
   - Or paste the full file anyway — GPT Instructions fields have grown over time, so check the current limit in the builder UI before trimming.
3. Save, and optionally add a conversation starter like "Evaluate this PRD" or "Draft a PRD for [feature]".
4. Repeat for each of the three skills as separate GPTs (e.g. "PRD Writer", "PRD Template", "PRD Evaluator") — one skill per GPT keeps the instructions focused and matches how they're designed to hand off to each other by name.

**Option B — ChatGPT Projects:**
1. Create a new Project.
2. Add the relevant `SKILL.md` file(s) to the Project's files.
3. Add a short Project instruction: "Follow the workflow and templates in the attached SKILL.md files. If asked to draft a PRD, use write-spec's process; if asked to evaluate one, use write-spec-evaluator's report format."

**Option C — No setup, one-off use:**
Paste the entire contents of the relevant `SKILL.md` at the start of a new chat, followed by your actual request (the feature idea, or the PRD to evaluate). Works in a single conversation with zero configuration; you'll need to re-paste it each new chat.

### Gemini, Copilot, Claude alternatives, and other chat tools

The same three options generally apply, under different names:
- **Gemini** → "Gems" (Gemini's equivalent of Custom GPTs): paste into the Gem's instructions.
- **Microsoft Copilot** → Copilot Studio custom agents, or just custom instructions in a chat.
- **Any API-based tool** (your own app calling an LLM API) → pass the `SKILL.md` content as the `system` message, and the user's actual request as the user message.

The underlying pattern is always the same: **the SKILL.md content is your system prompt; the user's feature idea or PRD draft is the first user message.**

### A note on cross-tool consistency

These skills were written and tuned against Claude's behavior (how it follows multi-step workflows, table formatting, etc.). Other models may follow the workflow slightly differently — e.g., skip a step, or format a table differently. If you hit that, add an explicit line to the instructions like "Follow every numbered step in order and do not skip the severity-sorting step before writing the report" to reinforce it for that specific model.

---

## Uploading this to GitHub

If you have a GitHub account and `git` installed locally:

```bash
# 1. Create a new repo on GitHub first (via github.com → New repository),
#    then clone it locally, OR initialize this folder as a new repo:

cd prd-skills-toolkit
git init
git add .
git commit -m "Initial commit: PRD skills toolkit"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo-name>.git
git push -u origin main
```

If you don't want to use the command line:
1. Go to github.com → **New repository** → name it (e.g. `prd-skills-toolkit`) → **Create repository**.
2. On the new repo's page, click **uploading an existing file**.
3. Drag in the whole `prd-skills-toolkit` folder (or its contents) and commit.

Either way, downstream users can then either `git clone` the repo, or grab a single file's raw content directly from a URL like:
```
https://raw.githubusercontent.com/<your-username>/<your-repo-name>/main/skills/write-spec/SKILL.md
```
— useful for pasting straight into a Custom GPT or Gem without downloading anything.

## License

An MIT license is included as a permissive default — swap it for whatever your organization requires before publishing.
