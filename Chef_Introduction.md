#Overview of CHEF

Chef is a configuration management tool written in Ruby and Erlang. It uses a pure-Ruby, domain-specific language (DSL) for writing system configuration "recipes".

Chef is a powerful automation platform that transforms complex infrastructure into code, bringing your servers and services to life. Whether you’re operating in the cloud, on-premises, or a hybrid, Chef automates how applications are configured, deployed, and managed across your network, no matter its size.

The user writes "recipes" that describe how Chef manages server applications and utilities (Apache HTTP Server,MySQL etc) and how they are configured. These recipes describe a series of resources that should be in a particular state.

State contains information on packages that should be installed, services that should be running, or files that should be written.

Chef is built with features for achieving desired state, centralized modeling of IT infrastructure, and resource primitives that serve as building blocks. These very same concepts allow Chef to handle the most difficult infrastructure challenges on the planet. Anything that can run the chef-client can be managed by Chef.

Chef can run in client/server mode or in a standalone configuration named "chef-solo". In client/server mode, the Chef client sends various attributes about the node to the Chef server. The server uses Solr to index these attributes and provides an API for clients to query this information. Chef recipes query the attributes and use the resulting data to configure the node.

#Components of CHEF




