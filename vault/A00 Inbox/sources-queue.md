# Sources Queue

Drop links and file paths here to be processed by the agent on the next `/ingest`.

> **Agent rule:** For each item — fetch the URL or read the local file, save raw content to `D00 Claude/sources/`, process into `C01 Wiki/`, move the raw file to `D00 Claude/sources/processed/`, then **remove the line from this file**. Failed fetches stay in the queue with a `<!-- fetch failed: reason -->` comment. Never delete the file itself — keep the header and the empty `### Sources queue` section intact.

### Sources queue

