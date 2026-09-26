---
name: repodify
description: "Instructions and context for interacting with the Repodify Podcast ecosystem (MCP and API)"
---

# Repodify AI Skill

You are operating within the Repodify ecosystem, a programmatic platform for creating and managing custom podcast RSS feeds ("Repodcasts").

## Core Capabilities

As an AI agent, you can natively manage Repodify feeds by connecting to the Repodify MCP Server.

### Installation
If the MCP server is not already in your context, you can instruct the user to configure it as a Server-Sent Events (SSE) MCP server pointing to:
`https://repodify.app/api/mcp`

Ensure they pass their API key in the configuration headers: `Authorization: Bearer <REPODIFY_API_KEY>`.

### MCP Tools
When connected, you have access to the following tools:
1. `search_apple_podcasts`: Search the Apple Podcasts directory to extract `audioUrl` links for episodes.
2. `create_repodcast`: Spin up a new feed and receive a `slug`.
3. `add_episode_to_repodcast`: Add an `audioUrl` to a specific feed using its `slug`.
4. `delete_repodcast`: Destroy a feed.
5. `list_feeds`: Check what feeds the user currently has.
6. `get_repodcast_details`: Fetch feed metadata and a list of all episodes with their IDs.
7. `reorder_episodes`: Change the order of episodes in a feed.
8. `update_repodcast`: Edit the feed's name, description, or image.
9. `submit_repodcast`: Submit the feed to the global PodcastIndex directory.
10. `delete_episode`: Remove a specific episode from a feed.
11. `update_episode`: Edit a specific episode's title, description, audioUrl, or imageUrl.
12. `get_repodcast_stats`: Fetch total XML fetches and actual MP3 downloads for a feed.
13. `update_profile`: Update the user's public profile (displayName, bio, imageUrl).

## Direct API Capabilities (Beyond MCP)
If you need to upload an audio file natively instead of just attaching a URL, Repodify provides two options:
1. Hit `POST /api/upload` (multipart/form-data) to get an S3 URL, then use the `add_episode_to_repodcast` MCP tool.
2. Hit `POST /api/v1/feeds/[slug]/episodes/upload` (multipart/form-data with `file` and `title`) to upload the MP3 and construct the episode in a single REST request.
3. Hit `POST /api/v1/profile/upload` (multipart/form-data with `file`) to upload a new avatar. This natively deletes the old avatar from cloud storage to save space.

## Workflow Example: Building a Playlist
If the user asks you to "Build a mixtape about History", you should:
1. Call `create_repodcast` with the name "History Mixtape".
2. Call `search_apple_podcasts` with the term "History" or specific historical events.
3. Loop through the search results and call `add_episode_to_repodcast` for the best matches.

Always inform the user when you have successfully constructed their feed.
