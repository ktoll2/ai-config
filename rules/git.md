# Git Rules

Git operations are inspection-only unless explicitly authorized: `status`,
`diff`, `log`, `show`, and `blame` are always fine.

- Do not commit, push, pull, fetch, merge, rebase, cherry-pick, reset, or
  amend history without explicit authorization for that specific action.
- Do not create, delete, or switch branches or tags, or change Git
  configuration, without explicit authorization.
- Never force-push, and never discard user changes (`checkout`, `restore`,
  `reset`, or `clean` against uncommitted work) without explicit
  authorization.
- Before any command that could discard uncommitted work, check status first
  and preserve what's there (stash or commit) rather than overwrite it.
- Authorization covers the specific action and scope requested, not every
  future Git operation: approval to push once doesn't imply approval to push
  again later, or to push somewhere else.
