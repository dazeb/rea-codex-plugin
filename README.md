# REA for Codex

A standalone Codex plugin marketplace for [REA by morluto](https://github.com/morluto/rea), maintained by [dazeb](https://github.com/dazeb).

The plugin provides an investigation skill and a local MCP connection for inspecting applications, managed assemblies, native binaries, JavaScript/Electron applications, packages, firmware and supported runtime evidence. It is a Codex integration wrapper, not a fork of the REA analysis engine or an official upstream release.

| Component | Version |
| --- | --- |
| Plugin | `0.1.0` |
| REA MCP server | `rea-agents@6.3.0` |

## Install in Codex

With a Codex CLI that supports plugin marketplaces:

```sh
codex plugin marketplace add dazeb/rea-codex-plugin --ref main
codex plugin add rea@rea-codex-plugin
```

Private repositories require GitHub access for the Git transport used by Codex. Alternatively, clone the repository and register the local checkout:

```sh
git clone https://github.com/dazeb/rea-codex-plugin.git
codex plugin marketplace add ./rea-codex-plugin
codex plugin add rea@rea-codex-plugin
```

Reconnect Codex or start a new chat if the tools are not visible. If REA is already installed through another marketplace, use one installation to avoid duplicate server connections. This repository does not modify your current installation automatically.

## Requirements

- A Codex host that supports local stdio MCP servers.
- Node.js and npm, including `npx`. The packaged upstream runtime requirement is `^22.19.0 || ^24.11.0 || >=26.0.0`.
- Access to the local files or processes you want to inspect.
- Workflow-specific analysis tools: native decompilation needs a supported existing Ghidra, Hopper or IDA setup; Android and firmware workflows have separate prerequisites. The plugin does not install these tools.

The server command is pinned in [`plugins/rea/mcp.json`](plugins/rea/mcp.json):

```sh
npx -y rea-agents@6.3.0 mcp
```

The first start downloads the npm package if it is not already cached. JavaScript/Electron static analysis does not need a native decompiler. Local stdio tools require a local host; publishing these files does not provision a hosted analysis service.

## Use

Select REA in Codex and supply a concrete target and question, for example:

- Inspect this application and explain how its features work.
- Compare these two releases and show the evidence for changes.
- Analyze this binary and explain its important functions.

The investigation skill chooses a tool according to the target, follows features through their relevant code and state, and requires findings to distinguish observations, inferences and unknowns. Complete source repositories can be analyzed with normal source tools; binary decompilation is used where artifact evidence is needed.

## Repository layout

```text
.agents/plugins/marketplace.json   Codex marketplace entry
plugins/rea/
  plugin.json                    Portable Agent Plugins manifest
  .codex-plugin/plugin.json       Codex compatibility manifest
  mcp.json                       Pinned local MCP server command
  skills/reverse-engineer-anything/
    SKILL.md                     Investigation instructions
    references/                  Workflow guides
  assets/rea.svg                 Plugin icon
  README.md                     Original plugin documentation
  LICENSE                       Upstream MIT license
```

The plugin files are copied unchanged from the original local `0.1.0` source. Repository documentation and the marketplace entry are added around that package. The original local plugin and installed cache are preserved.

## Attribution and license

REA is developed by **morluto**. The bundled skill, workflow references and license come from the published `rea-agents@6.3.0` package. The icon is the upstream favicon, with explicit 128-pixel dimensions added for presentation, obtained at commit `46c9cba03a52b8ec382a686cd70ded6128225db8`.

See the retained [MIT license](LICENSE) and [plugin attribution](plugins/rea/README.md). The REA server itself is fetched from npm rather than vendored into this repository.
