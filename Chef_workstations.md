##CHEEF WORKSTATION


A workstation is a computer that is configured to run various Chef command-line tools that synchronize with a chef-repo, author cookbooks, interact with the Chef server, interact with nodes, or applications like Chef Delivery.

The workstation is the location from which most users do most of their work such as:

* Developing cookbooks and recipes (writing them using Ruby syntax and patterns)
* Keeping the chef-repo synchronized with version source control
* Using command-line tools
* Configuring organizational policy, including defining roles and environments and ensuring that critical data is stored in data bags
* Interacting with nodes appropriately like performing a bootstrap operation

Chef includes tooling like the Chef development kit, encourages integration and unit testing, and defines workflow around cookbook authoring and policy. When a decision is to be made, the chef-client uses a reasonable default setting that can be easily changed.

Some important components of workstations are:

* **Knife**

Knife is a command-line tool that provides an interface between a local chef-repo and the Chef server.
Knife helps users to manage Nodes, Cookbooks and recipes, Roles, Stores of JSON data (data bags), including encrypted data, Environments, Cloud resources, including provisioning, The installation of the chef-client on management workstations and Searching of indexed data on the Chef server

* **Knife Plugin**

A knife plugin is a set of one or more commands that can be added to knife to support additional functionality that is not built-in to the base set of knife commands. Most of the knife plugins are built by members of the Chef community and several of them are built and maintained by Chef. A knife plugin is installed to the **~/.chef/plugins/knife/ directory**, so that it can be run just like any other knife command.

The same common options used by knife commands can also be used by knife plugins.A knife plugin can make authenticated API requests to the Chef server.

More information on knife plugins can be found [here](https://docs.chef.io/plugin_knife.html)

* **CHEF-REPO**

The chef-repo is the repository structure in which cookbooks are written, tested, and maintained.
Cookbooks contain recipes, attributes, custom resources, libraries, definitions, files, templates, tests, and metadata.
The chef-repo should be synchronized with a version control system (such as git,Perforce etc), and then managed just like source code.
The directory structure within the chef-repo varies. Some organizations prefer to keep all of their cookbooks in a single chef-repo, while other organizations prefer to use a chef-repo for every cookbook.


