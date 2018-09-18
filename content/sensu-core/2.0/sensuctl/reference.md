---
title: "Sensuctl Reference"
linkTitle: "Reference"
description: "Complete reference docs for sensuctl commands"
weight: 10
version: "2.0"
product: "Sensu Core"
platformContent: false
menu:
  sensu-core-2.0:
    parent: sensuctl
---

## Create

The `sensuctl create` command allows you to create and/or
update resources by reading from STDIN or a flag configured file (`-f`). The
accepted format of the `create` command is `wrapped-json`, which wraps the
contents of the resource in `spec` and identifies its 2.x `type` (see below for
an example, and [this table][2] for a list of supported types).

{{< highlight shell >}}
{
  "type": "CheckConfig",
  "spec": {
    "name": "marketing-site",
    "command": "check-http.rb -u https://dean-learner.book",
    "subscriptions": ["demo"],
    "interval": 15,
    "handlers": ["slack"],
    "organization": "default",
    "environment": "default"
   }
}
{
  "type": "Handler",
  "spec": {
    "name": "slack",
    "type": "pipe",
    "command": "handler-slack --webhook-url https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX --channel monitoring'",
    "environment": "default",
    "organization": "default"
  }
}
{{< /highlight >}}

Write all checks to `my-resources.json` in `wrapped-json` format:
{{< highlight shell >}}
sensuctl check list --format wrapped-json > my-resources.json
{{< /highlight >}}

Create all resources in `wrapped-json` format from `my-resources.json`:
{{< highlight shell >}}
cat my-resources.json | sensuctl create
{{< /highlight >}}

### Supported types

|wrapped-json types |   |   |   |
--------------------|---|---|---|
`AdhocRequest` | `adhoc_request` | `Asset` | `asset`
`Check` | `check` | `CheckConfig` | `check_config`
`Entity` | `entity` | `Environment` | `environment`
`Event` | `event` | `EventFilter` | `event_filter`
`Extension` | `extension` | `Handler` | `handler`
`Hook` | `hook` | `HookConfig` | `hook_config`
`Mutator` | `mutator` | `Organization` | `organization`
`Role` | `role` | `Silenced` | `silenced`