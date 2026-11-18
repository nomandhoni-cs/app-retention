# App Retention

An Agent Skill for designing, auditing, and testing why people get value from an app and choose to return. It translates the six patterns in an App Breakdown video into practical workflows: help people start, finish, stop, and resume at a useful moment. It separates product examples from evidence and works across app categories.

## Install

`app-retention.eskill` is a ZIP archive containing the `app-retention/` skill folder. The standard entry point is `app-retention/SKILL.md`. **Extract the archive first** for a local installation with the Vercel `skills` CLI. An extractor that requires `.zip` will accept the same bytes saved with a `.zip` filename.

```bash
unzip app-retention.eskill
```

From the root of the project where you want to use the skill, use Node.js 22.20+ and point the CLI at the extracted folder. Adjust the path as needed:

```bash
npx skills add /path/to/app-retention --list
npx skills add /path/to/app-retention --skill app-retention --copy
```

For a noninteractive install targeting a specific agent:

```bash
npx skills add /path/to/app-retention --skill app-retention -a codex --copy -y
```

To share via GitHub, put the contents of `app-retention/` at the repository root (so `SKILL.md` is directly at root). You can then install it with `npx skills add OWNER/app-retention --skill app-retention`. The [CLI reference](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) lists install options; the [Agent Skills spec](https://agentskills.io/specification) describes the format. Using the skill itself does not require Node, network access, or Python. Python is optional for the bundled helper scripts.

## Try it

Ask your agent to use the `app-retention` skill, for example:

- “Plan first use and a useful next-visit flow for a weekly invoicing app.”
- “Audit this onboarding for first-task blockers. Show what you verified, and what is a hypothesis.”
- “Plan an A/B test for a resume card. Our first-value baseline is 20%, and we care about a 3 percentage-point lift.”

## Files

```text
app-retention/
├── SKILL.md                  # Agent entry point and workflow
├── references/               # Six focused guides, loaded as needed
├── scripts/
│   ├── validate-skill.py      # Package and local link checks
│   └── plan-sample-size.py   # Approximate binary-outcome A/B test sizing
├── assets/                   # Build brief, audit and experiment templates; 65-source CSV
├── README.md
├── LICENSE
└── .gitignore
```

## Check your copy

From the extracted skill directory, run these with Python 3.8+ (standard library only):

```bash
python3 scripts/validate-skill.py
python3 scripts/plan-sample-size.py --baseline 0.20 --delta 0.03 \
  --eligible-per-week 1000 --follow-up-days 14
```

The calculator should give **2,943 units per arm** for that example, before losses or design adjustments. It is for independent, equal-allocation, fixed-horizon tests with one binary outcome. The directory check validates metadata, resource links, and the evidence index locally; it does not retest third-party URLs. To verify CLI discovery without installing, use the `--list` command above.

## Sources and license

The annotated [video guide](references/video-and-evidence.md) and [source library](references/source-library.md) credit the creator and link to studies, product documentation, and legal open copies where available. The original video, captions, and third-party publications are not redistributed here. The original skill instructions, research notes, templates, and scripts are [MIT-licensed](LICENSE); linked material retains its own terms.
