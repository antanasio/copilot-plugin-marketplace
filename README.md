# Copilot plugin marketplace

A **GitHub Copilot CLI plugin marketplace** containing one plugin, **`github-dev-toolkit`** (4 skills, 1 agent, 3 hooks, GitHub MCP server).

```
copilot-plugin-marketplace/
├── .github/
│   └── plugin/marketplace.json        # marketplace catalog
├── plugins/
│   └── github-dev-toolkit/
│       ├── plugin.json                # plugin manifest
│       ├── .mcp.json                  # GitHub MCP server (github.com)
│       ├── hooks.json                 # sessionStart / preToolUse / postToolUse
│       ├── hooks/scripts/*.js         # cross-platform Node hook scripts
│       ├── agents/github-maintainer.agent.md
│       ├── skills/
│       │   ├── github-pr-review/SKILL.md
│       │   ├── github-issue-triage/SKILL.md
│       │   ├── github-release-notes/SKILL.md
│       │   └── conventional-commits/SKILL.md
│       ├── README.md  CHANGELOG.md  LICENSE
├── scripts/validate.js                # manifest + skill + hook validation
└── tests/hooks.test.js                # hook smoke tests
```

## Test locally
```bash
node scripts/validate.js
node tests/hooks.test.js
copilot plugin install ./plugins/github-dev-toolkit
copilot            # then: /plugin list, /skills list, /agent, /mcp
```
Re-run `copilot plugin install ./plugins/github-dev-toolkit` after each change (installed plugins are cached).

## Install from the marketplace
```bash
copilot plugin marketplace add antanasio/copilot-plugin-marketplace
copilot plugin marketplace browse antanasio-copilot-plugins
copilot plugin install github-dev-toolkit@antanasio-copilot-plugins
```

To also appear in a community marketplace such as `github/awesome-copilot`, submit a separate contribution there and follow its contribution guidelines.

## Releasing updates
1. Bump the version in `plugin.json` and the marketplace catalog, and update `CHANGELOG.md`.
2. Run `node scripts/validate.js` and `node tests/hooks.test.js`.
3. Push the changes. Users can run `copilot plugin marketplace update antanasio-copilot-plugins` to refresh the catalog and `copilot plugin update github-dev-toolkit` to update the plugin.
