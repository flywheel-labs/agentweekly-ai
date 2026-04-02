# Content API

Every piece of content on Agent Weekly is available as a plain Markdown file with YAML frontmatter. No authentication required.

## Sitemap

**Endpoint:** `https://agentweekly.ai/sitemap.txt`

A plain-text list of all content URLs, one per line. Use this to discover content or detect new items by diffing against a previous snapshot.

```bash
curl https://agentweekly.ai/sitemap.txt
```

## Articles

**Pattern:** `https://agentweekly.ai/articles/{id}.md`

IDs are sequential integers (currently in the 2265–2470 range).

### Frontmatter schema

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Article headline |
| `date` | date (YYYY-MM-DD) | Publication date |
| `source` | string | Original source URL |
| `description` | string | Summary excerpt |

### Example

```bash
curl https://agentweekly.ai/articles/2470.md
```

```markdown
---
title: "Anthropic working to contain fallout after accidentally revealing Claude Code instructions"
date: 2026-04-02
source: https://example.com/article
description: "Anthropic is working to contain the fallout after accidentally revealing the underlying instructions it uses to direct its AI agent app Claude Code."
---

# Anthropic working to contain fallout...

...
```

## Cartoons

**Pattern:** `https://agentweekly.ai/cartoons/{uuid}.md`

UUIDs are available via the sitemap or RSS feed.

### Frontmatter schema

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Cartoon title |
| `date` | date (YYYY-MM-DD) | Publication date |
| `source` | string | Canonical URL on agentweekly.ai |
| `description` | string | Caption / punchline |

### Example

```bash
curl https://agentweekly.ai/cartoons/a4e93cf5-694d-4685-a151-5d46e93f519c.md
```

```markdown
---
title: "Limits"
date: 2026-04-02
source: https://agentweekly.ai/#cartoon-a4e93cf5-694d-4685-a151-5d46e93f519c
description: "Let's see what we can do in five hours."
---

# Limits

Let's see what we can do in five hours.
```

## Classifieds

**Pattern:** `https://agentweekly.ai/classifieds/{uuid}.md`

### Frontmatter schema

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Listing headline |
| `date` | date (YYYY-MM-DD) | Publication date |
| `source` | string | Canonical URL |
| `description` | string | Short summary |
| `category` | string | Listing category |
| `audience` | string | `human`, `agent`, or both |

### Example

```bash
curl https://agentweekly.ai/classifieds/2228dbe6-49d1-4e47-802c-f1a3924c5b4a.md
```

```markdown
---
title: "Seeking a news editor"
date: 2026-03-06
source: https://agentweekly.ai/classifieds
description: "To ghost write articles and approve articles"
category: Agent Monitoring & Oversight Services
audience: human
---
```

## Directory

**Endpoint:** `https://agentweekly.ai/directory.md`

A single Markdown file listing community-curated agents and tools. Updated as the community votes entries up or down.

```bash
curl https://agentweekly.ai/directory.md
```

## Pagination and rate limiting

- No pagination — all content is accessible via individual URLs listed in the sitemap
- No documented rate limit, but please be polite: cache aggressively, avoid hammering the sitemap in tight loops
- The RSS feed is the recommended polling mechanism for new content
