# Chef Server

- The Chef server acts as a hub for configuration data. The Chef server stores cookbooks, the policies that are applied to nodes, and metadata that describes each registered node that is being managed by the chef-client. Nodes use the chef-client to ask the Chef server for configuration details, such as recipes, templates, and file distributions. The chef-client then does as much of the configuration work as possible on the nodes themselves (and not on the Chef server). This scalable approach distributes the configuration effort throughout the organization.

- The Chef server can scale to the size of any enterprise and is sometimes referred to as Erchef.

- The following diagram shows the various components that are part of a Chef server deployment and how they relate to one another.
 
 ![alt text](https://github.com/pkdevaraj/Presentations/blob/a20c76968d2be8e27609c46c27c09d27f57a13d5/Chef%20Images/Chef_server.PNG "Chef_Server")
 
- Components and their Description:
 
- Clients: 	The Chef server is accessed primarily by nodes that are under management by Chef, as the chef-client runs occur. It is also accessed by individuals who maintain cookbooks and policy that is stored on the Chef server, typically from a workstation. And also by individual users with credentials to Chef server components, such as the Chef management console.

- Load Balancer: Nginx is an open-source HTTP and reverse proxy server that is used as the front-end load balancer for the Chef server. All requests to the Chef server API are routed through Nginx.

- Chef Manage: chef-server-webui is a Ruby on Rails 3.0 application that hosts the web interface for the Chef server.
The Chef management console uses the Chef server API for all communication to the Chef server.

- Chef Server: Erchef is a complete rewrite of the core API for the Chef server, which allows it to be faster and more scalable than previous versions. The API itself is still compatible with the original Ruby-based Chef server, which means that cookbooks and recipes that were authored for the Ruby-based Chef server will continue to work on the Erlang-based Chef server. The chef-client is still written in Ruby.

- Bookshelf: Bookshelf is used to store cookbook content—files, templates, and so on—that have been uploaded to the Chef server as part of a cookbook version. Cookbook content is stored by content checksum. If two different cookbooks or different versions of the same cookbook include the same file or template, Bookshelf will store that file only once. The cookbook content managed by Bookshelf is stored in flat files and is separated from the Chef server and search index repositories.
All cookbooks are stored in a dedicated repository.

- Message Queues	
Messages are sent to the search index using the following components:
    RabbitMQ is used as the message queue for the Chef server. All items that will be added to the search index repository are first added to a queue.

     chef-expander is used to pull messages from the RabbitMQ queue, process them into the required format, and then post them to chef-solr for indexing.

     chef-solr wraps Apache Solr and exposes its REST API for indexing and search.

All messages are added to a dedicated search index repository.

##**Capacity Planning**

- This section provides guidance for capacity planning and how to choose the right configuration–standalone, high availability, or tiered–for the Chef server. This section provides guidance and not hard/fast rules. This is because some requests to the Chef server API are more computationally expensive than others. In general, it’s better to start small and then scale the Chef server as needed. Premature optimization can hinder more than help because it may introduce unnecessary complexity.

##**Scaling the Chef Server**

- The Chef server itself is highly scalable. A single virtual machine running the Chef server can handle requests for many thousands of nodes. As the scale increases, it’s a straightforward process to expand into a tiered front-end, back-end architecture with horizontally scaled front-ends to relieve pressure on system bottlenecks.

- That said, it’s best to isolate failure domains with their own Chef server, rather than trying to run every node in an infrastructure from a single central, monolithic Chef server instance/cluster.

- For instance, if there are West coast and East coast data centers, it is best to have one Chef server instance in each datacenter. Deploys to each Chef server can be synchronized upstream by CI software. The primary limiting bottleneck for Chef server installations is almost always input/output operations per second (IOPS) performance for the database filesystem.

##**CCRs/min**

- The key unit of measure for scaling the Chef server is the number of chef-client runs per minute: CCRs/min. For example, 500 nodes set to check in every 30 minutes is equivalent to 16.66 CCRs/min.

- Typically, the Chef server does not require a high availability or tiered topology until the number of CCRs/min is higher than 333/min (approximately 10k nodes).

- While synthetic benchmarks should be taken with a grain of salt, as they don’t typically represent real-world performance, internal synthetic benchmarks at Chef have seen a standalone Chef server installed on a c3.2xlarge Amazon Web Services (AWS) instance handle more than 1,000 CCRs/min (30k nodes).
