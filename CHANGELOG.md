## [0.3.0] - 2026-11-19

### ⚙️ Miscellaneous Tasks

- *(prek)* Label hook names by source

### 📚 Documentation

- Add AGENTS.md and mise/prek guidelines, update README
- Explain how consumers reuse hooks via the manifest
- Move guidelines under docs/guidelines
- *(glossary)* Define core shared-dev-tooling terms

### 🚀 Features

- *(tasks)* [**breaking**] Name tasks <tool>:<verb> and tag them by purpose
- *(prek)* Publish hook manifest wrapping shared mise tasks
- *(tooling)* Add shell lint hooks and release:cut task

### 🐛 Bug Fixes

- *(prek)* Align local hook file filters with the published manifest
- *(tasks)* Limit mise:outdated to project tools
- *(changelog)* Skip release commits and keep parser order

### 🚜 Refactor

- *(tasks)* Group task files into category subfolders
- *(prek)* Run local hooks through shared mise tasks
- *(tasks)* Name task files <tool>.tasks.toml
## [0.2.0] - 2026-11-19

### ⚙️ Miscellaneous Tasks

- *(tasks)* Move git-cliff and prek tasks into tasks/
- *(taplo)* Add taplo to autoformat TOML configuration
- *(toml)* Format TOML configuration with taplo

### 🚀 Features

- *(prek)* Check mise.lock consistency
- *(mise)* Add maintenance task group
- *(prek)* Validate mise tasks

### 🐛 Bug Fixes

- *(prek)* Run taplo hooks via repo-pinned binary
## [0.1.0] - 2026-11-19

### ⚙️ Miscellaneous Tasks

- Initial commit
- *(gitignore)* Compose ignore rules from upstream templates
- *(editorconfig)* Add cross-language formatting defaults
- *(gitattributes)* Normalize line endings and mark binaries
- *(prek)* Configure prek hooks with cooldown and priorities
- *(changelog)* Setup git-cliff changelog generation
- *(mise)* Enforce min release date and lockfile usage, min version

### 📚 Documentation

- *(readme)* Describe shared task scope and usage

### 🚀 Features

- *(hooks)* Add prek install and run tasks
