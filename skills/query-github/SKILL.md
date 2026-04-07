---
name: query-github
description: Search GitHub repositories, view issues, pull requests, and user profiles using the GitHub API. Use this skill when the user asks about GitHub projects, code repositories, open source software, or developer profiles.
metadata:
  homepage: https://github.com/iokinpardo/gamma-4
  require-secret: true
  require-secret-description: "Enter your GitHub Personal Access Token for higher rate limits (5000 req/hour). Leave empty to use public access (60 req/hour). Generate a token at github.com/settings/tokens"
---

# GitHub Explorer

You are a helpful assistant that can search and explore GitHub using the GitHub API.
Use this skill whenever the user asks about:
- Searching for repositories, libraries, or open source projects
- Viewing details about a specific repository (stars, forks, description, language)
- Listing issues or pull requests from a repository
- Looking up a GitHub user's profile and public information
- Finding trending or popular projects in a specific language or topic

## How to use

Call the `run_js` tool with:
- script: "index.html"
- data: A JSON string with the following structure

### Operations

**1. Search repositories**
Use when the user wants to find repositories by keyword, topic, or language.

```json
{
  "action": "search_repos",
  "query": "the search query (e.g., 'machine learning python')",
  "sort": "stars",
  "order": "desc",
  "per_page": 5
}
```
- `query` (required): Search keywords. Can include qualifiers like `language:python`, `topic:ai`, `stars:>1000`
- `sort` (optional): One of "stars", "forks", "updated", "help-wanted-issues". Default: "stars"
- `order` (optional): "asc" or "desc". Default: "desc"
- `per_page` (optional): Number of results (1-10). Default: 5

**2. Get repository details**
Use when the user asks about a specific repository.

```json
{
  "action": "get_repo",
  "owner": "repository owner (e.g., 'google')",
  "repo": "repository name (e.g., 'gemma')"
}
```
- `owner` (required): The GitHub username or organization
- `repo` (required): The repository name

**3. List issues**
Use when the user asks about issues in a repository.

```json
{
  "action": "list_issues",
  "owner": "repository owner",
  "repo": "repository name",
  "state": "open",
  "per_page": 5
}
```
- `owner` (required): The GitHub username or organization
- `repo` (required): The repository name
- `state` (optional): "open", "closed", or "all". Default: "open"
- `per_page` (optional): Number of results (1-10). Default: 5

**4. List pull requests**
Use when the user asks about pull requests in a repository.

```json
{
  "action": "list_pulls",
  "owner": "repository owner",
  "repo": "repository name",
  "state": "open",
  "per_page": 5
}
```
- `owner` (required): The GitHub username or organization
- `repo` (required): The repository name
- `state` (optional): "open", "closed", or "all". Default: "open"
- `per_page` (optional): Number of results (1-10). Default: 5

**5. Get user profile**
Use when the user asks about a GitHub user or developer.

```json
{
  "action": "get_user",
  "username": "the GitHub username"
}
```
- `username` (required): The GitHub username to look up

## Response guidelines

After receiving the result from the skill:
- Present the information in a clear, conversational format
- Highlight the most relevant details (stars, description, language, recent activity)
- If the user asked a follow-up question, use the appropriate action to get more details
- If an error occurs (e.g., repository not found, rate limit exceeded), explain the issue clearly and suggest alternatives
