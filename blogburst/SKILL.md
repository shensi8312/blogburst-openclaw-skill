---
name: BlogBurst
description: AI content creation & distribution. Brainstorm titles, generate blog posts, and create optimized content for 9 platforms (Twitter, LinkedIn, Bluesky, Telegram, Discord, Reddit, TikTok, YouTube, Threads).
homepage: https://blogburst.ai
metadata:
  {"openclaw": {"emoji": "📝", "requires": {"env": ["BLOGBURST_API_KEY"]}, "primaryEnv": "BLOGBURST_API_KEY"}}
---

# BlogBurst - AI Content Creation & Distribution

BlogBurst helps you go from idea to published content across 9 social platforms. The typical workflow is:

1. **Brainstorm** a title with AI chat
2. **Generate** a full blog post from the title
3. **Create** platform-optimized posts for Twitter, LinkedIn, TikTok, etc.

You can also repurpose existing articles by URL.

## Setup

1. Sign up at [blogburst.ai](https://blogburst.ai)
2. Go to Dashboard > API Keys to generate a key
3. Set environment variable:
```bash
export BLOGBURST_API_KEY="your-key"
```

All API requests use the header: `X-API-Key: $BLOGBURST_API_KEY`

Base URL: `https://api.blogburst.ai/api/v1`

---

## API 1: Brainstorm Titles

Chat with AI to develop a compelling title for your content.

**Endpoint**: `POST /chat/title`

**Request**:
```json
{
  "messages": [
    {"role": "user", "content": "I want to write about AI in healthcare"}
  ],
  "language": "en"
}
```

This is a multi-turn conversation. Send the full message history each time:
```json
{
  "messages": [
    {"role": "user", "content": "I want to write about AI in healthcare"},
    {"role": "assistant", "content": "Great topic! What aspect interests you most?"},
    {"role": "user", "content": "AI helping doctors diagnose diseases faster"}
  ],
  "language": "en"
}
```

**Response**:
```json
{
  "success": true,
  "reply": "Here are some title ideas based on AI-assisted diagnosis...",
  "suggested_titles": [
    "How AI Detects What Doctors Miss in 5 Seconds",
    "Medical AI: From Assistant to Lifesaver",
    "When AI Becomes Your First Doctor"
  ],
  "usage": {"tokens_used": 350, "cost": 0.001, "model": "gemini-2.5-flash"}
}
```

**When to use**: When the user wants help coming up with a topic or title, or says things like "help me brainstorm", "what should I write about", "suggest some titles about X".

---

## API 2: Generate Blog Post

Generate a full blog article from a topic or title.

**Endpoint**: `POST /blog/generate`

**Request**:
```json
{
  "topic": "How AI Detects What Doctors Miss in 5 Seconds",
  "tone": "professional",
  "language": "en",
  "length": "medium"
}
```

**Parameters**:
- `topic` (required): The title or topic (5-500 chars)
- `tone`: professional | casual | witty | educational | inspirational (default: professional)
- `language`: Language code, e.g. "en", "zh" (default: en)
- `length`: short (500-800 words) | medium (1000-1500 words) | long (2000-3000 words) (default: medium)

**Response**:
```json
{
  "success": true,
  "title": "How AI Detects What Doctors Miss in 5 Seconds",
  "content": "Full markdown blog post content here...",
  "summary": "A concise summary of the article...",
  "keywords": ["AI", "healthcare", "diagnosis", "medical AI"],
  "usage": {"tokens_used": 2500, "cost": 0.005, "model": "gemini-2.5-flash"}
}
```

**When to use**: When the user wants to generate a blog post, article, or long-form content from a topic.

---

## API 3: Generate Platform Content

Generate optimized content for multiple social platforms from a topic. This is the main content distribution endpoint.

**Endpoint**: `POST /blog/platforms`

**Request**:
```json
{
  "topic": "How AI Detects What Doctors Miss in 5 Seconds",
  "platforms": ["twitter", "linkedin", "bluesky", "telegram", "discord"],
  "tone": "professional",
  "language": "en"
}
```

**Parameters**:
- `topic` (required): The title or topic (5-500 chars)
- `platforms` (required): Array of 1-9 platforms from: twitter, linkedin, reddit, bluesky, threads, telegram, discord, tiktok, youtube
- `tone`: professional | casual | witty | educational | inspirational (default: professional)
- `language`: Language code (default: en)

**Response**:
```json
{
  "success": true,
  "topic": "How AI Detects What Doctors Miss in 5 Seconds",
  "twitter": {
    "thread": [
      "1/ AI can now detect diseases that doctors miss. Here's how it's saving lives...",
      "2/ A study found AI caught 95% of early-stage cancers, vs 85% for radiologists.",
      "3/ The key? AI analyzes millions of images. A doctor sees thousands in a lifetime."
    ]
  },
  "linkedin": {
    "post": "I've been researching AI in healthcare for 2 years.\n\nThe results are staggering...",
    "hashtags": ["#AIHealthcare", "#MedTech", "#DigitalHealth"]
  },
  "bluesky": {
    "posts": ["AI is quietly revolutionizing medical diagnosis. Here's what most people don't know..."]
  },
  "telegram": {
    "post": "**AI in Medical Diagnosis: The Silent Revolution**\n\nDoctors are getting a powerful new ally..."
  },
  "discord": {
    "post": "Hey everyone! Wanted to share something fascinating about AI in healthcare..."
  },
  "reddit": {
    "title": "How AI is detecting diseases doctors miss - a deep dive",
    "body": "I've been following AI in healthcare closely and wanted to share...",
    "suggestedSubreddits": ["r/artificial", "r/healthcare", "r/technology"]
  },
  "tiktok": {
    "hook": "Did you know AI can detect cancer faster than a doctor?",
    "script": "Here's something wild. AI systems can now...",
    "caption": "AI is changing medicine forever",
    "hashtags": ["#AI", "#Healthcare", "#MedTech", "#Science"]
  },
  "youtube": {
    "title": "How AI Detects What Doctors Miss",
    "description": "In this video, we explore how artificial intelligence...",
    "script": "What if I told you that an AI can spot a disease...",
    "tags": ["AI healthcare", "medical AI", "diagnosis"]
  },
  "usage": {"tokens_used": 3000, "cost": 0.006, "model": "gemini-2.5-flash"}
}
```

**When to use**: When the user wants to create social media posts, distribute content across platforms, or says things like "create posts for Twitter and LinkedIn about X", "generate social content", "help me post about X on all platforms".

---

## API 4: Repurpose Existing Content

Transform an existing blog post or article into platform-optimized posts.

**Endpoint**: `POST /repurpose`

**Request with URL**:
```json
{
  "content": "https://myblog.com/my-article",
  "platforms": ["twitter", "linkedin", "bluesky"],
  "tone": "casual",
  "language": "en"
}
```

**Request with text**:
```json
{
  "content": "Your full article text here (minimum 50 characters)...",
  "platforms": ["twitter", "linkedin", "bluesky"],
  "tone": "casual",
  "language": "en"
}
```

**Parameters**:
- `content` (required): A URL to an article, or the full text
- `platforms` (required): Array from: twitter, linkedin, reddit, bluesky, threads
- `tone`: professional | casual | witty | educational | inspirational
- `language`: Language code (default: en)

**Response**: Same format as API 3 (platform-specific content for each requested platform).

**When to use**: When the user provides a URL or pastes existing content and wants it adapted for social platforms.

---

## Recommended Workflow

For the best results, guide the user through this flow:

1. Ask what topic they want to create content about
2. Call **API 1** (`/chat/title`) to brainstorm titles together
3. Once they pick a title, call **API 3** (`/blog/platforms`) to generate content for their chosen platforms
4. Present the generated content organized by platform

If the user already has a blog post URL, skip to **API 4** (`/repurpose`).

If the user wants a full blog article first, use **API 2** (`/blog/generate`) before step 3.

## Supported Platforms

| Platform | ID | Content Style |
|----------|-----|---------------|
| Twitter/X | twitter | Threads with hooks (280 chars per tweet) |
| LinkedIn | linkedin | Professional insights + hashtags |
| Bluesky | bluesky | Short authentic posts (300 chars) |
| Telegram | telegram | Rich formatted broadcasts |
| Discord | discord | Community-friendly announcements |
| Reddit | reddit | Discussion posts with subreddit suggestions |
| TikTok | tiktok | Hook + script + caption + hashtags |
| YouTube | youtube | Title + description + script + tags |
| Threads | threads | Conversational posts |

## Links

- Website: https://blogburst.ai
- API Docs: https://api.blogburst.ai/docs
- GitHub: https://github.com/shensi8312/blogburst-openclaw-skill
