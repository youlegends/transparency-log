# YouLegends — Public Transparency Log

Append-only audit log of every lottery ticket spawned in YouLegends. Updated every 5 minutes by an automated server bot. Never amend, never force-push.

## What's here

One JSONL file per UTC day under tickets/YYYY-MM-DD.jsonl. Each line is one lottery ticket:

```json
{
"ticket_id": "uuid",
"giveaway_id": "uuid or null",
"video_id": "uuid or null",
"earned_at": "2026-05-26T14:32:11Z",
"source": "video|battle|streak|admin|first_video_bonus",
"user_hash": "sha256(user_id || daily-salt)"
}
```

The daily-salt for each UTC date is published in salts.json — rotated daily, never revoked. With the salt, anyone can verify which user_hash belongs to a given user on a given day, but cannot track the same user across days.

## Why

YouLegends runs a provably fair lottery. Before each draw, we commit to a snapshot of all eligible tickets via tickets_hash in the giveaway's fairness-proof record. This repository is the raw evidence that the eligible-tickets list wasn't fabricated after the fact — every ticket has been publicly logged here within ~5 minutes of being earned, long before the draw runs.

## Verifying a draw

Use tools/verify_giveaway.js from the main YouLegends repo. It re-reads this log and recomputes the winner sequence offline — no YouLegends infrastructure access required.

## License

Released into the public domain (CC0) — the data isn't "ours" to license. Snapshot freely.
