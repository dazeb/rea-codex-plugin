# REA for Codex

Local plugin packaging for [REA by morluto](https://github.com/morluto/rea).
Plugin version: 0.1.0. Upstream server and bundled skill: rea-agents 6.3.0.
This wrapper is maintained by dazeb and is not an official upstream release.

## Runtime

The MCP server starts with `npx -y rea-agents@6.3.0 mcp` over stdio.
The first start downloads the pinned npm package if it is not already cached.
Node.js must satisfy the upstream engine requirement:
`^22.19.0 || ^24.11.0 || >=26.0.0`.

JavaScript and Electron static inspection needs no native analysis engine.
Native decompilation needs an existing supported Ghidra, Hopper, or IDA setup.
Android and firmware workflows have additional upstream prerequisites.
The plugin does not install those engines.

## Using the plugin

Enable REA in Codex, then reconnect or start a new chat if its tools are not
visible. Supply an application, package, binary, or a specific runtime target
and ask what to investigate. The bundled skill selects the appropriate tools
and requires conclusions to cite evidence and state limitations.

The plugin's MCP configuration provides the server connection. Do not also
register the same server through standalone REA setup merely to use this plugin.
An account copy of this package still needs a host that supports local stdio
servers and access to the requested files or processes.

## Upstream Material

`skills/reverse-engineer-anything/` and `LICENSE` come unchanged from the
published rea-agents 6.3.0 npm package. `assets/rea.svg` is REA's upstream favicon,
with explicit 128-pixel dimensions added for plugin presentation, retrieved at
repository commit `46c9cba03a52b8ec382a686cd70ded6128225db8`.

`plugin.json` is the portable Agent Plugins manifest.
`.codex-plugin/plugin.json` supplies the matching Codex compatibility manifest.
