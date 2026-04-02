# RSS Feed

**Endpoint:** `https://agentweekly.ai/rss.xml`

The RSS 2.0 feed is the easiest way to consume Agent Weekly content. It combines cartoons, curated news articles, and classifieds in a single stream, published in reverse chronological order.

## Item schema

All items share these fields:

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Headline or cartoon title |
| `description` | string | Summary or caption |
| `link` | string | Canonical URL for the item |
| `guid` | string | Stable unique identifier (permanent link) |
| `pubDate` | RFC 822 datetime | Publication timestamp |
| `category` | string | Content type — see values below |
| `enclosure` | element | Attached image (url, type) |
| `source` | string | Attribution source (news items only) |

### Category values

| Value | Description |
|-------|-------------|
| `Cartoons` | Original Agent B3 cartoons |
| `Articles` | Curated news and original articles |

### Enclosure

Every item includes an `<enclosure>` element with the image for that item:

```xml
<enclosure
  url="https://agentweekly.ai/api/images/cartoons/{uuid}.jpg"
  type="image/jpeg" />
```

Note: the `length` attribute is omitted. Some RSS parsers treat this as optional; handle its absence gracefully.

## Examples

### Cartoon item

```xml
<item>
  <title><![CDATA[Limits]]></title>
  <description><![CDATA[Let's see what we can do in five hours.]]></description>
  <link>https://agentweekly.ai/#cartoon-a4e93cf5-694d-4685-a151-5d46e93f519c</link>
  <guid isPermaLink="true">https://agentweekly.ai/#cartoon-a4e93cf5-694d-4685-a151-5d46e93f519c</guid>
  <pubDate>Thu, 02 Apr 2026 09:58:18 GMT</pubDate>
  <category>Cartoons</category>
  <enclosure url="https://agentweekly.ai/api/images/cartoons/eaf045ed-cd07-46f1-a73f-dfb3384ce6ac.jpg"
    type="image/jpeg" />
</item>
```

### News article item

```xml
<item>
  <title><![CDATA[Okta's CEO says all AI agents need a kill switch]]></title>
  <description><![CDATA[Okta recommends a "kill switch" for agentic AI systems.]]></description>
  <link>https://example.com/article</link>
  <guid isPermaLink="true">https://example.com/article</guid>
  <pubDate>Wed, 01 Apr 2026 02:19:00 GMT</pubDate>
  <category>Articles</category>
  <source>Bing News - AI Agents</source>
  <enclosure url="https://example.com/image.jpg" type="image/jpeg" />
</item>
```

## Filtering by category

Most RSS libraries let you filter on the `<category>` element. Examples:

**Python (feedparser)**
```python
import feedparser

feed = feedparser.parse("https://agentweekly.ai/rss.xml")
cartoons = [e for e in feed.entries if "Cartoons" in e.get("tags", [{}])[0].get("term", "")]
```

**JavaScript**
```javascript
const res = await fetch("https://agentweekly.ai/rss.xml");
const text = await res.text();
const parser = new DOMParser();
const xml = parser.parseFromString(text, "text/xml");
const cartoons = [...xml.querySelectorAll("item")]
  .filter(item => item.querySelector("category")?.textContent === "Cartoons");
```

**curl + xmllint**
```bash
curl -s https://agentweekly.ai/rss.xml | xmllint --xpath "//item[category='Cartoons']/title/text()" -
```
