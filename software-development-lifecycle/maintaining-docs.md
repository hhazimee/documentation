# Maintaining This Documentation

> Keep docs accurate with minimal overhead. If you change the process, update the doc in the same PR.

---

## 1. Ownership

Every file has an owner **role** (not person). The owner is responsible for accuracy and quarterly review.

| Directory | Owner Role | Backup |
|-----------|-----------|--------|
| phases/ | Tech Lead | BA |
| standards/ | Tech Lead | Senior Dev |
| runbooks/ | BA | Tech Lead |
| templates/ | BA | Tech Lead |
| references/ | Tech Lead | QA Lead |
| diagrams/ | Tech Lead | Senior Dev |
| Root docs (README, getting-started, framework) | Tech Lead | BA |
| maintaining-docs.md | Tech Lead | — |
| clickup-workflow.md | BA | Tech Lead |

---

## 2. When to Update

Update documentation when:
- [ ] A process step changes (added, removed, reordered)
- [ ] A tool changes (new tool, tool replaced, tool removed)
- [ ] Team size changes (scaling notes may need adjustment)
- [ ] A post-mortem identifies a documentation gap
- [ ] A new team member reports confusion during onboarding

**Rule:** If you change the process, update the doc in the same PR. Documentation updates are not separate tasks.

---

## 3. How to Update

1. Edit the file directly in a feature branch
2. Submit a PR with the `docs` conventional commit type: `docs(scope): description [CU-xxxx]`
3. One reviewer approves (owner role or backup)
4. Update the `Last Verified` date in the file's metadata header (if present)
5. Merge

---

## 4. How to Add a New Document

Before creating a new file, check if an existing file can absorb the content. New files increase maintenance burden.

If a new file is truly needed:
1. Determine which directory it belongs in (standards/, runbooks/, templates/, references/)
2. Follow the format of existing files in that directory
3. Add a link from the relevant phase cheat sheet (phases/*.md)
4. Add a link from getting-started.md if it's a commonly accessed file
5. Add it to references/artifacts-checklist.md
6. Assign an owner role

---

## 5. How to Retire a Document

1. Create an `archive/` directory if it doesn't exist
2. Move the file to `archive/` with a note at the top: `> **Archived [date].** Replaced by [new-file.md](path/to/new-file.md).`
3. Remove links to the archived file from all navigation (README, getting-started, phase cheat sheets)
4. Do NOT delete — git history preserves content, but `archive/` makes retirement visible
5. Delete archived files after 6 months

---

## 6. Cross-Reference Maintenance

When renaming or moving a file, update all references:

```bash
# Find all references to an old path
grep -rn "old-filename.md" --include="*.md" .

# Verify no broken links after changes
grep -roh '\]\([^)]*\.md\)' --include="*.md" . | sort -u | while read link; do
  target=$(echo "$link" | sed 's/.*(\(.*\))/\1/')
  [ ! -f "$target" ] && echo "BROKEN: $target"
done
```

---

## 7. Quarterly Review

Every 3 months, each owner role:
1. Re-reads their assigned files
2. Checks for staleness (outdated tools, processes, team references)
3. Updates the `Last Verified` date
4. Creates a ClickUp task for any needed updates

**Schedule:** January, April, July, October — first week.

---

## 8. Annual Health Check

Once per year (January), the Tech Lead audits:
- [ ] All files still relevant? Remove or archive unused docs
- [ ] All `Last Verified` dates within 12 months?
- [ ] Any undocumented processes? Create new docs or add sections
- [ ] Any unused docs getting stale? Archive them
- [ ] Cross-references intact? Run the broken link check above
- [ ] Team has grown/shrunk? Update scaling notes in phase cheat sheets
