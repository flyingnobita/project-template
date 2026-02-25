# Specifications

Technical specifications for the project.

## Tech Stack

| Layer     | Technology                  | Notes |
| --------- | --------------------------- | ----- |
| Runtime   | (e.g. Node 20, Python 3.12) |       |
| Framework | (e.g. Next.js, FastAPI)     |       |
| Database  | (e.g. PostgreSQL, SQLite)   |       |

## Config & Credentials

### Config split

| File          | Contents                                   |
| ------------- | ------------------------------------------ |
| `.env`        | API keys, tokens, account identifiers only |
| `config.toml` | Paths, retention, log level                |

Secrets: env vars only, never in config.toml.

### Environment Variables (.env)

| Variable  | Required | Notes                    |
| --------- | -------- | ------------------------ |
| `EXAMPLE` | Yes      | Example API key or token |

### config.toml (paths, logging)

Profile-based sections: `[paths.<profile>]`, `[logging.<profile>]`.

| Setting         | Choice                       |
| --------------- | ---------------------------- |
| Default profile | `profile = "dev"` (or omit)  |
| Override        | `APP_PROFILE` or `--profile` |

Example: `[paths.dev]` has `db_path`, `[logging.dev]` has `level`,
`retention_days`.

## Project Structure

The following is an example structure. Adapt for your stack (e.g. Go uses
`cmd/`, `internal/`; Next.js uses `app/`, `pages/`).

```text
# Add your project structure
src/
├── config/          # .env + config.toml loading and validation
├── db/              # libSQL connection, schema, queries
├── logging/         # Logging setup and utilities
└── ...
```

## Logging

| Setting      | Choice                                                                    |
| ------------ | ------------------------------------------------------------------------- |
| Location     | `logs/` folder                                                            |
| Filename     | `app.log`                                                                 |
| Format       | Human-readable: `%(asctime)s - %(name)s - %(levelname)s - %(message)s`    |
| Timestamp    | ISO 8601: `%Y-%m-%dT%H:%M:%S`                                             |
| Rotation     | `TimedRotatingFileHandler`, daily at midnight                             |
| Backup count | 14 days (configurable via config.toml `logging.<profile>.retention_days`) |
| Output       | File + console (both)                                                     |

## Tooling

| Decision        | Choice                     |
| --------------- | -------------------------- |
| Package manager | mise, npm, cargo, go mod   |
| Test framework  | (pytest, jest, cargo test) |
| Formatter       | prettier                   |
| Type Checker    | (mypy)                     |
| Linter          | markdownlint-cli2(md)      |
| CI              | GitHub Actions             |

### Line endings (cross-platform)

LF in repo. `.gitattributes` (`* text=auto eol=lf`) normalizes; Git converts for
Windows. `.editorconfig` enforces `end_of_line = lf`.
