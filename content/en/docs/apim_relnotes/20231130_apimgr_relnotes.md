---
title: API Gateway and API Manager 7.7 November 2023 Release Notes
linkTitle: API Gateway and API Manager November 2023
weight: 95
date: 2023-09-11
description: null
---
API Gateway and API Manager updates are cumulative, comprising new features and changes delivered in previous updates unless specifically indicated otherwise in the Release notes.

placeholder

## Installation

* To **update** your API Gateway, see [Update from API Gateway One Version](/docs/apim_installation/apigw_upgrade/upgrade_steps_oneversion/).
* To **upgrade** from an older version, see [Upgrade from API Gateway 7.5.x or 7.6.x](/docs/apim_installation/apigw_upgrade/upgrade_steps_extcass/).
* For more details on supported platforms for software installation, see [System requirements](/docs/apim_installation/apigtw_install/system_requirements/).
* For a summary of the system requirements for a Docker deployment, see [Set up Docker environment](/docs/apim_installation/apigw_containers/deployment_flows/custom_image_deployment/docker_scripts_prereqs/).

### Update a container deployment

Any custom `.fed` files deployed to a container must be upgraded using [upgradeconfig](/docs/apim_installation/apigw_upgrade/upgrade_analytics#upgradeconfig-options) or [projupgrade](/docs/apim_reference/devopstools_ref#projupgrade-command-options). They must be upgraded the same way, regardless of whether they are API Manager enabled or not. The `.fed` files contain the updates for the API Manager configuration and can be used to build containers.

## New features and enhancements

The following new features and enhancements are available in this update.

### placeholder 1

placeholder

## Important changes

It is important, especially when upgrading from an earlier version, to be aware of the following changes in the behavior or operation of the product in this update, which might impact your current installation.

### placeholder 2

placeholder

## End of support notices

To stay current and align our offerings with customer demand and best practices, Axway might discontinue support for some capabilities.

As part of this update, the following features have notice for removal:

<!-- There are no end of support notices in this update. -->

* Support for IBM DB2 version 10.5 as a database will end in February 2024.
* Support for CA Siteminder filters will end in August 2024.
* Support for Oracle Access Manager filters will end in August 2024.
* Support for RSA Cleartrust (RSA Access Manager) will end in August 2024.
* Support for customer created images for container deployment, by way of EMT scripts, will end in August 2024 (use of Axway created images only will be supported).
* Support for Client Application Registry (CAR) will end in February 2024. The API Gateway can still act as an OAuth server without CAR, but API Manager will be required when CAR-only mode is no longer available.

## Removed features

The following features have been removed from the product in this update:

placeholder

## Fixed issues

This version of API Gateway and API Manager includes:

* Fixes from all 7.7 updates released prior to this version. For details of all the update fixes included, see the corresponding [Release note](/docs/apim_relnotes/) for each 7.7 update.
* Additional fixes might be delivered as patches up to 15 months after the release date. You can find the list of patches available on top of this update on [Axway Support](https://support.axway.com/en/search/index/type/Downloads/q/20231130/ipp/100/product/324/product/464/version/3034/version/3035/subtype/8). If no patches were created for this release, the link will return "No search results found".

### Fixed security vulnerabilities

placeholder

### Other fixed issues

placeholder

## Known issues

The following are known issues for this update.

### JSON Remove Node filter behavior change

The JSON Remove Node filter is not working as expected when parsing an already empty array.

If the filter uses a syntax like `$.apis[*]` to make an array empty but the array in the JSON fragment is already empty, the filter throws an exception. The only way to force the array to be empty is to provide the `$.apis` syntax, but that removes the whole field.

Related issue: RDAPI-29426

### Policy Studio Toolbar

Policy Studio perspective has an intermittent error with the toolbar failing to display on the UI. All operations provided by the toolbar can be executed using menu items.

Related issue: RDAPI-29504

### Data Maps cannot be created or configured in Policy Studio

Data maps cannot be created or configured in Policy Studio from May 2023 release because of a conflict with Eclipse RCP 4.9. The data maps created in previous releases will still work correctly on the API Gateway runtime environment. You can develop and export configurations in Policy Studio versions prior to May 2023, and deploy the configuration upgraded in this release.

Related issue: RDAPI-29504

### Policy Studio Graphic Dispose error

An error dialog notifying a Graphic Dispose error might be shown upon closing Policy Studio. If the error occurs, it will also be shown in the Policy Studio logs. This error has no impact.

Related issue: RDAPI-29504

### Changing Scripting filter engine in YAML projects

In Policy Studio YAML projects, when updating the scripting engine in the scripting filter, the old script is not deleted. Customers can manually delete the old script from the project with no impact.

Related issue: RDAPI-29887

### Scripting filter whiteboard attributes not preloaded for Jython scripts

The Scripting filter now uses a Jython 2.7 scripting environment (previously, Jython 2.5) to execute Jython scripts. As a result of this version change, the whiteboard attributes, such as `http.request.uri` and `http.request.verb`, are no longer preloaded for use by Jython scripts. However, you can run a Jython script to load these attributes before they are accessed as follows:

```none
from com.vordel.trace import Trace

def invoke(msg):
    msg.forceGenerateAttributes()
    Trace.info("This trace statement was generated in script filter!  [" + str(msg.get("http.request.verb")) + "] [" + str(msg.get("http.request.uri")) + "]")
    return True
```

Related Issue: RDAPI-21363

### API Manager runtime does not perform full parameter validation for compound schemas

In API Manager, when you import an OAS definition, which contains a `PathItem` with a content-type of `application/x-www-form-urlencoded` or `multipart/form-data`, and the `content` contains a compound schema of `anyOf` or `oneOf`, the internal model ends up with a list of optional form parameters without a link to the original schema definition. As a result, the API Manager runtime cannot correctly validate inbound requests to the API methods in question because the schema information is missing. This has the potential side-effect of incorrectly allowing certain combinations of form parameters to be sent to the backend service. This is best illustrated with an example.

Consider the following `PathItem` definition:

```json
   "/form-anyOf": {
      "post": {
        "requestBody": {
          "content": {
            "application/x-www-form-urlencoded": {
              "schema": {
                "$ref": "#/components/schemas/TestAnyOf"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    }
  },
```

where the `TestAnyOf` schema is defined as:

```json
      "TestAnyOf": {
        "anyOf": [
          {
            "$ref": "#/components/schemas/Cat"
          },
          {
            "$ref": "#/components/schemas/Dog"
          }
        ]
      },
      "Cat": {
        "additionalProperties": false,
        "type": "object",
        "required": [
          "name"
        ],
        "properties": {
          "name": {
            "type": "string",
            "enum": ["cat","felix"]
          }
        }
      },
      "Dog": {
        "additionalProperties": false,
        "type": "object",
        "required": [
          "age"
        ],
        "properties": {
          "age": {
            "type": "integer"
          },
          "time": {
            "type": "string",
            "format": "date-time"
          }
        }
      }
```

This results in the optional form parameters `name`, `age`, and `time` being generated and stored as part of the internal model for the API method. If the following body is sent as part of a runtime request, parameter validation will succeed and all parameters will be forwarded to the backend service, despite the underlying schema indicating that the request body must contain `anyOf` 'Cat' or 'Dog', but not both.

```json
{code}
name=felix&age=5&time=2022-12-31T22:59:01Z
{code}
```

Related Issue: RDAPI-29098

### API Manager quota functionality does not work with MySQL 8

If you are using a MySQL database for API Manager quotas, you must use MySQL 5.7, otherwise a SQLException will be raised.

Related Issue: RDAPI-29436

### URLLIB2 issues in Jython 2.7.3

Following the upgrade to Jython 2.7.3, the following issue has been observed for some `urllib2` based requests to a server - "TypeError: cannot make memory view because object does not have the buffer interface". This does not affect all requests, and it has been documented externally as a known issue with versions above Jython 2.7.2. For custom Jython scripts, a potential workaround is to use the `urllib3` library instead.

Related Issue: RDAPI-29910

### Visual Mapper exception

During the first transformation performed by the Visual Mapper filter runtime there is an exception with a message "Could not register default TransformerFactory". This will not impact the transformation performed and can be ignored.

Related Issue: RDAPI-30439

### Supported characters for filtering Applications in API Manager

Characters which are not included in the ISO-8859-1 standard (for example, Chinese characters) are not supported for use in API Manager when filtering Applications.

Related Issue: RDAPI-24001

## Documentation

To find all available documentation for this product's version:

1. Go to [Library, on the Axway Documentation portal](https://docs.axway.com/bundle).
2. From the left pane **Product** list, select **API Management**.

Customers with active support contracts must log in to access restricted content.

## Supported platforms

For information on the different operating systems, databases, browsers, and thick client platforms supported by each Axway product, see [Supported Platforms](https://docs.axway.com/bundle/Axway_Products_SupportedPlatforms_allOS_en_HTML5/page/api_management.html).

## Support services

The Axway Global Support team provides worldwide 24 x 7 support for customers with active support agreements. Email [support@axway.com](mailto:support@axway.com) or visit [Axway Support](https://support.axway.com/).

See [Get help with API Gateway](/docs/apim_administration/apigtw_admin/trblshoot_get_help/) for the information that you should be prepared to provide when you contact Axway Support.
