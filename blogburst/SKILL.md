# BlogBurst - AI Content Repurposing

Turn any article or blog post into 10+ social media posts in seconds.

## What it does

BlogBurst automatically transforms your long-form content into platform-optimized social media posts for:
- Twitter/X (threads)
- LinkedIn
- Bluesky
- Telegram
- Discord
- Reddit
- Product Hunt

## Usage

### Repurpose an article URL
```
Repurpose this article for social media: https://example.com/my-blog-post
```

### Repurpose text content
```
Turn this into social posts:

[paste your article text here]
```

### Specify platforms
```
Create Twitter and LinkedIn posts from: https://example.com/article
```

## API Integration

This skill uses the BlogBurst API. You'll need a free API key from [blogburst.ai](https://blogburst.ai).

### Setup

1. Get your API key at https://blogburst.ai/dashboard/api
2. Set the environment variable:
```bash
export BLOGBURST_API_KEY="your-api-key"
```

### API Endpoint

```bash
curl -X POST https://api.blogburst.ai/api/v1/repurpose \
  -H "Authorization: Bearer $BLOGBURST_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "Your article text or URL here",
    "platforms": ["twitter", "linkedin", "bluesky"],
    "tone": "professional",
    "language": "en"
  }'
```

### Response

```json
{
  "results": {
    "twitter": {
      "thread": ["1/ First tweet...", "2/ Second tweet...", "3/ Final tweet #hashtag"]
    },
    "linkedin": {
      "post": "Full LinkedIn post content...",
      "hashtags": ["#ContentMarketing", "#AI"]
    },
    "bluesky": {
      "posts": ["Short post for Bluesky..."]
    }
  }
}
```

## Examples

### Example 1: Quick repurpose
```
User: Repurpose my latest blog post about AI automation for Twitter and LinkedIn

OpenClaw: I'll use BlogBurst to create optimized posts...

[Returns Twitter thread + LinkedIn post]
```

### Example 2: Batch content
```
User: Create a week's worth of social content from this article

OpenClaw: I'll generate varied posts for each platform...

[Returns multiple posts per platform with different angles]
```

## Supported Platforms

| Platform | Character Limit | Features |
|----------|----------------|----------|
| Twitter/X | 280 | Threads, hashtags |
| LinkedIn | 3000 | Long-form, hashtags |
| Bluesky | 300 | Short posts |
| Telegram | 4096 | Markdown, longer content |
| Discord | 2000 | Markdown, embeds |
| Reddit | 40000 | Title + body, subreddit suggestions |
| Product Hunt | 1000 | Tagline, description, maker comment |

## Tone Options

- `professional` - Business-appropriate
- `casual` - Friendly and relaxed
- `witty` - Clever and humorous
- `educational` - Informative and teaching-focused

## Language Support

- English (`en`)
- Chinese (`zh`)
- More coming soon

## Links

- Website: https://blogburst.ai
- API Docs: https://api.blogburst.ai/docs
- Support: support@blogburst.ai

## Tags

content-repurposing, social-media, ai, automation, twitter, linkedin, bluesky, marketing
