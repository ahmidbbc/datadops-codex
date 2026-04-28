# DatadOps for Codex

DatadOps is a Codex plugin that packages reusable Datadog investigation workflows on top of the official Datadog MCP server.

It keeps the original plugin name `datadops` and provides four operational skills:
- `@service-health-overview`
- `@incident-response`
- `@performance-investigation`
- `@deployment-health-check`

## What it adds

The Datadog MCP server exposes raw observability data. DatadOps turns that data into repeatable workflows for common operational tasks:
- fast service health checks
- structured incident investigation
- performance bottleneck analysis
- deployment validation and rollback guidance

## Requirements

This plugin expects the Datadog MCP server to be available through the bundled `.mcp.json` configuration.

Bundled MCP server:
- `datadog` via `https://mcp.datadoghq.com/api/unstable/mcp-server/mcp?toolsets=core,apm,alerting`

You may be prompted to authenticate with Datadog the first time Codex uses the server, depending on your Codex setup.

Datadog currently documents its MCP server as under active development, and the official remote endpoint still uses the `/api/unstable/` path. This plugin keeps that official endpoint but limits the enabled toolsets to the ones the packaged skills actually use: `core`, `apm`, and `alerting`.

## Public Distribution

This plugin is packaged as a standard Codex plugin directory:

```text
plugins/datadops/
  .codex-plugin/plugin.json
  .mcp.json
  skills/
  assets/
  README.md
  PRIVACY.md
  TERMS.md
```

For a public release, publish this directory in a public repository and keep the metadata in `.codex-plugin/plugin.json` aligned with the final repository URL.

## Local Development

For local testing, you can register the plugin in a home-local Codex marketplace.

The local marketplace entry points to:
- `~/.agents/plugins/marketplace.json`
- `~/plugins/datadops`

## Example prompts

```text
Use @service-health-overview to summarize the health of our production services.
```

```text
Use @incident-response to investigate why the payment service is returning 500 errors.
```

```text
Use @performance-investigation to find the bottleneck in checkout latency.
```

```text
Use @deployment-health-check to validate checkout-service version 2.1.4 in production.
```

## Example output

Below is the kind of response DatadOps is designed to produce after using Datadog data through the MCP server:

```text
Service: checkout-service
Environment: production
Overall status: Warning

Key signals
- Error rate increased from 0.4% to 2.1% in the last 30 minutes
- P95 latency increased from 420ms to 780ms after the latest deployment
- No infrastructure saturation detected on hosts or containers

Likely contributors
- Elevated 5xx responses on /api/checkout/submit
- Trace samples show longer downstream payment-provider calls
- Recent deployment event correlates with the first latency spike

Recommended next steps
1. Inspect failed traces for checkout submit requests
2. Compare application logs before and after the deployment window
3. Consider rollback if error rate remains above the service threshold
```

## Known limitations

### OAuth and Datadog organization switching

When Datadog access is configured through OAuth, the active MCP session is scoped to the currently connected Datadog organization.

In that setup, environment filters such as `env:preprod` or `env:prod` only narrow data inside the current Datadog organization. They do not switch the underlying OAuth connection or move the plugin to another Datadog organization.

As a result, DatadOps cannot currently force a disconnect or reconnect of the Datadog MCP session from inside a workflow. If a user needs to investigate a different Datadog organization, the MCP connection must be changed outside the plugin through Codex or MCP session management.

## Source layout

```text
.codex-plugin/plugin.json
.mcp.json
skills/
assets/
README.md
PRIVACY.md
TERMS.md
