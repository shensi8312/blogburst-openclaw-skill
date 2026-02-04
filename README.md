# BlogBurst OpenClaw Skill

Official OpenClaw skill for [BlogBurst](https://blogburst.ai) - AI-powered content repurposing.

## Installation

```bash
npx clawhub@latest install blogburst
```

Or manually:
```bash
cd ~/.openclaw/skills
git clone https://github.com/AugmentOS/blogburst-skill.git blogburst
```

## Setup

1. Sign up at [blogburst.ai](https://blogburst.ai)
2. Get your API key from the dashboard
3. Set the environment variable:

```bash
export BLOGBURST_API_KEY="your-api-key"
```

## Usage

Just ask OpenClaw:

```
Repurpose this article for Twitter and LinkedIn: https://myblog.com/article

Turn this into social media posts:
[paste your content]

Create a week of social content from my latest blog post
```

## Features

- Supports 7+ platforms (Twitter, LinkedIn, Bluesky, Telegram, Discord, Reddit, Product Hunt)
- Multiple tone options (professional, casual, witty, educational)
- Multi-language support (English, Chinese)
- Platform-optimized content with correct character limits

## Links

- [BlogBurst Website](https://blogburst.ai)
- [API Documentation](https://api.blogburst.ai/docs)
- [OpenClaw](https://openclaw.ai)

## License

MIT
