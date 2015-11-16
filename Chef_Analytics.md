# Chef Analytics

The Chef Analytics platform is a feature of Chef that provides real-time visibility into what is happening on the Chef server, including what’s changing, who made those changes, and when they occurred. Individuals may be notified of these changes in real-time. Use this visibility to verify compliance against internal controls.

###Chef Analytics Components:

The following diagram shows the relationships between the various elements of Chef Analytics, including how information is routed from various nodes to the Chef Analytics server (through the Chef server) nodes, where reports about chef-client run outcomes may be viewed, where rules are processed, and where Chef Analytics data may be viewed.

![alt text](https://github.com/pkdevaraj/Presentations/blob/a20c76968d2be8e27609c46c27c09d27f57a13d5/Chef%20Images/Chef_analytics.PNG "Chef_analytics")

###Features and their Descriptions:

**Controls**:

A control is an automated test that is built into a cookbook, and then used to test the state of the system for accordance with specifications. Accordance can be many things. For example, ensuring that file and directory management meets specific internal IT policies—”Does the file exist?”, “Do the correct users or groups have access to this directory?”. Accordance may also be complex, such as helping to ensure goals defined by large-scale compliance frameworks such as PCI, HIPAA, and Sarbanes-Oxley can be met.

**Audit Mode**:

The chef-client may be run in audit-mode. Use audit-mode to evaluate custom rules—also referred to as audits—that are defined in recipes. audit-mode may be run in the following ways:

By itself (i.e. a chef-client run that does not build the resource collection or converge the node).

As part of the chef-client run, where audit-mode runs after all resources have been converged on the node.

Each audit is authored within a recipe using the control_group and control methods that are part of the Recipe DSL. Recipes that contain audits are added to the run-list, after which they can be processed by the chef-client. Output will appear in the same location as the regular chef-client run (as specified by the log_location setting in the client.rb file).

Finished audits are reported back to the Chef server. From there, audits are sent to the Chef Analytics platform for further analysis, such as rules processing and visibility from the actions web user interface.

**Chef Actions**:

The Chef server gathers a lot of data. For example:

- Changes made to each node object.

- The run history for all nodes.

- The history of every cookbook (and cookbook version).

- How and where policy settings—roles, environments, and data bags—are applied.

- Which users made which changes.

The Chef Analytics server collects all of this data and makes it visible from the Chef Analytics user interface.

**Reporting**:

Use Chef reporting to keep track of what happens during the execution of chef-client runs across all of the machines that are management by Chef. Reports can be generated for the entire organization and they can be generated for specific nodes.

Chef reporting data is collected during the chef-client run and the results are posted to the Chef server at the end of the chef-client run at the same time the node object is uploaded to the Chef server.

**Rules**:

Chef Analytics includes a powerful rules processing system that allows notifications to be generated based on observed events in the data stream, such as:

- Cookbook uploads.

- Modifications to environments.

- Machines on which chef-client runs have failed.

- Machines on which audit-mode runs have failed.

- Resources that were updated as a result of a chef-client run.

Notifications may be sent to any email address, a chat service like HipChat or Slack, or to a webhook-based service for generic intergrations.


[**NEXT**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_Cookbooks.md)  

[**BACK TO CONTENTS**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_Readme.md)
