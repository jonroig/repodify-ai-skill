---
name: analytics-digest
description: Generates a beautiful Markdown summary of all active feeds and their Axiom/Firebase analytics. Use this skill when the user asks for a report of their feed performance or when running a cron job to send weekly reports.
---

# Analytics Digest Skill

This skill pulls the latest analytics for all of the user's Repodcast feeds and formats them into a beautifully structured Markdown report artifact.

## Workflow

1. **Verify Authentication**: Ensure you are authenticated with the MCP or API. If running as a background task, ensure you have the `repodify_live_...` Bearer token context.
2. **Fetch Feeds**: Either query the API for the list of the user's feeds or ask the user for a specific feed slug. (If running globally, fetch the most popular feeds).
3. **Pull Stats**: Use the `get_repodcast_stats` tool for each feed.
4. **Generate Artifact**: Create a Markdown artifact using `write_to_file` in the artifacts directory.
   - Use a clear `# Analytics Report` header.
   - Use a Markdown table to compare feeds.
   - Highlight feeds that have massive `totalEpisodeDownloads` (Axiom plays).
5. **Present**: Once the artifact is created, notify the user.

## Formatting Guidelines
- Separate "Feed XML Requests" from "Actual MP3 Downloads".
- Use Mermaid diagrams if there is chronological data, but since the endpoint returns total stats, a clean table is preferred.
