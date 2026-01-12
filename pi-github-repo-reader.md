---
name: pi-github-repo-reader
description: Use pi to read GitHub repositories without cloning, replicating zread MCP functionality. Use for exploring repo structure, reading files, and searching code.
---

# PI + GitHub Repository Reading

This skill replicates the zread MCP server functionality using `pi` with GitHub API access.

## Prerequisites

Install GitHub CLI for best experience:
```bash
# macOS
brew install gh

# Linux
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

Authenticate (only needed for private repos):
```bash
gh auth login
```

---

## Tool 1: Get Repository Structure

**Purpose:** Get directory structure of a GitHub repo without cloning.

### Using gh CLI (Recommended)
```bash
pi -p "Use gh to get the directory structure of the facebook/react repository at the root level. Show me the tree structure with file types and sizes."
```

For specific subdirectory:
```bash
pi -p "Use gh to get the directory structure of facebook/react/src directory. Show me the complete tree structure."
```

### Using curl + GitHub API
```bash
pi -p "Use curl to query GitHub API for the contents of vercel/next.js repository root directory. Use the GitHub Contents API endpoint. Parse and display the results as a directory tree showing folders vs files."
```

### Prompt Template for Structure
```bash
pi -p "You are a GitHub repository explorer. Get the directory structure of [OWNER/REPO] repository at path [PATH - optional].

Use GitHub CLI (gh) or curl to query the GitHub Contents API:
- Endpoint: https://api.github.com/repos/[OWNER]/[REPO]/contents/[PATH]
- Or use: gh repo view [OWNER]/[REPO] --json name,path,contentType

Display the results as a clean directory tree showing:
1. Directory names with trailing /
2. File names with extensions
3. Indentation showing hierarchy
4. Total count of files and directories

Format: Use tree-like indentation with └── and ├── characters."
```

---

## Tool 2: Read File Contents

**Purpose:** Read full file contents from a GitHub repo without cloning.

### Using gh CLI (Recommended)
```bash
pi -p "Use gh to read and display the full contents of package.json from the facebook/react repository. Show the complete file content with proper formatting."
```

For specific path:
```bash
pi -p "Use gh to read the file src/components/Button.tsx from the facebook/react repository. Display the complete code with syntax highlighting preserved."
```

### Using curl + GitHub API
```bash
pi -p "Use curl to fetch and display the README.md file contents from the vercel/next.js GitHub repository via the GitHub API. Preserve all formatting, line breaks, and special characters."
```

### Prompt Template for Reading Files
```bash
pi -p "You are a GitHub file reader. Read and display the full contents of [FILE_PATH] from the [OWNER/REPO] repository.

Use one of these methods:
1. GitHub CLI: gh repo view [OWNER]/[REPO]:[FILE_PATH]
2. GitHub API: curl https://raw.githubusercontent.com/[OWNER]/[REPO]/main/[FILE_PATH]

Requirements:
- Display the COMPLETE file contents - do not truncate
- Preserve original formatting (indentation, line breaks)
- For code files: preserve syntax highlighting
- If file is very large (>1000 lines), show first 500 lines and note the size
- Include the file path and repository as a header

Output the full file content in a code block."
```

### Read from Specific Branch
```bash
pi -p "Use gh to read the file package.json from the facebook/react repository on the 'beta' branch. Use: gh repo view facebook/react:package.json --branch beta"
```

---

## Tool 3: Search Repository

**Purpose:** Search repository code, issues, docs, and commits.

### Search Code
```bash
pi -p "Search the facebook/react repository for 'useState' in the codebase. Use GitHub search API or gh search to find all files containing this term. Show file paths and relevant code snippets."
```

### Search for Function/Pattern
```bash
pi -p "Search the vercel/next.js repository for the implementation of 'getStaticProps' function. Use GitHub code search to find where this is defined and how it's used. Show the relevant code snippets with file paths."
```

### Search Issues
```bash
pi -p "Search for issues in the facebook/react repository related to 'useEffect cleanup'. Use gh to search issues and show the issue numbers, titles, and status."
```

### Search Commits
```bash
pi -p "Search commits in the vercel/next.js repository related to 'performance optimization'. Show commit hashes, authors, dates, and commit messages."
```

### Prompt Template for Searching
```bash
pi -p "You are a GitHub repository search expert. Search the [OWNER/REPO] repository for: [QUERY]

