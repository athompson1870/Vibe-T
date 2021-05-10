# vibe-tools

CLI tools for AI agents. Execute commands and collaborate with other AI agents from the terminal.

- **Teammates** — Commands you can ask questions (e.g. `repo`, `web`, `ask`)
- **Skills** — Commands that perform tasks (e.g. `browser`, `plan`, `doc`)

All commands return a result (no long-running processes).

## Requirements

- Node.js >= 18
- [pnpm](https://pnpm.io/) (recommended for development)

## Installation

```bash
# Global install (recommended for use by AI agents)
pnpm add -g vibe-tools
# or
npm install -g vibe-tools
```

## Usage

```bash
vibe-tools <command> [query] [options]
```

### Commands

| Command   | Description |
|----------|-------------|
| `ask`    | Ask any model a direct question |
| `web`    | Web search / answers from the internet (Perplexity, Gemini, etc.) |
| `repo`   | Context-aware answers about this (or a GitHub) repo |
| `plan`   | Generate an implementation plan using AI |
| `doc`    | Generate documentation for a repository |
| `browser`| Browser automation (open, act, observe, extract) via Stagehand |
| `github` | PR and issue info |
| `mcp`    | Run MCP server tools via natural language |
| `youtube`| Analyze YouTube videos (summary, transcript, plan, etc.) |
| `clickup`| ClickUp task details |
| `linear` | Linear integration |
| `xcode`  | Build, run, and lint Xcode projects |
| `wait`   | Pause for N seconds |

### Examples

```bash
vibe-tools web "latest shadcn/ui installation instructions"
vibe-tools repo "explain the authentication flow" --subdir=src
vibe-tools plan "Add user authentication to the login page"
vibe-tools doc --output docs.md
vibe-tools browser open "https://example.com" --html
vibe-tools ask "What is the capital of France?" --provider openai --model gpt-4o
```

### Common options (many commands)

- `--provider=<provider>` — openai, anthropic, perplexity, gemini, openrouter, modelbox, xai, groq
- `--model=<model>` — Override default model
- `--save-to=<path>` — Save output to a file
- `--with-doc=<url>` — Include content from URL(s) as context (use for specific docs/URLs instead of `web`)
- `--debug` — Verbose logs

## Configuration

- **Config:** `vibe-tools.config.json` (project or `~/.vibe-tools/config.json`)
- **Secrets:** `.vibe-tools.env` or `~/.vibe-tools/.env` (API keys)

API keys are also read from environment variables and (when configured) Doppler.

## Development

This repo uses **pnpm** as the package manager and script runner.

```bash
# Install dependencies
pnpm install

# Run commands with latest source (no build)
pnpm dev <command> [query] [options]

# Examples
pnpm dev web "test query"
pnpm dev repo "explain src structure"
pnpm dev browser open "https://example.com"

# Build for release
pnpm run compile
pnpm run build

# Lint and format
pnpm run lint
```

### Browser command testing

1. Start test server: `pnpm serve-test` (runs in background at http://localhost:3000)
2. Add test HTML under `tests/commands/browser/`
3. Run: `pnpm dev browser <subcommand> ...`
