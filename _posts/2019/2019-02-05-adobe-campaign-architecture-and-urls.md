---
title: "Adobe Campaign: Software Architecture, URLs, and Image Management"
categories: [opensource,adobe campaign,devops]
---

<p class="text-center">☕🖥️🌐</p>

Software architecture of Adobe Campaign, directory organization, server configuration (Tomcat/Apache), and management of URLs and static resources (images, XSL, JSP). This guide is ideal for system administrators and developers working with Adobe Campaign Classic deployments.

<!--more-->

## Introduction

Adobe Campaign Classic is built on a **Java EE architecture**, typically deployed with **Tomcat** (port 8080) or integrated with a web server like **Apache** (ports 80/443). This article covers:
- Directory structure and configuration files.
- Server configuration (Tomcat/Apache).
- URL mapping and static resource management (images, XSL, JSP).
- Common use cases and troubleshooting tips.

Notes for Apache: 
- See [INS_Installing_Campaign_in_Linux__Integration_into_a_Web_server](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Linux__Integration_into_a_Web_server.html)

## Installation directory

By default, Adobe Campaign is installed under the `neolane` user. To verify the home directory:
```console
$ cat /etc/passwd | grep neolane
neolane:x:1001:1001::/usr/local/neolane:/bin/bash
```

For this guide, we assume Adobe Campaign is installed in:

```console
/usr/local/neolane/nl6/
```

(Referred to as / in the following sections.)

## Adobe Campaign Namespaces

In Adobe Campaign, **namespaces** are prefixes used to organize schemas, tables, and APIs. They help avoid naming conflicts and logically group related functionalities. Below are the core namespaces and their purposes.

### `NMS`: Neolane Marketing Server

Covers **marketing-related schemas and tables**, such as:
- **Recipients** (`nms:recipient`): The main table for storing customer profiles.
- **Deliveries** (`nms:delivery`): Tables for email, SMS, and other campaign deliveries.
- **Campaigns** (`nms:operation`): Tables for managing marketing campaigns.
- **Lists** (`nms:group`): Tables for managing recipient groups.
- **Templates** (`nms:template`): Templates for deliveries and campaigns.

### `XTK`: eXtended ToolKit

Covers **low-level operations**, technical and system-level functionalities, such as:

- **Workflows** (`xtk:workflow`): Workflow schemas and execution.
- **JavaScript APIs** (`xtk:javascript`): Server-side JavaScript APIs.
- **Session management** (`xtk:session`): Authentication and session handling.
- **Data schemas** (`xtk:srcSchema`): Base schemas for extending data models.

### `CRM`: Customer Relationship Management

CRM connector functionalities, such as integrating with external CRM systems (e.g., Salesforce, Microsoft Dynamics):
- **CRM connectors** (`crm:connector): Configuration for CRM integrations.
- **Synchronization** (`crm:sync`): Data synchronization between Adobe Campaign and CRM systems.

## Directory Structure Overview

Adobe Campaign's installation directory contains several key subdirectories:

```console
/usr/local/neolane/nl6/
├── bin/            # Executable scripts and binaries
├── conf/           # Configuration files
├── customers/      # Customer-specific configurations
├── datakit/        # Core application data and resources
├── deprecated/     # Legacy files (v6.0)
├── examples/       # Sample files and templates
├── java/           # Java libraries
├── lang/           # Language packs
├── migration/      # Migration scripts
├── rsetup/         # Setup and deployment scripts
├── tomcat-7/       # Tomcat server files
    └── conf/
        ├── apache_neolane.conf # Apache Configuration file
        └── server.xml  # Tomcat Configuration file
├── web/            # Web application files
├── zoneinfo/       # Timezone data
├── logs/           # Log files
│   ├── catalina.YYYY-MM-DD.log  # Tomcat logs
│   └── ...
└── var/            # Runtime and workflow data
    ├── res/        # Instance-specific resources
    │   └── <instanceName>/
    └── <instanceName>/  # Instance-specific directories
        ├── billing/
        ├── export/
        ├── incoming/
        ├── log/    # Log files for MTA, workflows, etc.
        │   ├── inMail.log
        │   ├── mta.log
        │   ├── runwf.log
        │   ├── stat.log
        │   └── wfserver.log
        ├── mta/
        ├── postupgrade/
        ├── redir/
        ├── upload/
        ├── workflow/  # Workflow execution files
        │   └── wf-<internalName>/
        │       └── httpTransfer/
        │           └── xxx.xml
        └── logins.log

```

## URL Mapping and Static Resources

### Common Application Server URLs

For an Adobe Campaign server (e.g., https://myserver-mkt-prod1.campaign.adobe.com or http://t.my-customserver.com):

URL Path | Description
--- | ---
`/view/home` | Homepage of the Adobe Campaign client.
`/nl/` | `/usr/local/neolane/nl6/web/`
`/nl/webForms/defaultWebApp.css` | `/usr/local/neolane/nl6/web/webforms/defaultWebApp.css`
`/webApp/{webApp-internalName` | web apps
`/{jssp-namespace}/{jssp-name}.jssp` | JSSP pages
`/nl/jsp/logon.jsp` | Logon page, redirects to Client install/download page
`/nl/jsp/install.jsp` | Client install/download page

### Health check

- `/r/test` -> test page, returns XML, see https://docs.campaign.adobe.com/doc/AC/en/PRO_Production_procedures_Monitoring_processes.html#Automatic_monitoring
- `/nl/jsp/ping.jsp` -> ping
  
### Resource Server (CDN)

Adobe Campaign uses a resource server (CDN) to serve public resources, such as images and files uploaded via the client console. Example URLs:

- `/r/test` -> test page
- `/res/instance_name/` -> Public resource files

### Default URL Mappings

Adobe Campaign maps URLs to local paths for serving static resources (images, JSP, XSL). Here’s a summary of the most common mappings:

Desc | URL | Local path
--- | --- | ---
Client exposition | `/nl` | `/web`
Datakit images | `/crm/img` | `/datakit/crm/eng/img`
. | `/ncm/img` | `/datakit/ncm/eng/img`
. | `/nl/img` | `/datakit/nl/eng/img`
. | `/nms/img` | `/datakit/nms/eng/img`<br><ul><li>Neolane Marketing Server (NMS) in `nms-logo-01.png`</li><li>program.png, asset.png, task.png</li></ul>
. | `/xtk/img` | `/datakit/xtk/eng/img`<br><ul><li>Navigation menus: print, paste, xtksave</li><li>Navigation explorer: navnode.png, navroot.png, loading.gif</li><li>Workflow UI: wfplay.png, /background, /activities</li><li>Schema explorer: xtklink.png</li></ul>
Datakit XSL | `/nms/xsl` | `/datakit/nms/eng/xsl`
. | `/xtk/xsl` | `/datakit/xtk/eng/xsl`
JSP exposition | `/nl/jsp` | `/datakit/nl/eng/jsp`
. | `/nms/jsp` | `/datakit/nms/eng/jsp`
. | `/xtk/jsp` | `/datakit/xtk/eng/jsp`
Legacy v6.0 js/css | `/xtk` | `/deprecated/xtk`
. | `/nms` | `/deprecated/nms`
. | `/crm` | `/deprecated/crm`
Empty path for `web.xml` | ` ` | `/web`
Other | `/cus` | `../customers`
. | `/res` | `/var/res`
. | `/examples` | `/examples`


## Conclusion
Understanding Adobe Campaign’s directory structure, server configuration, and URL mapping is essential for administrators and developers. This guide provides a foundation for managing and troubleshooting Adobe Campaign Classic deployments.
