# Chef Guide to Create Cookbooks

Here, let us see the basics of creating a Chef cookbook. Cookbooks are the configuration units that allow us to configure and perform specific tasks within Chef on our remote nodes. We build cookbooks and then tell Chef which nodes we want to run the steps outlined in the cookbook.

These are few features of Cookbook.

A **Recipe** is the main workhorse of the cookbook. A cookbook can contain more than one recipe, or depend on outside recipes. Recipes are used to declare the state of different resources.

**Attributes** in Chef are basically settings. They could be considered as simple key-value pairs for anything you might want to use in your cookbook.

The **Files** subdirectory within the cookbook contains any static files that we will be placing on the nodes that use the cookbook.

**Templates** are similar to files, but they are not static. Template files end with the .erb extension, meaning that they contain embedded Ruby.

###Getting Started with Chef 

- **Installation of CHEF**

Chef is installed and configured in three main phases: setting up the Chef server, setting up a workstation, and then installing the chef-client on each node that will be under management by Chef.

Before installation make sure that the system requirements (specified [here](https://docs.chef.io/chef_system_requirements.html)) are met.

To install a Chef Server check [here](https://docs.chef.io/install_server.html) for instructions.

To install a Workstation check [here](https://docs.chef.io/install_dk.html) for instructions

To install a Chef Client check [here](https://docs.chef.io/install_bootstrap.html) for instructions.

Chef also has additional features that can be enabled as part of the setup and configuration process. This can be found [here] (https://docs.chef.io/install.html).

- **Creation of CookBooks**

Let us now create a Simple Cookbook on Ubuntu.

This is be a very simple cookbook that installs and configures the Nginx web server on our node.

To begin, Enter ~/chef-repo directory on the workstation by entering the following command
  
**cd ~/chef-repo**

Now create a cookbook by using knife. It can be used to perform work on our workstation and also to connect with the Chef server or individual nodes.

The general syntax for creating a cookbook is:

**knife cookbook create cookbook_name**

In this case name the cookbook as nginx instead of cookbook_name.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/CreateCookbook1.png "Createcookbook1")

Knife builds a simple structure within our cookbooks directory for our new cookbook. Cookbook structure can viewed by navigating into the cookbooks directory, and into the directory with the cookbook name.

- **Creating a Simple Recipe**

In the recipes subdirectory, there is a file called default.rb created by default.

This is the recipe that will be run if you reference the "nginx" recipe. We need to add our code and actions in this file.

Open the file with any text editor and add the contents as shown in the figure below:

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/ContentsofRecipie.png "Contents of Receipe")

Plan the actions that need to happen for the Nginx web server to start and run. This is done by configuring "resources". Resources do not describe how to do something; they simply describe what a part of the system should look like when it is complete.

Make sure the software is installed by creating a "package" resource first.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/packageCreation.png "PkgCreation")

This little piece of code defines a package resource for Nginx. The first line begins with the type of resource (package) and the name of the resource ('nginx'). The rest is a group of actions and parameters that declare what n to be performed with the resource.

In this resource, set action :install. This line tells Chef that the resource described should be installed. The node that runs this recipe will check that Nginx is installed. If it is, it will check that off the list of things to do. If not, it will install the program using the methods available on the client system and then check it off.

After installation of the service, adjust its current state on the node. By default, Ubuntu does not start Nginx after installation, so change that as shown below

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/nodechange.png "NodeChange")

Here, resource is of the "service" type. This declares that for the Nginx service component (the part that allows us to manage the server with init or upstart), to start the service right now, and also enable it to start automatically when the machine is restarted.

The final resource that is declared is the actual file that we will be serving. Since this is just a simple file that will not be modifying anything, simply declare the location of the file and tell it where in the cookbook to get the file as shown below.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/cookbooklocationchange.png%5B.png "CookbookChangeLocation")

The "mode" line sets the permissions on the file created. In this case, the root user is allowed to read and write permissions and everyone else read permissions.

Save and close this file.

- **Creating the Index file**

We defined a "cookbook_file" resource which should move a file called "index.html" into the document root on the node. So create this file in ''files/default" subdirectory of the cookbook.

Enter the contents as shown below and save it.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/indexfileContent.png "IndexFileContent")

- **Creating a Helper Cookbook**

When a node tries to run the cookbook that was created as it is now, chances are, it will fail.

That is because it will attempt to install Nginx from the Ubuntu repositories, and the package database on the node is most likely out-of-date. Usually, run "sudo apt-get update" prior to running package commands.

To address this, create a simple cookbook whose only purpose is to ensure that the package database is updated.

This can be done using the same knife syntax  used before. Create this cookbook "apt":

**knife cookbook create apt**

Edit the default recipe for the new cookbook.

In this file, declare an "execute" resource. This is simply a way of defining a command that is to run on the node.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/aptinstallcontent.png "AptInstallUpdate")

Now, there are a number of ways that to make sure that this is executed before Nginx cookbook. Add it to the node's run-list before the Nginx cookbook, but it can also be tied into the Nginx cookbook itself.

This is probably the better option because it need not add the "apt" cookbook before the "nginx" cookbook on every node which is configured for Nginx.

So adjust a few things in the Nginx cookbook to make this happen. First, open the Nginx recipe file again add the contens below and save it.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/ningxChanges.png "ningxfilechanges")

Edit the metadata.rb file. This file is checked when the Chef server sends the run-list to the node, to see which other recipes should be added to the run-list.


![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/metadatacontents.png "metadatafilecontents")

Nginx cookbook now relies on apt cookbook to take care of the package database update.

- **Add the Cookbook to Node**

Upload them to chef server using the command below.

**knife cookbook upload apt**

**knife cookbook upload nginx**

Now, modify the run-list of our nodes typing:

**knife node edit name_of_node**

name_of_node here is client1 with contents as shown below

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/clientcontents.png "ClientContents")

Set the EDITOR environmental variable before this works using the commands below

#####export EDITOR=name_of_editor

This is a simple JSON document that describes some aspects of the node where the "run_list" array, is currently empty.

Add Nginx cookbook to that array using the command:

**"recipe[name_of_recipe]"**

Contents of the file are updated as shown below
![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/clientcontentsupdated.png "ClientContentsUpdated")

Now, SSH into the node and run the Chef client software. This will cause the client to check into the Chef server. Once it does this, it will see the new run-list that has been assigned it.

SSH into the node and then run this:

**sudo chef-client**

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/SSHResponse.png "SSHResponse")

As you can see, the apt cookbook was sent over and run as well, even though it wasn't in the run-list we created. That is because Chef intelligently resolved dependencies and modified the actual run-list before executing it on the node.

**Note**: There are various methods of ensuring that one cookbook or recipe is run before another. Adding a dependency is only one choice, and other methods may be preferred.

We can verify that this works by going to our node's IP address or domain name:

**http://node_domain_or_IP**

The Response should be something like this.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef%20Images/finalpingresponse.png "FinalResponse")

[**NEXT**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_conclusion.md)   

[**BACK TO CONTENTS**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_Readme.md)
  
