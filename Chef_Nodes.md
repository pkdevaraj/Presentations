##**NODES**

- A node is any machine-physical, virtual, cloud, network device, etc, that is under management by Chef.
- The types of nodes that can be managed by Chef are:

-- Server: A physical node is typically a server or a virtual machine, but it can be any active device attached to a network that is capable of sending, receiving, and forwarding information over a communications channel.

-- Cloud: A cloud-based node is hosted in an external cloud-based service, such as Amazon Web Services (AWS), OpenStack, Rackspace, Google Compute Engine, or Microsoft Azure. Plugins are available for knife to provide support for external cloud-based services. knife can use these plugins to create instances on cloud-based services. Once created, the chef-client can be used to deploy, configure, and maintain those instances.

-- Virtual Machine: A virtual node is a machine that runs only as a software implementation, but otherwise behaves much like a physical machine.

-- Network Device: A network node is any networking device—a switch, a router—that is being managed by a chef-client, such as networking devices by Juniper Networks, Arista, Cisco, and F5. Use Chef to automate common network configurations, such physical and logical Ethernet link properties and VLANs, on these devices.

-- Containers: Containers are an approach to virtualization that allows a single operating system to host many working configurations, where each working configuration—a container is assigned a single responsibility that is isolated from all other responsibilities. Containers are popular as a way to manage distributed and scalable applications and services.

- The key components of nodes that are under management by Chef include:

-- Chef Client: A chef-client is an agent that runs locally on every node that is under management by Chef. When a chef-client is run, it will perform all of the steps that are required to bring the node into the expected state, including:
         
            * Registering and authenticating the node with the Chef server
            * Building node object
            * Synchronizing cookbooks
            * Compiling the resource collection by loading each of the required cookbooks, including recipes, attributes, and all other dependencies.
            * Taking the appropriate and required actions to configure the node
            * Looking for exceptions and notifications, handling each as required
            * RSA public key-pairs are used to authenticate the chef-client with the Chef server every time a chef-client needs access to data that is stored on the Chef server. This prevents any node from accessing data that it shouldn’t and it ensures that only nodes that are properly registered with the Chef server can be managed.

-- Ohai: Ohai is a tool that is used to detect attributes on a node, and then provide these attributes to the chef-client at the start of every chef-client run. Ohai is required by the chef-client and must be present on a node. (Ohai is installed on a node as part of the chef-client install process.)

The types of attributes Ohai collects include:
 
 Platform details
 
 Network usage
 
 Memory usage
 
 CPU data
 
 Kernel data
 
 Host names
 
 Fully qualified domain names

#*Manage Nodes*

- There are several ways to manage nodes directly, including by using knife, the Chef management console add-on for the Chef server, or by using command-line tools that are specific to chef-client.
- knife can be used to create, edit, view, list, tag, and delete nodes.
- knife plug-ins can be used to create, edit, and manage nodes that are located on cloud providers.
- The Chef management console add-on can be used to create, edit, view, list, tag, and delete nodes. In addition, node attributes can be modified and nodes can be moved between environments.
The chef-client can be used to manage node data using the command line and JSON files. Each JSON file contains a hash, the elements of which are added as node attributes. In addition, the run_list setting allows roles and/or recipes to be added to the node.
- chef-solo can be used to manage node data using the command line and JSON files. Each JSON file contains a hash, the elements of which are added as node attributes. In addition, the run_list setting allows roles and/or recipes to be added to the node.
- The command line can also be used to edit JSON files and files that are related to third-party services, such as Amazon EC2, where the JSON files can contain per-instance metadata that is stored in a file on-disk and then read by chef-solo or chef-client as required.

#*Node Objects*
- For the chef-client, two important aspects of nodes are groups of attributes and run-lists. An attribute is a specific piece of data about the node, such as a network interface, a file system, the number of clients a service running on a node is capable of accepting, and so on. A run-list is an ordered list of recipes and/or roles that are run in an exact order. The node object consists of the run-list and node attributes, which is a JSON file that is stored on the Chef server. The chef-client gets a copy of the node object from the Chef server during each chef-client run and places an updated copy on the Chef server at the end of each chef-client run.
- An attribute is a specific detail about a node. Attributes are used by the chef-client to understand:

     -- The current state of the node
     -- What the state of the node was at the end of the previous chef-client run
     -- What the state of the node should be at the end of the current chef-client run

- Attributes are defined by:

     -- The state of the node itself.
     -- Cookbooks (in attribute files and/or recipes)
     -- Roles
     -- Environments
 
- During every chef-client run, the chef-client builds the attribute list using:
 
     --  Data about the node collected by Ohai
     -- The node object that was saved to the Chef server at the end of the previous chef-client run
     -- The rebuilt node object from the current chef-client run, after it is updated for changes to cookbooks (attribute            files and/or recipes), roles, and/or environments, and updated for any changes to the state of the node itself

- After the node object is rebuilt, all of attributes are compared, and then the node is updated based on attribute precedence. At the end of every chef-client run, the node object that defines the current state of the node is uploaded to the Chef server so that it can be indexed for search.

- Attributes

 An attribute is a specific detail about a node, such as an IP address, a host name, a list of loaded kernel modules, the version(s) of available programming languages that are available, and so on. 
 An attribute may be unique to a specific node or it can be identical across every node in the organization. Attributes are most commonly set from a cookbook, by using knife, or are retrieved by Ohai from each node prior to every chef-client run. All attributes are indexed for search on the Chef server.
