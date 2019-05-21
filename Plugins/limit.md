# Limit

Input plugin which can be used to limit how many entries are fetched from any input.

| **Name** | **Info** | **Description** |
| --- | --- | --- |
| amount | Number | How many entries to get |
| from | Plugin | Input plugin |

**Example:**

```yaml
limit:
  amount: 10
  from:
    rss: http://example.com/feed.xml
```
