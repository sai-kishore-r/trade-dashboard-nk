---
description: Token-efficient context discipline for agents working in this repo
alwaysApply: true
---

# Token optimization

- **Search before read:** Grep/Glob `src/Store`, `src/Components`, hook names before opening files
- **Never bulk-read:** `charting_library/`, `universe.json`, `package-lock.json`, `node_modules`
- **Narrow reads:** Use offset/limit; max ~80 lines unless actively editing
- **Start multi-file tasks:** Read `SKILLS.md`, pick one skill, load only that `SKILL.md`
- **Cross-repo:** Open sibling backend only when API/auth contracts change
- **One skill max:** Load one skill + its `reference.md` per task
