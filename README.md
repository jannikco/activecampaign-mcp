# ActiveCampaign MCP server

Find existing marketing contacts and create a new contact record without changing subscriptions.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ACTIVECAMPAIGN_API_KEY`
- `ACTIVECAMPAIGN_HOST`



Credential help: https://developers.activecampaign.com/reference/authentication

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call activecampaign_list_contacts '{"limit":5}'
```

## Use with an MCP client

Launch `node /absolute/path/activecampaign-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| activecampaign_list_contacts | Read | activecampaign list contacts |
| activecampaign_create_contact | Explicit approval required | activecampaign create contact |

## Concrete workflow

Find existing marketing contacts and create a new contact record without changing subscriptions.

1. activecampaign_list_contacts
2. activecampaign_create_contact

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Import with PipMCP](https://pipmcp.com/github/start?integration=openapi-to-mcp&utm_source=github&utm_campaign=github-activecampaign-mcp&utm_content=readme) when you want the hosted service. This provider is not currently listed as a managed template. Import selected-openapi.json (REST) or the official GraphQL schema linked in provenance, configure authentication, and review the tools before execution. Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/activecampaign/).

## Provenance and maintenance

- https://developers.activecampaign.com/reference/list-all-contacts
- https://developers.activecampaign.com/reference/create-a-new-contact

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
