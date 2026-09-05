# Rules

Small, reusable policy documents that inform agents, profiles, and project-specific instructions. Each rule is human-maintained prose describing one concern; it is not itself an enforcement mechanism. Tool adapters (`tools/<tool>/`) and self-contained agent instructions (`agents/`) are what actually apply a rule in a given AI tool, translated into whatever mechanism that tool supports: a permission block, an agent's tool allow-list, a subagent's system prompt.

## What's here

| Rule | Concern | Applied as |
|---|---|---|
| [`git.md`](git.md) | Git is inspection-only by default: no commit, push, history rewrite, or branch changes without explicit authorization. | See the "permission rules" section of each tool's adapter README. |
| [`coding.md`](coding.md) | Follow existing project conventions, prefer focused changes, keep public APIs stable unless a change requires otherwise. | `agents/global/AGENTS.md`. |
| [`testing.md`](testing.md) | Build/type-check, run focused tests before broader ones, add a regression test for bug fixes. | `agents/global/AGENTS.md`; the `tester` subagent in both tool adapters. |

## Adding a rule

Keep each rule focused on one concern, short enough to read in full, and written as policy ("do X", "don't do Y") rather than narrative. A rule describes *what* the policy is; it's the job of `agents/global/AGENTS.md` or a tool adapter to describe *how* a specific tool enforces or follows it. If a new rule needs enforcement in a specific tool (a new permission pattern, a new agent restriction), update that tool's adapter under `tools/<tool>/` and note the mapping in the table above.
