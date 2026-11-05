# Repository Guidelines

## Skill Layout

Skills live directly under `skills/<skill-name>/`. Use lowercase, hyphen-separated names and keep the `SKILL.md` frontmatter `name` identical to the directory name.

Each skill contains:

- `SKILL.md`: invocation description and instructions.
- `agents/openai.yaml`: interface display name and short description.
- `references/`: bundled guidance, source attribution, and licenses.

## Maintaining Skills

When adding or renaming a skill, update its directory, frontmatter, interface metadata, and affected links together. Describe what the skill does and when to invoke it in the frontmatter `description`.

Keep `SKILL.md` focused on actions and reference selection. Link detailed guidance from `references/` using relative paths, with clear conditions for reading it. Match the existing two-space YAML indentation in `agents/openai.yaml`.

When changing behavior, keep the instructions, invocation description, and interface metadata consistent. Verify local links and heading anchors, then walk through a representative request to check which references are read and what result is expected.

## Bundled References

Preserve source attribution, licenses, and the distinction between requirements and recommendations. Keep skill-specific instructions separate from attributed source text.

Follow the owning skill's source-update rules. The Uber skill requires a complete, unmodified guide; the Google skill preserves all four bundled documents. When replacing references, check that the skill's links and reading instructions still match the new content.
