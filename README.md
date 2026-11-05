# Skills

A collection of coding agent skills for code review, Go style, and Git commit messages. Each skill bundles reference documents for offline use.

## Available skills

| Skill | Purpose |
| --- | --- |
| [code-review](skills/code-review/SKILL.md) | Review changes against requirements and project standards, with risk assessment, evidence, and prioritized findings. |
| [conventional-commits](skills/conventional-commits/SKILL.md) | Draft, revise, and review commit messages using Conventional Commits 1.0.0. |
| [google-go-style](skills/google-go-style/SKILL.md) | Write, refactor, and review Go code using Google's Go Style Guide, Style Decisions, and Best Practices. |
| [uber-go-style](skills/uber-go-style/SKILL.md) | Write, refactor, and review Go code using the complete Uber Go Style Guide. |

## Install

The [Skills CLI](https://github.com/vercel-labs/skills) requires Node.js 22.20 or later. Run this command from your project:

```sh
npx skills add mingo-liu/skills
```

Follow the prompts to select skills and target agents. Skills install to the current project by default. Add `-g` to install globally.

To install a specific skill:

```sh
npx skills add mingo-liu/skills --skill google-go-style
```

## Use

After installation, name the skill and task in your request. For example:

```text
Use code-review to review the current branch against main and report actionable findings.
```

```text
Use conventional-commits to draft a commit message for the staged changes.
```

```text
Use google-go-style to review naming and error handling in this Go package.
```

```text
Use uber-go-style to refactor this function while preserving its behavior.
```

For Go style, choose the guide that matches your project's conventions.

## Contribute

Skills live in `skills/<skill-name>/`. Each directory contains `SKILL.md`, `agents/openai.yaml`, and `references/`. Read the [Repository Guidelines](AGENTS.md) before adding or changing a skill.
