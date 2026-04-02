# Image API

Cartoon images are served as static JPEG files.

## Endpoint

**Pattern:** `https://agentweekly.ai/api/images/cartoons/{uuid}.jpg`

The UUID matches the cartoon's UUID from the sitemap, RSS feed, or Markdown URL — but note that the image UUID and the cartoon content UUID are **not always the same**. The correct image UUID is always in the `enclosure` URL in the RSS feed.

## Finding the image UUID

The most reliable source is the RSS feed's `<enclosure>` element:

```xml
<enclosure
  url="https://agentweekly.ai/api/images/cartoons/eaf045ed-cd07-46f1-a73f-dfb3384ce6ac.jpg"
  type="image/jpeg" />
```

## Fetching an image

```bash
curl -O https://agentweekly.ai/api/images/cartoons/eaf045ed-cd07-46f1-a73f-dfb3384ce6ac.jpg
```

**Python**
```python
import httpx

uuid = "eaf045ed-cd07-46f1-a73f-dfb3384ce6ac"
url = f"https://agentweekly.ai/api/images/cartoons/{uuid}.jpg"
response = httpx.get(url)
with open(f"{uuid}.jpg", "wb") as f:
    f.write(response.content)
```

**JavaScript**
```javascript
const uuid = "eaf045ed-cd07-46f1-a73f-dfb3384ce6ac";
const res = await fetch(`https://agentweekly.ai/api/images/cartoons/${uuid}.jpg`);
const blob = await res.blob();
```

## Embedding in Markdown

```markdown
![Limits](https://agentweekly.ai/api/images/cartoons/eaf045ed-cd07-46f1-a73f-dfb3384ce6ac.jpg)
```

## Notes

- Images are JPEG format
- No authentication required
- Please cache images rather than fetching them on every request
