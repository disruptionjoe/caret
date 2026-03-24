# Capture-Before-Route

## Notation

```
^^ [intake agent: clean slate]
  capture input → /data/intake/[timestamp]-[source].md
    [extraction header: preview only]
    [original text: preserved as-is]
    [no disposition decision]

^ [review agent: separate pass]
  walk each item in /data/intake/
    read extraction header
    route to disposition gate
```

## What it does

Splits intake and routing into two separate operations run by different agents at different times. The intake agent captures the raw input (message, email, file, document) without judgment. Writes one file per item to a holding area. Includes an extraction header that previews what's inside but takes no action. A separate review pass, hours or days later, reads each file and routes it.

## When to use it

When you need a record of everything that came in. When intake rate is variable and you want to decouple arrival from processing. When you want humans to review and approve routing before the system acts. When you need to handle back-pressure: if the downstream system is slow, intake can keep working without blocking. When you can afford latency in exchange for completeness.

## When not to use it

When you need real-time routing. When disk space is constrained and you can't afford to keep an intake buffer. When you need to prevent duplicates and you can only afford one pass. When the system is so simple that a single routing decision at intake time is sufficient.

## Design notes

Separation of concerns. One agent captures. One agent routes. They don't need to talk to each other except through the file system. The intake agent's only job is to move raw input from external source to /data/intake/. It doesn't read, parse, or decide anything. It stores. That's all.

The extraction header is metadata. It lives at the top of the file and contains just enough information for the review agent to make an informed routing decision without re-reading the whole document. Example: subject line, first paragraph, sender, date, file type. Enough to categorize. Not the whole content.

Original text is preserved as-is. If the input was an email, store the full email. If it was a Slack message with threading, store the threading. Don't clean it. Don't normalize it. Don't reformat it. You may learn later that what looked like noise was important. Preserve it.

Naming matters. Use a consistent timestamp format (ISO 8601) and source identifier. `/data/intake/2026-03-24T09:30:00Z-email-alice@example.com.md` is better than `/data/intake/new-item.md`. It tells you when it arrived and where it came from without opening the file.

The intake agent is deliberately restricted. Give it read access to the input source and write access to /data/intake/. Don't give it access to the downstream system. Don't give it authority to approve or classify. This prevents the intake agent from making mistakes that cascade. If intake is wrong, you lose one item. If intake routes wrong, you waste time on a misclassified item.

The review pass is separate. It runs on a schedule (daily, hourly) or on demand. It reads each file in /data/intake/, checks the extraction header, decides on disposition, then moves or deletes the file. Once routed, the file is out of /data/intake/. The goal is to keep /data/intake/ as a transient buffer, not a database.

Duplicates are your problem. If the same email arrives twice, intake captures it twice. The review agent must detect and handle duplicates. This is actually good: it forces you to build deduplication logic in one place (the review agent) rather than trying to do it at intake. Simpler and more auditable.

Backpressure is managed automatically. If intake is fast and review is slow, items accumulate in /data/intake/. You can see how many items are pending just by counting files. You can parallelize the review pass by spinning up more review agents. You can also slow down intake if needed. The separation gives you visibility and control.

Latency is the cost. Between arrival and routing, there's a delay. For urgent items, this is unacceptable. For batch items, it's fine. Know which you have. If you need real-time routing for some items and batch routing for others, consider a hybrid: fast-path routing for urgent items, then capture-before-route for the rest.

Storage is your other cost. Each item takes up disk space. If intake is very high-volume and items are large, /data/intake/ can fill up. Implement a cleanup policy: delete items after review, or after a time limit, or both. Don't let it grow unbounded.

The extraction header format should be machine-readable (YAML or JSON) so that the review agent can parse it without re-reading the whole file. This makes the review agent faster and keeps it focused.

Testing is straightforward. Test intake by feeding it various input types and verifying that files appear in /data/intake/ with the right timestamps and extraction headers. Test review by hand-crafting files in /data/intake/ and verifying that the review agent routes them correctly. Test deduplication by creating two identical items and verifying that review detects and handles it.

One warning: don't use capture-before-route as an excuse to avoid thinking about structure. The extraction header still needs to be designed. It still needs to capture the right signals. An incomplete extraction header makes the review agent's job harder. Invest in getting it right.
