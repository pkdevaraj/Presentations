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


Knife builds a simple structure within our cookbooks directory for our new cookbook. Cookbook structure can viewed by navigating into the cookbooks directory, and into the directory with the cookbook name.

**Creating a Simple Recipe**

In the recipes subdirectory, there is a file called default.rb created by default.

This is the recipe that will be run if you reference the "nginx" recipe. We need to add our code and actions in this file.

Open the file with any text editor and add the contents as shown in the figure below:

/////////////////////

Add contentsofReceipie.png here

/////////////////////////

Plan the actions that need to happen for the Nginx web server to start and run. This is done by configuring "resources". Resources do not describe how to do something; they simply describe what a part of the system should look like when it is complete.

Make sure the software is installed by creating a "package" resource first.

//////////////////

Add Packagecreation.png

/////////////////

This little piece of code defines a package resource for Nginx. The first line begins with the type of resource (package) and the name of the resource ('nginx'). The rest is a group of actions and parameters that declare what n to be performed with the resource.

In this resource, set action :install. This line tells Chef that the resource described should be installed. The node that runs this recipe will check that Nginx is installed. If it is, it will check that off the list of things to do. If not, it will install the program using the methods available on the client system and then check it off.

After installation of the service, adjust its current state on the node. By default, Ubuntu does not start Nginx after installation, so change that as shown below

//////////////

add Changenode.png

//////////////

Here, resource is of the "service" type. This declares that for the Nginx service component (the part that allows us to manage the server with init or upstart), to start the service right now, and also enable it to start automatically when the machine is restarted.

The final resource that is declared is the actual file that we will be serving. Since this is just a simple file that will not be modifying anything, simply declare the location of the file and tell it where in the cookbook to get the file as shown below.

//////////

Add cookbookchangelocation.png


/////////


The "mode" line sets the permissions on the file created. In this case, the root user is allowed to read and write permissions and everyone else read permissions.

Save and close this file.

**Creating the Index file**
