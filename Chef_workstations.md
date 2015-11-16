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

* **Chef Development Kit (Chef DK)**

Chef DK is a package that contains all the development tools you will need when coding Chef. It combines the best of the breed tools developed by Chef community with Chef Client. 

Here are few things that you can do with Chef DK:
     
     - Get your cookbook dependencies under control and have a good way of composing the cookbooks you need with the new Berkshelf 3.0
     - Take advantage of built-in testing with the default lint tool for cookbooks FoodCritic, cookbook unit
     - Testing framework ChefSpec & the leading integration testing framework for coded infrastructure Test Kitchen
     - Easily setup and upgrade the Chef Client on your workstation

To install chef development kit follow the instruction [here](https://docs.chef.io/install_dk.html).



* **Knife**

Knife is a command-line tool that provides an interface between a local chef-repo and the Chef server.
Knife helps users to manage Nodes, Cookbooks and recipes, Roles, Stores of JSON data (data bags), including encrypted data, Environments, Cloud resources, including provisioning, The installation of the chef-client on management workstations and Searching of indexed data on the Chef server.

To know more about Knife check [this](https://docs.chef.io/knife.html).

* **Knife Plugin**

A knife plugin is a set of one or more commands that can be added to knife to support additional functionality that is not built-in to the base set of knife commands. Most of the knife plugins are built by members of the Chef community and several of them are built and maintained by Chef. A knife plugin is installed to the **~/.chef/plugins/knife/ directory**, so that it can be run just like any other knife command.

The same common options used by knife commands can also be used by knife plugins.A knife plugin can make authenticated API requests to the Chef server.

More information on knife plugins can be found [here](https://docs.chef.io/plugin_knife.html).

* **CHEF-REPO**

The chef-repo is the repository structure in which cookbooks are written, tested, and maintained.
Cookbooks contain recipes, attributes, custom resources, libraries, definitions, files, templates, tests, and metadata.
The chef-repo should be synchronized with a version control system (such as git,Perforce etc), and then managed just like source code.
The directory structure within the chef-repo varies. Some organizations prefer to keep all of their cookbooks in a single chef-repo, while other organizations prefer to use a chef-repo for every cookbook.

More information on this can be found [here](https://docs.chef.io/chef_repo.html).

* **Knife.rb**

A Knife.rb file is used to specify the chef-repo-specific configuration details for knife.
This file is loaded every time this executable is run.The default location in which knife expects to find this file is ~/chef-repo/.chef/knife.rb. When a knife.rb file is present in this directory, the settings contained within that file will override the default configuration settings.

More information on how to configure using knife.rb file can be found [here](https://docs.chef.io/config_rb_knife.html).

* **metadata.rb**

Every cookbook requires some amount of metadata. Metadata is stored in a file called metadata.rb that lives at the top of each cookbook’s directory. The contents of the metadata.rb file provides hints to the Chef server so that cookbooks are deployed to each node correctly.

A metadata.rb file is never interpreted directly. Rather, the metadata.rb file provides a simple location to store and edit data that is then compiled by the Chef server and stored as JSON data. This is compiled when a cookbook is uploaded to the Chef server or when the knife cookbook metadata subcommand is run. knife creates a metadata.rb file automatically whenever the knife cookbook create subcommand is run.

Editing of metadata should only be done using the metadata.rb file, and then either by uploading the cookbook in which that metadata.rb file is located to the Chef server or by asking the Chef server to recompile the metadata into JSON data.

More information on this can be found [here](https://docs.chef.io/config_rb_metadata.html).

* **Kitchen**

Kitchen is used to automatically test cookbook data across any combination of platforms and test suites. This is defined in a .kitchen.yml file using a driver plugin architecture. Supports cookbook testing across many cloud providers and virtualization technologies and also supports all common testing frameworks that are used by the Ruby community.

Check [this](http://kitchen.ci/docs/getting-started/) to get started with kitchen.

* **ChefSpec**

	
ChefSpec is used to simulate the convergence of resources on a node. This runs the chef-client on a local machine
using chef-zero or chef-solo. It is an extension of RSpec, a behavior-driven development (BDD) framework for Ruby
and is one of the fastest way to test resources and recipes.

This is a part of ChefDK and run ChefSpec using the command below in the command line:

$ chef exec rspec

More information on how to use chefspec is listed [here](https://docs.chef.io/chefspec.html).

[**NEXT**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_Nodes.md)     

[**BACK TO CONTENTS**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_Readme.md)

