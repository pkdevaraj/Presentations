##**NODES**

- A node is any machine-physical, virtual, cloud, network device, etc, that is under management by Chef.
- The types of nodes that can be managed by Chef are:
- Server: A physical node is typically a server or a virtual machine, but it can be any active device attached to a network that is capable of sending, receiving, and forwarding information over a communications channel. In other words, a physical node is any active device attached to a network that can run a chef-client and also allow that chef-client to communicate with a Chef server.

- Cloud: A cloud-based node is hosted in an external cloud-based service, such as Amazon Web Services (AWS), OpenStack, Rackspace, Google Compute Engine, or Microsoft Azure. Plugins are available for knife that provide support for external cloud-based services. knife can use these plugins to create instances on cloud-based services. Once created, the chef-client can be used to deploy, configure, and maintain those instances.

- Virtual Machine: A virtual node is a machine that runs only as a software implementation, but otherwise behaves much like a physical machine.

- Network Device: A network node is any networking device—a switch, a router—that is being managed by a chef-client, such as networking devices by Juniper Networks, Arista, Cisco, and F5. Use Chef to automate common network configurations, such physical and logical Ethernet link properties and VLANs, on these devices.

- Containers: Containers are an approach to virtualization that allows a single operating system to host many working configurations, where each working configuration—a container is assigned a single responsibility that is isolated from all other responsibilities. Containers are popular as a way to manage distributed and scalable applications and services.
