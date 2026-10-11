# Carbon League replay snapshot

Last successful snapshot prepared: **2026-10-11T02:15:42+00:00** (UTC). Games: **400**.

This dedicated repository contains only trusted, public match data. It is
replaced with a single root commit on every meaningful export. Clone with:

```sh
git clone --depth 1 https://github.com/JUZI1/carbon-league-replays.git
```

Use the actual repository URL in place of OWNER/REPOSITORY. No GitHub API,
raw.githubusercontent.com, archive download, or Git LFS is required. For a clean
shallow clone with **no local commits or edits**, updates also work with:

```sh
git pull --rebase --depth 1 origin main
```

Ordinary merge-based `git pull` may reject rewritten history. A new disposable
`git clone --depth 1` for each refresh is the most predictable and bounded option.
Keep analysis outputs outside the clone. A long-lived clone can retain unreachable
old objects locally; recreate it periodically (or use local Git garbage collection)
to reclaim disk space. The main branch itself always has just one reachable commit.

## Files and fields

- `replays/<id>-<game>.json.gz`: byte-for-byte copies of authenticated website
  `/data/<id>/<game>` downloads, without recompression or transformation.
- `index.json`: JSON array of the games included in this snapshot. `id` is the
  match ID; `game` is the 1-based game number. `created`/`finished` are Unix
  timestamps (seconds). `strategies.a`/`.b` contain only public strategy IDs and
  names. `scores`, `winner`, `statuses`, and `action_timing` use slots `a`/`b`.
  `order[0]` and `order[1]` map replay player indices to these slots. `steps` is
  the referee's step count. `action_timing.<slot>.total_seconds` is total strategy
  action time. `file` is the relative gzip path. Missing legacy values are null.
- `leaderboard.json`: the complete public `/api/leaderboard` response at export
  time, including its already-public author display names; no account records.

The default scope is completed games from the last 7 days with retained replays,
up to 400 newest games. Administrators can limit the scope by public strategy ID
or author display name (either match qualifies). Expired/over-limit files disappear
from the next snapshot. The index and files are authoritative for this snapshot.
Retention, changed export settings, public metadata, or leaderboard changes can publish an updated snapshot even without a new game. Identical snapshots make no commit. The leaderboard updates with each
publication.

Strategy source, embedded models, private diagnostics, account IDs/passwords,
session data and credentials are never added. Force-pushing bounds reachable Git
history; GitHub decides when unreachable old objects are garbage-collected, so
removal is not a guarantee that previously public data cannot be recovered.
