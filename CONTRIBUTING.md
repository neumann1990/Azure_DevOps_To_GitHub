# Contributing

These are working notes, not documentation. Rough and current beats polished and stale.

## Adding something

1. Find the folder it belongs to (see [`README.md`](README.md)). If nothing fits, drop it in [`session/03-open-questions.md`](session/03-open-questions.md) and sort it later.
2. Write the bullet. Add a `Source: <url>` line under it if it came from somewhere.
3. Set the file's `status` in the frontmatter honestly — downgrade it to `researched` if you added something you haven't tested.
4. Bump `updated`.

## The two callouts

Keep these intact. They are the only thing separating Kevin's judgement from scraped research.

```markdown
> **Kevin:** My own opinion, experience, or decision.

> ⚠️ **Unverified.** From a source I don't fully trust, or a number that may have moved.
```

## When you verify something hands-on

Change `status: researched` to `status: verified` and say what you actually ran. A verified claim is one someone executed, not one they read twice.

## New files

Copy the frontmatter block from any existing file, then add a row to the folder's index table so it's discoverable.

## Working with Claude on this repo

[`AGENTS.md`](AGENTS.md) tells an agent how to navigate the repo and what not to do with it. If you change the conventions above, change `AGENTS.md` to match — otherwise agents will keep following the old rules.
