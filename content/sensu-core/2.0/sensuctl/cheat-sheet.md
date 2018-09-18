---
title: "Sensuctl Cheat Sheet"
linkTitle: "Cheat Sheet"
description: "Quick reference for sensuctl commands"
weight: 5
version: "2.0"
product: "Sensu Core"
platformContent: false
menu:
  sensu-core-2.0:
    parent: sensuctl
---

### Getting started

{{< highlight shell >}}
# What am I monitoring?
sensuctl entity list

# What checks am I running?
sensuctl check list

# What events are entering the pipeline?
sensuctl event list
{{< /highlight >}}

### Creating event pipelines

{{< highlight shell >}}
# Create a filter using the command line
sensuctl filter create --interactive

# Create a mutator using the command line
sensuctl mutator create --interactive

# Create a handler using the command line
sensuctl handler create --interactive
{{< /highlight >}}

### Automating event production with the Sensu agent

{{< highlight shell >}}
# Create a check using the command line
sensuctl check create --interactive
{{< /highlight >}}

### Getting help

{{< highlight shell >}}
# See all sensuctl commands
sensuctl -h

# See all subcommands
sensuctl {entity, event, check} -h

# See usage conventions for a subcommand
sensuctl {entity, event, check} {list, info, create} -h
{{< /highlight >}}

