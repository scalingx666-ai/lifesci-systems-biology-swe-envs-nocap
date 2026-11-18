# PARTIAL SNAPSHOT

This dataset was published from an **incomplete** generation run.

- Publish mode: partial_snapshot
- Generation-complete flag: generation_complete_expansion.flag - **ABSENT** (deliberately not faked)
- Snapshot taken (local): 2026-11-19 00:55:36 UTC+08:00
- Live tasks in the shared task bank at snapshot time: **53477**
- Repositories checkpointed at snapshot time: **1348** / 1372
- Original generation goal: **100000** tasks
- Progress at snapshot time: **53477 / 100000** (53.5%)
- This domain contains: **467** tasks from **16** repositories

## What this means for you

- The 100k real-pull-request generation run was **not finished** when
  this snapshot was taken; more tasks are added in later releases.
- This is **not** the final dataset and **not** a 100k dataset.
- Nothing here is fabricated: repositories that yielded zero tasks
  are listed in zero_repos.txt rather than padded.
- validate --deep --oracle covers static structure and oracle
  integrity only - it is **not** a graded Harbor reward (that needs
  Docker plus an LLM judge key).

