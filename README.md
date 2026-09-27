# Antgrade for Claude

![Antgrade icon](assets/icon.svg)

Local, unpublished connector package for accessing Antgrade workspaces,
conversations, messages, and participating agents from Claude.

## Structure

Claude's [connector directory](https://claude.com/docs/connectors/directory)
lists hosted MCP servers. The remote connector is Antgrade's existing
`https://beta.antgrade.dev/mcp` endpoint; a repository is not itself a running
connector or a directory submission.

This repository also packages that endpoint using Claude's
[plugin layout](https://claude.com/docs/plugins/build):

```text
.claude-plugin/plugin.json  Plugin identity and description
.mcp.json                   Remote MCP connection, without credentials
assets/icon.svg             Square Antgrade symbol
assets/icon.png             1024 × 1024 transparent icon for directory submission
docs/submission.md          Draft listing and outstanding submission work
README.md                  Setup and development notes
```

There is no build step or dependency installation. The server and OAuth
implementation remain in the containing shokunin repository at
`apps/antgrade/src/mcp/` and `apps/antgrade/src/auth/`. Changes to tools, permissions,
or interactive views belong there. This repository owns the Claude package and
listing materials.

## Connect during development

The connector currently targets the beta deployment at `https://beta.antgrade.dev/mcp`.
This configuration does not establish that the service has been tested in Claude.

With Claude Code already installed, run from this repository:

```sh
claude plugin validate .
claude --plugin-dir .
```

Use `/mcp` to connect and complete Antgrade's OAuth sign-in. For claude.ai or
Claude Desktop, add the HTTPS endpoint as a custom connector and sign in with
an Antgrade account. Select only the workspaces you want to authorize.
For a private deployment, change the URL in your working copy to its HTTPS
`/mcp` endpoint. Claude's hosted client must be able to reach it.

Try listing your workspaces, reading a conversation, or explicitly requesting a
message be sent to a selected conversation. Hosted-agent operations require an
available participating agent. The MCP App provides interactive selections.
Revoke access in Antgrade under Account → Security → Connected apps.

Clients must support MCP 2026-07-28 per-request discovery and metadata. Legacy
initialize handshakes are rejected; verify support in the target Claude client.

OAuth discovery starts at
`/.well-known/oauth-protected-resource/mcp`, with authorization-server
metadata at `/.well-known/oauth-authorization-server` on the same origin.
Use the MCP resource audience, not the separate REST API audience. Keep tokens,
reviewer credentials, and client secrets out of this repository.

## Branding

`assets/icon.svg` and `assets/icon.png` reuse the square vermilion symbol from
`brands/antgrade/logo/antgrade-symbol-vermilion.*` in shokunin. Update both copies
when the brand source changes. The PNG is 1024 × 1024 with a transparent background.
Use it for the icon field in Claude's connector submission portal; it has not been
uploaded automatically.

Antgrade advertises the SVG through its MCP server metadata at
`https://beta.antgrade.dev/brand/icon.svg`. Hosts decide whether to display MCP
icons. The Claude plugin manifest has no documented icon field.

## Local Git submodule

This is an independent Git repository on `main`, tracked by shokunin at
`connectors/antgrade-claude`. Its initial commit is local, with no publishing
remote. The submodule URL points at this local checkout and is intentionally
machine-specific; another machine cannot initialize it from that URL.

Commit connector changes here before staging the updated gitlink in shokunin.
When publication is explicitly requested, create its remote, push this history,
replace the local URL in shokunin's `.gitmodules`, and run `git submodule sync`.

## Publication status

No repository, plugin, or directory listing has been published. No license has
been selected. See [submission notes](docs/submission.md) for the remaining work;
the scaffold does not establish Claude compatibility or directory acceptance.
