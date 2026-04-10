# renovate-config

Shared [Renovate Bot](https://docs.renovatebot.com/) configuration presets for
all repos in the [Beeping](https://github.com/beeping-io) ecosystem.

## Usage

Add a `renovate.json` to your repo root:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>beeping-io/renovate-config"]
}
```

### Ecosystem-specific presets

For repos that target a specific language/framework, extend the variant instead:

| Preset | Repos | Extra rules |
|---|---|---|
| `github>beeping-io/renovate-config:flutter` | `beeply`, `beeping_flutter` | pub manager, Firebase grouping, SDK pin |
| `github>beeping-io/renovate-config:cpp` | `beeping-core` | CMake/vcpkg, no automerge (ABI check) |
| `github>beeping-io/renovate-config:node` | `beeping-web`, `beeping-node`, `portal`, `www` | npm, Next.js/React grouping, Tailwind grouping |
| `github>beeping-io/renovate-config:python` | `beeping-python` | pip/poetry, pytest grouping |
| `github>beeping-io/renovate-config:rust` | `beeping-cli` | Cargo, serde/tokio grouping |

Example for a Flutter repo:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>beeping-io/renovate-config:flutter"]
}
```

## What the default preset does

- **Schedule**: runs early Monday mornings (`before 6am on monday`)
- **Automerge**: minor and patch updates (not major)
- **Grouping**: `@types/*`, testing tools, lint/format tools
- **Concurrency**: max 5 PRs open, max 3 PRs/hour
- **Vulnerability alerts**: always enabled, bypass schedule
- **Lock file maintenance**: weekly
- **Semantic commits**: PR titles follow Conventional Commits (`chore(deps): ...`)
- **Dependency dashboard**: issue tracking all pending updates

## Validation

CI runs [`renovate-config-validator`](https://docs.renovatebot.com/config-validation/)
on every push and PR to ensure presets are valid.

## License

[Apache-2.0](LICENSE)
