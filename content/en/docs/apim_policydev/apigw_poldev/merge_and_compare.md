{
"title": "Compare and merge API Gateway configurations",
"linkTitle": "Compare and merge API Gateway configurations",
"weight": 13,
"date": "2019-10-17",
"description": "Compare the currently loaded API Gateway configuration with a configuration stored in a deployment package, and merge any differences."
}

In Policy Studio, you can compare the currently loaded API Gateway configuration with the following:

* Configurations stored in a deployment package (`.fed`).
* Configurations stored in a server configuration file (`.xml`).

Note that you cannot compare API Gateway currently loaded configuration against a policy package (`.pol`) or an environment package (`.env`).

You can also merge any differences between the configurations. Differences between configurations are identified as additions, deletions, or conflicts. When merging configurations, you can choose which differences to merge.

## Compare and merge configurations

To compare the currently loaded configuration against the configuration in a `.fed` file, follow these steps:

1. Click the **Compare** button on the Policy Studio toolbar.
2. In the **Comparing target with** field, click the **Browse** button to choose a `.fed` file to compare the configuration with.
3. Enter the passphrase for the configuration, if one has been set, and click **OK**. The configurations are compared and the results are displayed in a tree view. Only entities with differences are shown.
4. To see detailed differences, click a configuration entity in the tree. The differences for that entity are displayed in the **Difference Details** pane.
5. To merge differences into the currently loaded configuration, select the check box next to each difference to be merged, and click the **Merge** button at the top right of the window.

{{< alert title="Note" color="primary" >}}If you modify the currently loaded configuration after the **Compare and Merge** tab is opened, click the **Refresh** button to refresh the comparison and show any new differences. {{< /alert >}}

## Comparison results

The following image shows the result of a comparison:

![Comparison Result](/Images/docbook/images/deploy/merge_compare_result.png)

The **Difference Counts** pane shows the number of differences in total, the number of additions, the number of deletions, and the number of conflicts.

The **Differences** tree view shows all of the differences in the configuration entities:

* Entities with green plus icon are additions. They exist in the `.fed` file but not in the currently loaded configuration.
* Entities with a red minus icon are deletions. They exist in the currently loaded configuration but not in the `.fed` file.
* Entities with a yellow warning icon are conflicts. They exist in both configurations but are not the same.

The **Difference Details** pane shows the values of the fields in each configuration when you click on an entity in the tree view. The second column shows the values of the fields in the `.fed` file, and the third column shows the values of the fields in the currently loaded configuration. The fields that are different in each configuration are highlighted.

In the preceding image:

* The cron expression `Run at 2am every day in Jan` is a deletion.
* The cron expression `Run at 2:10pm and at 2:44pm every Wednesday in the month of March` is an addition.
* The user `sampleuser` is a conflict, because the password field has a different value in each configuration.

Some configuration entities contain references to other entities. In this case, an icon is displayed for the field in the **Difference Details** pane. Double-click a row with an icon to view the differences for those entities.

## Filter differences

To filter nodes from the **Differences** tree view based on their type, click **View Nodes**, and select from the following options:

* **Additions**
* **Deletions**
* **Conflicts**

All differences are shown by default.

## Select differences for merging

To select nodes for merging from the **Differences** tree view based on their type, click **View Nodes**, and select from the following options:

* **Additions**
* **Deletions**
* **Conflicts**

Additions are selected by default.

{{< alert title="Note" >}}If there are changes in the structure of a policy being merged, then it is possible that false positive circular dependencies are detected and a trace is outputted with this information. This is due to the updating mechanism in Policy Studio, which is based on change notifications from the Entity Store. The policy indicated in the trace should be checked to verify that there is no circular dependency and is a false positive.{{< /alert >}}