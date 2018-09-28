---
title: "Using GitHub for RBAC in Sensu Enterprise"
linkTitle: "GitHub for RBAC"
product: "Sensu Enterprise Dashboard"
version: "2.9"
weight: 1
menu:
  sensu-enterprise-dashboard-2.9:
    parent: guides
---

In this guide, we'll cover configuring and using the Sensu Enterprise Dashboard GitHub RBAC.

- [Prerequisites](#prerequisites)
  - [GitHub Organization Creation and Configuration](#github-organization-creation-and-configuration)
  - [Sensu Enterprise Dashboard Configuration](#sensu-enterprise-dashboard-configuration)
  - [Testing the Configuration](#testing-the-configuration)
  - [Wrapping It Up](#wrapping-it-up)
  - [References](#references)

## Prerequisites

Before diving into this guide, we recommend having the following components ready:

- A working Sensu Enterprise deployment with Sensu Enterprise Dashboard
- A GitHub [account][1]

## GitHub Organization Creation and Configuration

1.) If you don't already have an organization, go to https://github.com/settings/organizations and create an one.

2.) Once created or if using an already made one, go to https://github.com/organizations/<myOrganization>/settings/applications, replacing <myOrganization> with the name or the organization. 

3.) Select "New OAuth App"

4.) Name your application, Homepage URL will be the Sensu Enterprise Dashboard location

http://sensuenterpriseclassic:3000

Authorization callback URL will be

http://sensuenterpriseclassic:3000/login/callback

5.) Once created, make note of the Client ID and Client Secret. They will be used in the Sensu Enterprise Dasbhoard configuration later.

6.) Add teams that you would like access to the Sensu Enterprise Dashboard

https://github.com/<myOrganization>/myTestingg/teams

<add picture of Client ID and Client Secret>

## Sensu Enterprise Dashboard Configuration

1.) On the server running Sensu Enterprise Dashboard, inside `/etc/sensu/dashboard.json`, add the following object to the `dashboard` hash where the `clientId` and `clientSecret` arrtibutes need to be modified, as well as the `roles` hash

{{< highlight json >}}
{
  "dashboard": {
    "...": "...",
    "github": {
      "clientId": "18b4d5db4d30e4af49f8",
      "clientSecret": "93b1170f171d4ff7d55dee03c293ac540c25a98d",
      "server": "https://github.com",
      "roles": [
        {
          "name": "myTeam",
          "members": [
            "myOrganizaton/myTeam"
          ]
        }
      ]
    }
  }
}
{{< /highlight >}}

## Testing the Configuration

Attempt to log into the Sensu Enterprise Dashboard using credentials for a user that is a team member within the Organization created earlier or already made, that has the OAuth `clientId` and `clientSecret` associated with it.

http://sensuenterpriseclassic:3000

## Wrapping It Up

## References

- [RBAC for GitHub reference][7]
- [GitHub Organizations][8]

<!-- LINKS -->
[1]: https://github.com/
[7]: ../../rbac/rbac-for-gitlab/
[8]: https://help.github.com/articles/creating-a-new-organization-from-scratch/