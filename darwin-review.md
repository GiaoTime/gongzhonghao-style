# Darwin Skill Review: gongzhonghao-style

Date: 2026-05-19
Mode: full_test_partial + final_static_check
Scope: Static Darwin rubric review, JSON validation, rule-consistency scan, and previously executed with-skill / baseline tests for the two highest-risk scenarios.

## Score

| Dimension | Weight | Rating | Weighted |
| --- | ---: | ---: | ---: |
| Frontmatter quality | 8 | 9 | 7.2 |
| Workflow clarity | 15 | 9 | 13.5 |
| Boundary coverage | 10 | 10 | 10.0 |
| Checkpoint design | 7 | 10 | 7.0 |
| Instruction specificity | 15 | 9 | 13.5 |
| Resource integration | 5 | 8 | 4.0 |
| Overall architecture | 15 | 9 | 13.5 |
| Tested performance | 25 | 9 | 22.5 |
| Total | 100 | - | 91.2 |

Final score: **91.2 / 100**

Previous score: **89.5 / 100**

Delta: **+1.7**

## Latest Changes Checked

- Added a top-priority "正文保真" constraint: default behavior is layout adaptation, not body expansion.
- Allowed title rewriting into a WeChat-friendly 爆款软文标题, while preventing unsupported claims in the title.
- Required the backend handoff to stop at `save_to_draft_box`.
- Changed publish permission to `author_manual_publish_only`.
- Clarified that the author must manually preview, confirm, and publish.
- Removed an internal conflict where the old opening rule could encourage adding new content.
- Reworked the literary sample so it uses source information only instead of adding new facts or scenes.
- Updated `evals/evals.json` to test: title may change, body may not expand, draft box only, author manual publish.

## Validation

### Static Checks

- `evals/evals.json`: valid JSON.
- Frontmatter length: 282 characters, well below the 1024-character limit.
- `SKILL.md`: 399 lines, below the recommended 500-line ceiling.
- `README.md`: 228 lines.
- No remaining `requires_user_confirmation` or `create_draft` action in current eval expectations.
- Current payload uses:
  - `action: save_to_draft_box`
  - `publish_permission: author_manual_publish_only`
  - `backend_preview: must_preview_before_author_publish`

### Prior With-Skill / Baseline Evidence

Workspace:

```text
/Users/zhangpeng/.agents/skills/gongzhonghao-style-workspace/
```

Eval 3, external link repost without source text:

- Baseline generated a complete article despite missing source text.
- Improved with-skill output refused to fabricate a publishable body and requested source/link/body metadata.
- Result: pass.

Eval 5, WorkBuddy handoff from short input:

- Baseline lacked a structured `wechat_draft_handoff`.
- Initial with-skill output had the payload but over-expanded the body.
- Final with-skill output used short draft mode, kept body concise, and included the handoff payload.
- Result: pass.

## Current Strengths

- Strong trigger coverage for WeChat Official Account, WorkBuddy, and Tencent ecosystem scenarios.
- Clear separation between body preservation and layout freedom.
- Title optimization is allowed, but constrained by source truth.
- Backend automation is bounded to saving drafts; author manual publish is mandatory.
- Unreadable links cannot become fabricated publishable articles.
- Five eval prompts now include objective/manual assertions.

## Remaining Optional Improvements

- Add a small assertion runner script if you want CI-style automated scoring after moving this into Git.
- Run all five evals with independent agents after the repo exists, so Darwin can record a complete Git-based ratchet history.

## Verdict

Ready to put into a Git repository. There are no blocking issues in the current skill package. The remaining items are optional automation improvements, not content or safety gaps.
