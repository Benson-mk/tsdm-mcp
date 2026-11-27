# Issue tracker: GitHub

Use `gh` for issues and specs in `Benson-mk/tsdm-mcp`.

- Publish: `gh issue create --title "..." --body "..."`. Use a heredoc for multiline bodies.
- Fetch: `gh issue view <number> --json number,title,body,labels,comments`.
- List: `gh issue list` with the relevant `--state` and `--label` filters.
- Comment: `gh issue comment <number> --body "..."`.
- Change labels: `gh issue edit <number> --add-label "..."` or `--remove-label "..."`.
- Close: `gh issue close <number> --comment "..."`.

**PRs as a request surface: no.**

## Wayfinding

- Keep the map in one issue labeled `wayfinder:map`. Link child tickets as GitHub sub-issues
  and label them `wayfinder:<type>` (`research`, `prototype`, `grilling`, or `task`).
  If sub-issues are unavailable, use a map task list and put `Part of #<parent>` in each child.
- Use native issue dependencies. To add a blocker, get its database ID with
  `gh api repos/{owner}/{repo}/issues/<blocker> --jq .id`, then run
  `gh api --method POST repos/{owner}/{repo}/issues/<child>/dependencies/blocked_by -F issue_id=<id>`.
  If dependencies are unavailable, put `Blocked by: #<number>` in the child body.
- In map order, pick the first open, unassigned child with no open blockers.
  Claim it with `gh issue edit <number> --add-assignee @me` before other writes.
- To resolve a child, comment with the answer, close it, and add a context pointer
  to the map's Decisions-so-far.
