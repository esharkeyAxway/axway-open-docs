---
title: API Gateway and API Manager 7.7 August 2021 Release Notes
linkTitle: API Gateway and API Manager August 2021
weight: 95
date: 2021-06-21
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

### Elastic-Stack Logging is available for API Gateway

The Elastic-Stack (Elasticsearch, Logstash, and Kibana) solution, version 3.2.0, is now production-ready for you to integrate with your API Gateway. For more information see, [Configure Elastic-Stack Logging](/docs/apim_administration/apigtw_admin/logging/#configure-elastic-stack-logging).

### YAML configuration store

It is now possible to deploy [YAML configuration](/docs/apim_yamles/) stores in the API Gateway Manager web UI on port 8090. For more information, see [Manage domain topology in API Gateway Manager](/docs/apim_administration/apigtw_admin/managetopology/#deploy-a-yaml-deployment-package).

### ICAP message preview

The ICAP filter now supports message preview ([RFC 3507, Section 4.5](https://datatracker.ietf.org/doc/html/rfc3507#section-4.5)). For more information, see [Message preview in Configure ICAP servers](/docs/apim_policydev/apigw_external_connections/common_icap_conf/#enable-message-preview-in-request-headers).

## Important changes

It is important, especially when upgrading from an earlier version, to be aware of the following changes in the behavior or operation of the product in this update, which may impact on your current installation.

### McAfee Anti-Virus filter has been retired

The McAfee Anti-Virus filter has been retired in this update. This means that this filter is no longer available to use when creating policies in Policy Studio. Existing configurations that use the filter will show a warning when upgraded in Policy Studio or with an upgrade tool, such as `projupgrade`.

It is important that you update your policies and replace the McAfee Anti-Virus filter with the [Internet Content Adaption Protocol (ICAP)](/docs/apim_policydev/apigw_external_connections/common_icap_conf/) virus scan filter, or remove it entirely.

It will still be possible to deploy upgraded configurations containing the retired McAfee filter, and updated gateways will continue to run existing deployed configuration, but the McAfee filter, now deprecated, will show a warning in the gateway trace files and will always return a fail response.

### Support for Apache Cassandra 3.11.11

API Gateway now supports Apache Cassandra 3.11.11. For details on how to upgrade existing Apache Cassandra environments, see [Upgrade Apache Cassandra](/docs/apim_installation/apigw_upgrade/upgrade_cassandra/).

{{< alert title="Note" >}}Apache Cassandra version 2.2 onwards will no longer be supported by Apache Cassandra after their end of service date of April 2022. Axway will continue to provide support for these versions on a best efforts basis post April 2022, however, no critical updates will be available from Apache Cassandra from that time. Therefore, we recommend you to update your Cassandra installation to version 3.11.11 before that time.
{{< /alert >}}

### Unauthenticated request rate limiter is available in API Manager

You can now configure an unauthenticated request rate limiter in your API Manager. For more information, see [Configure API Manager unauthenticated request rate limiter](/docs/apim_administration/apimgr_admin/api_mgmt_config/#configure-api-manager-unauthenticated-request-rate-limiter).

### Notice of schedule change for updates

The cadence of the updates for API Gateway, API Manager, and API Portal has changed. From the August update onwards, the update schedule follows a three months release cycle.

## Deprecated features

<!--As part of our software development life cycle we constantly review our API Management offering. In this update, the following capabilities have been deprecated-->

No capabilities have been deprecated in this update.

## End of support notices

### Apache Cassandra 2.2.x

<!-- There are no end of support notices in this update.-->

Apache Cassandra version 2.2 onwards will no longer be supported by Apache Cassandra after their end of service date of April 2022. Axway will continue to support these versions on a best efforts basis, however, no critical updates will be available from Apache Cassandra from that time.

## Removed features

<!-- To stay current and align our offerings with customer demand and best practices, Axway might discontinue support for some capabilities. As part of this review, the following features have been removed: -->

### Antivirus filters

The McAfee Anti-Virus filter has been retired in this update.

## Fixed issues

This version of API Gateway and API Manager includes:

* Fixes from all 7.5.3, 7.6.2, and 7.7 service packs released prior to this version. For details of all the service pack fixes included, see the corresponding *SP Readme* attached to each service pack on [Axway Support](https://support.axway.com).
* Fixes from all 7.7 updates released prior to this version. For details of all the update fixes included, see the corresponding [Release note](/docs/apim_relnotes/) for each 7.7 update.

### Fixed security vulnerabilities

Table

### Other fixed issues

Table

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
