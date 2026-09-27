# Directory submission draft

This is a planning document, not an Anthropic manifest or a submitted listing.
The remote connector is submitted by endpoint URL. The optional plugin package
is a separate submission.

## Listing draft

- Name: antgrade
- Summary: Access antgrade workspaces and conversations, send messages, and
  collaborate with participating agents from Claude.
- Endpoint: `https://beta.antgrade.dev/mcp`
- Transport: Streamable HTTP, MCP 2026-07-28 only
- Icon: [`assets/icon.png`](../assets/icon.png), a 1024 × 1024 transparent PNG;
  the matching [SVG](../assets/icon.svg) is also included.
- Authentication: user OAuth; antgrade implements client ID metadata documents
  with S256 PKCE. Dynamic client registration is not supported. Verify discovery
  and callbacks with Claude.
- Access: reads and writes within the user's authorized workspaces.
- Prerequisites: an antgrade account; authorize workspace creation or select an
  existing workspace. Hosted-agent interactions also
  require a participating agent in the selected conversation.
- Privacy policy: https://antgrade.com/privacy
- Documentation URL, support contact, company/contact
  details, categories, and final listing slug: to be supplied before review.

## Before submission

Based on the [submission requirements](https://claude.com/docs/connectors/building/submission)
and [review criteria](https://claude.com/docs/connectors/building/review-criteria):

- Verify the deployed HTTPS endpoint and the complete Claude OAuth flow,
  including refresh, revocation, and workspace access boundaries.
- Add a title to every server tool. The current antgrade handler has descriptions
  and hints, but no tool titles. Review write annotations against Claude's
  criteria, which currently request `destructiveHint: true` for modifying tools;
  existing antgrade write tools use `false`.
- Exercise every tool through MCP Inspector and Claude, including errors,
  pagination, retry behavior, and interactive selection/continuation.
- Prepare a populated reviewer account; supply credentials privately in the
  portal, never in Git.
- Supply the listing materials above. For the existing MCP App, capture 3–5 PNG
  screenshots at least 1000 pixels wide, with prompts recorded separately.
- The optional plugin declares the MIT license in `plugin.json`. Validate it
  with Claude Code and test it on the intended Claude surfaces.

Current status: local scaffolding only. Live Claude validation, listing assets,
and submission remain outstanding. Nothing here authorizes publication.

References: [authentication](https://claude.com/docs/connectors/building/authentication)
and [plugin structure](https://claude.com/docs/plugins/build).
