# Chef Guide to Create Cookbooks

Here, let us see the basics of creating a Chef cookbook. Cookbooks are the configuration units that allow us to configure and perform specific tasks within Chef on our remote nodes. We build cookbooks and then tell Chef which nodes we want to run the steps outlined in the cookbook.

These are few features of Cookbook.

A **Recipe** is the main workhorse of the cookbook. A cookbook can contain more than one recipe, or depend on outside recipes. Recipes are used to declare the state of different resources.

**Attributes** in Chef are basically settings. They could be considered as simple key-value pairs for anything you might want to use in your cookbook.

The **Files** subdirectory within the cookbook contains any static files that we will be placing on the nodes that use the cookbook.

**Templates** are similar to files, but they are not static. Template files end with the .erb extension, meaning that they contain embedded Ruby.

###Getting Started with Chef 

**Installation of CHEF**

Chef is installed and configured in three main phases: setting up the Chef server, setting up a workstation, and then installing the chef-client on each node that will be under management by Chef.

Before installation make sure that the system requirements (specified [here](https://docs.chef.io/chef_system_requirements.html)) are met.

To install a Chef Server check [here](https://docs.chef.io/install_server.html) for instructions.

To install a Workstation check [here](https://docs.chef.io/install_dk.html) for instructions

To install a Chef Client check [here](https://docs.chef.io/install_bootstrap.html) for instructions.

Chef also has additional features that can be enabled as part of the setup and configuration process. This can be found [here] (https://docs.chef.io/install.html).

**Creation of CookBooks**

Let us now create a Simple Cookbook on Ubuntu.

This is be a very simple cookbook that installs and configures the Nginx web server on our node.

To begin, Enter ~/chef-repo directory on the workstation by entering the following command
  
####**cd ~/chef-repo**

Now create a cookbook by using knife. It can be used to perform work on our workstation and also to connect with the Chef server or individual nodes.

The general syntax for creating a cookbook is:

####**knife cookbook create cookbook_name**

In this case name the cookbook as nginx instead odcookbook_name.

///////////

Add CreateCookbook1.png

///////////




