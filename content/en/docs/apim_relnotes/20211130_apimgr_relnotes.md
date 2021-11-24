---
title: API Gateway and API Manager 7.7 November 2021 Release Notes
linkTitle: API Gateway and API Manager November 2021
weight: 95
date: 2021-09-21
description: API Gateway and API Manager updates are cumulative, comprising new
  features and changes delivered in previous updates unless specifically
  indicated otherwise in the Release notes.
---
## Installation

* To **update** your API Gateway, see [Update from API Gateway One Version](/docs/apim_installation/apigw_upgrade/upgrade_steps_oneversion/).
* To **upgrade** from an older version, see [Upgrade from API Gateway 7.5.x or 7.6.x](/docs/apim_installation/apigw_upgrade/upgrade_steps_extcass/).
* For more details on supported platforms for software installation, see [System requirements](/docs/apim_installation/apigtw_install/system_requirements/).
* For a summary of the system requirements for a Docker deployment, see [Set up Docker environment](/docs/apim_installation/apigw_containers/docker_scripts_prereqs/).

### Update a container deployment

Any custom `.fed` files deployed to a container must be upgraded using [upgradeconfig](/docs/apim_installation/apigw_upgrade/upgrade_analytics#upgradeconfig-options) or [projupgrade](/docs/apim_reference/devopstools_ref#projupgrade-command-options). They must be upgraded the same way, regardless of whether they are API Manager enabled or not. The `.fed` files contain the updates for the API Manager configuration and can be used to build containers.

## New features and enhancements

The following new features and enhancements are available in this update.

### placeholder 1

placeholder

### Set Client Credentials as a Grant type

You can now enable OAuth authorization for access tokens as Client credential type to share resources from another server using a Client ID and a Client Secret. For more information, see [Setting Grant type - Client Credentials](/docs/apim_administration/apimgr_admin/api_mgmt_virtualize_web/#grant-type---client-credentials).

### New Amplify menu header

A new customisable header has been integrated to API Manager and API Gateway Manager. The new header allows you to enable search and help in multiple Axway portals, and to access the [Amplify platform](https://platform.axway.com/#/) portal. For more information see, [Customize Amplify menu header](/docs/apim_administration/apimgr_admin/api_mgmt_custom/#customize-amplify-menu-header).

## Important changes

It is important, especially when upgrading from an earlier version, to be aware of the following changes in the behavior or operation of the product in this update, which may impact on your current installation.

### placeholder 2

placeholder

### Docker scripts now use Python 3

The Externally Managed Topology (EMT) scripts were upgraded from Python 2.7 to Python 3. For more information, see [Set up Your Docker Evironment](/docs/apim_installation/apigw_containers/docker_scripts_prereqs/#set-up-your-docker-environment).

## Deprecated features

<!--As part of our software development life cycle we constantly review our API Management offering. In this update, the following capabilities have been deprecated-->

No capabilities have been deprecated in this update.

## End of support notices

### Developer tools on Windows 8.1

This is a reminder that in February 2022 we will remove support for the installation and update of [developer tools](/docs/apim_installation/apigtw_install/install_dev_tools/) on Windows 8.1

## Removed features

<!-- To stay current and align our offerings with customer demand and best practices, Axway might discontinue support for some capabilities. As part of this review, the following features have been removed: -->

### placeholder 4

placeholder

## Fixed issues

This version of API Gateway and API Manager includes:

* Fixes from all 7.5.3, 7.6.2, and 7.7 service packs released prior to this version. For details of all the service pack fixes included, see the corresponding *SP Readme* attached to each service pack on [Axway Support](https://support.axway.com).
* Fixes from all 7.7 updates released prior to this version. For details of all the update fixes included, see the corresponding [Release note](/docs/apim_relnotes/) for each 7.7 update.

### Fixed security vulnerabilities

placeholder

### Other fixed issues

placeholder

## Known issues

The following are known issues for this update.

### Scripting filter whiteboard attributes not preloaded for Jython scripts

The Scripting filter now uses a Jython 2.7 scripting environment (previously, Jython 2.5) to execute Jython scripts. As a result of this version change, the whiteboard attributes, such as `http.request.uri` and `http.request.verb`, are no longer preloaded for use by Jython scripts. However, you can run a Jython script to load these attributes before they are accessed as follows:

```
from com.vordel.trace import Trace

def invoke(msg):
    msg.forceGenerateAttributes()
    Trace.info("This trace statement was generated in script filter!  [" + str(msg.get("http.request.verb")) + "] [" + str(msg.get("http.request.uri")) + "]")
    return True
```

Related Issue: RDAPI-21363

### When an API Gateway instance is started, Xerces SAXParserImpl writes warnings to the error console

At API Gateway instance startup, the following warnings are logged to the error console, as opposed to the trace log:

```
Warning: org.apache.xerces.jaxp.SAXParserImpl$JAXPSAXParser: Property 'http://javax.xml.XMLConstants/property/accessExternalDTD' is not recognized.
Warning: org.apache.xerces.jaxp.SAXParserImpl$JAXPSAXParser: Property 'http://www.oracle.com/xml/jaxp/properties/entityExpansionLimit' is not recognized.
```

These new properties were added in JAXP 1.5 specification, which is supported by the embedded implementation in the JRE but not supported yet in Xerces-J Apache implementation. These are harmless warning messages, which are written to the error console instead of throwing an exception if a property is not supported by the Apache Xerces-J implementation.

Related Issue: RDAPI-22218

## Documentation

To find all available documentation for this product version:

1. Go to [Manuals on the Axway Documentation portal](https://docs.axway.com/bundle).
2. In the left pane **Filters** list, select your product or product version.

Customers with active support contracts need to log in to access restricted content.

For information on the different operating systems, databases, browsers, and thick client platforms supported by each Axway product, see [Supported Platforms](https://docs.axway.com/bundle/Axway_Products_SupportedPlatforms_allOS_en).

## Support services

The Axway Global Support team provides worldwide 24 x 7 support for customers with active support agreements.

Email [support@axway.com](mailto:support@axway.com) or visit [Axway Support](https://support.axway.com/).

See [Get help with API Gateway](/docs/apim_administration/apigtw_admin/trblshoot_get_help/) for the information that you should be prepared to provide when you contact Axway Support.
