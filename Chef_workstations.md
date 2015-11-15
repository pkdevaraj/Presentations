##CHEEF WORKSTATION


A workstation is a computer that is configured to run various Chef command-line tools that synchronize with a chef-repo, author cookbooks, interact with the Chef server, interact with nodes, or applications like Chef Delivery.

The workstation is the location from which most users do most of their work, including:

* Developing cookbooks and recipes (and authoring them using Ruby syntax and patterns)
* Keeping the chef-repo synchronized with version source control
* Using command-line tools
* Configuring organizational policy, including defining roles and environments and ensuring that critical data is stored in data bags
* Interacting with nodes, as (or when) required, such as performing a bootstrap operation

While Chef includes tooling like the Chef development kit, encourages integration and unit testing, and defines workflow around cookbook authoring and policy, it’s important to note that you know best about how your infrastructure should be put together. Therefore, Chef makes as few decisions on its own as possible. When a decision must be made, the chef-client uses a reasonable default setting that can be easily changed. While Chef encourages the use of the tooling packaged in the Chef development kit, none of these tools should be seen as a requirement or pre-requisite for being successful using Chef.

