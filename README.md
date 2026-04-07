# query-github - AI Edge Gallery Skill for Gemma-4

A GitHub Explorer skill for [Google AI Edge Gallery](https://github.com/google-ai-edge/gallery) that enables the [Gemma-4](https://deepmind.google/models/gemma/gemma-4/) model to search and explore GitHub directly from your mobile device.

## What it does

This skill extends Gemma-4's capabilities with GitHub API access, allowing you to:

- **Search repositories** by keyword, language, or topic
- **View repository details** including stars, forks, language, license, and topics
- **List issues** from any public repository (open, closed, or all)
- **List pull requests** with branch information and status
- **Look up user profiles** with stats, bio, and social links

All results are displayed in a mobile-optimized dark-themed webview with GitHub-style cards.

## Requirements

- [AI Edge Gallery](https://play.google.com/store/apps/details?id=com.google.ai.edge.gallery) app installed
- Gemma-4 model downloaded in the app (E2B or E4B recommended for mobile)
- Internet connection (for GitHub API calls)

## How to import

### Option 1: Import via URL

In AI Edge Gallery, load the skill using this URL:

```
https://raw.githubusercontent.com/iokinpardo/gamma-4/claude/github-skill-gemma-dNhmA/skills/query-github/
```

### Option 2: Clone and load locally

```bash
git clone https://github.com/iokinpardo/gamma-4.git
cd gamma-4
```

Then push the `skills/query-github/` directory to your device:

```bash
adb push skills/query-github/ /sdcard/Download/query-github/
```

Load it from local storage in the AI Edge Gallery app.

## GitHub Token (optional)

The skill works without authentication using GitHub's public API (60 requests/hour). For higher rate limits (5,000 requests/hour), provide a Personal Access Token:

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Generate a new token (classic) with `public_repo` scope
3. When prompted by AI Edge Gallery, enter the token

## Skill structure

```
skills/query-github/
├── SKILL.md              # Skill metadata and LLM instructions
└── scripts/
    ├── index.html        # JavaScript handler (GitHub API calls)
    └── webview.html      # Interactive results display
```

## Example prompts

Once the skill is loaded with Gemma-4, try asking:

- "Search for the most popular machine learning repositories"
- "Show me the details of the google/gemma repository"
- "What are the open issues in facebook/react?"
- "List the pull requests in tensorflow/tensorflow"
- "Tell me about the GitHub user torvalds"

## Supported actions

| Action | Description | Required fields |
|--------|-------------|-----------------|
| `search_repos` | Search repositories | `query` |
| `get_repo` | Repository details | `owner`, `repo` |
| `list_issues` | List issues | `owner`, `repo` |
| `list_pulls` | List pull requests | `owner`, `repo` |
| `get_user` | User profile | `username` |

## License

MIT
