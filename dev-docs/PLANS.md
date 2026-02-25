# Build Plan

Suggested implementation order.

## Build Order

1. **Project scaffolding**
   - Package config (pyproject.toml, package.json, Cargo.toml, go.mod)
   - Tool config (mise.toml)
   - Source layout
   - `.env.example` (API keys only)
   - `config.toml.example` (paths, logging, profiles)

2. **Core setup**
   - Config loading (.env + config.toml, profile support)
   - Logging (if needed)

3. **Feature implementation**
   - Add features in dependency order

4. **Tests & CI**
   - Unit tests
     - GitHub Actions workflow

5. **Documentation**
   - README
   - Usage examples