Use appropriate search method:
- Code search: gh search code --repo [OWNER/REPO] '[QUERY]'
- Issues search: gh search issues --repo [OWNER/REPO] '[QUERY]'
- Commits search: gh search commits --repo [OWNER/REPO] '[QUERY]'

Display results showing:
1. For code: file paths, language, and relevant snippets
2. For issues: issue number, title, status, and URL
3. For commits: hash, author, date, and message

Format results clearly with the most relevant matches first."
```

### Advanced Search with Filters
```bash
pi -p "Search the facebook/react repository for files matching the pattern '*.test.js' that contain 'useState'. Use GitHub code search with filename and content filters. Show matching files with line numbers."
```

---

## Combined Workflows

### Explore Then Read
```bash
# First explore structure
pi -p "Get the directory structure of vercel/next.js/packages/ directory using gh API."

# Then read a specific file
pi -p "Read the file packages/next/package.json from vercel/next.js repository using gh."
```

### Search Then Read
```bash
# First find the file
pi -p "Search vercel/next.js repository for files containing 'ImageOptimizer'. Show file paths and matches."

# Then read the implementation
pi -p "Read the file src/shared/lib/image-optimizer.ts from vercel/next.js repository using gh."
```

---

## Complete Prompt Reference

### get_repo_structure equivalent
```bash
pi -p "Use GitHub CLI (gh) or GitHub API to get the complete directory tree structure of [OWNER/REPO] at path [optional_path]. Display as a formatted tree with └── and ├── characters, showing directories with / suffix and file extensions."
```

### read_file equivalent
```bash
pi -p "Use GitHub CLI (gh) or GitHub raw content URL to read and display the COMPLETE contents of [FILE_PATH] from [OWNER/REPO] repository. Preserve all formatting, indentation, and special characters. Show the full file in a code block."
```

### search_doc equivalent (code search)
```bash
pi -p "Use GitHub search API or gh search code to find '[QUERY]' in the [OWNER/REPO] repository. Display matching file paths, line numbers if available, and relevant code snippets from the top 10 results."
```

### search_doc equivalent (issues)
```bash
pi -p "Use GitHub search API or gh search issues to find issues matching '[QUERY]' in the [OWNER/REPO] repository. Display issue numbers, titles, status (open/closed), and URLs."
```

### search_doc equivalent (commits)
```bash
pi -p "Use GitHub search API or gh search commits to find commits related to '[QUERY]' in the [OWNER/REPO] repository. Display commit hashes (short), authors, dates, and commit messages."
```

---

## GitHub API Endpoints Reference

For manual use or when gh is not available:

### Get Contents
```bash
# Directory listing
curl https://api.github.com/repos/OWNER/REPO/contents/PATH

# Raw file content
curl https://raw.githubusercontent.com/OWNER/REPO/BRANCH/PATH
```

### Search
```bash
# Code search
curl https://api.github.com/search/code?q=QUERY+repo:OWNER/REPO

# Issues search
curl https://api.github.com/search/issues?q=QUERY+repo:OWNER/REPO

# Commits search
curl https://api.github.com/search/commits?q=QUERY+repo:OWNER/REPO
```

---

## Quick Reference Table

| Task | Command Pattern |
|------|-----------------|
| Get repo structure | `pi -p "Use gh to get directory structure of OWNER/REPO at PATH..."` |
| Read file | `pi -p "Use gh to read FILE_PATH from OWNER/REPO..."` |
| Search code | `pi -p "Search OWNER/REPO for QUERY using gh search code..."` |
| Search issues | `pi -p "Search issues in OWNER/REPO for QUERY..."` |
| Search commits | `pi -p "Search commits in OWNER/REPO for QUERY..."` |

## Best Practices

1. **Use gh CLI**: It's faster and handles authentication better
2. **Specify repo format**: Always use `owner/repo` format (e.g., `facebook/react`)
3. **Explore first**: Use `get_repo_structure` before `read_file` to understand layout
4. **Specific queries**: For search, use specific terms for better results
5. **Public repos**: No authentication needed for public repositories
6. **Private repos**: Must authenticate with `gh auth login` first

## Notes

- zread MCP server makes API calls to GitHub, not prompts to a model
- This skill uses `pi` with bash/gh/curl to make the same API calls
- Works with both public and private GitHub repositories
- No need to clone the entire repository
