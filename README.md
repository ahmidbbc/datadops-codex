# DatadOps Codex Plugin

DatadOps is a Codex plugin built on top of the Datadog MCP server.

It provides reusable operational workflows for:
- service health overviews
- incident response
- performance investigations
- deployment health checks

## Plugin location

The actual plugin package lives in:

```text
plugins/datadops
```

## Included workflows

- `@service-health-overview`
- `@incident-response`
- `@performance-investigation`
- `@deployment-health-check`

## Demo

Watch the plugin in action on GitHub:


Preview:

![DatadOps demo teaser](./plugins/datadops/assets/datadops-demo-teaser.gif)

## Repository contents

```text
plugins/datadops/
  .codex-plugin/plugin.json
  .mcp.json
  assets/
  skills/
  README.md
  PRIVACY.md
  TERMS.md
```

## Documentation

For plugin-specific installation, usage, and limitations, see:

- [Plugin README](./plugins/datadops/README.md)
- [Privacy Policy](./plugins/datadops/PRIVACY.md)
- [Terms of Use](./plugins/datadops/TERMS.md)
