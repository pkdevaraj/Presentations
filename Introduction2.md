## CHEF - CONFIGURATION MANAGEMENT TOOL


###Configuration Management 

Configuration management (CM) is a systems engineering process for establishing and maintaining consistency of a product's performance, functional and physical attributes with its requirements, design and operational information throughout its life.

CM is the practice of handling changes systematically in an organized way so that a system maintains its integrity over time. This system implements the policies, procedures, techniques, and tools that are required to manage, evaluate proposed changes, track the status of changes and support documentation as the system changes.

Configuration Management when applied over the life cycle of a system, provides visibility and control of its performance. It verifies if a system performs as intended, and is identified and documented in sufficient detail to support its projected life cycle.

###Configuration Management Tools
There are various tools available for configuration management and few of them are listed below.

- #####Ansible

    Combines multi-node deployment, ad-hoc task execution, and configuration management in one package. Manages nodes over       SSH and requires python to be installed on them. Modules work over JSON and standard output and can be written in any        language. Uses YAML to express reusable descriptions of systems.
    
- #####Bcfg2

    Software to manage the configuration of a large number of computers using a central configuration model and the              client–server model. The enables reconciliation between clients' state and the central configuration                         specification at any time.
    
- #####Cdist

    Cdist is a zero dependency configuration management system. It requires only ssh on the target host, which is usually        enabled on all Unix-like machines. Only the administration host needs to have Python 3.2 installed.

- #####Chef
    Chef is a configuration management tool written in Ruby, and uses a pure Ruby DSL for writing configuration "recipes".       These recipes contain resources that should be put into the declared state. Chef is generally used as a client–server        tool.

- #####Puppet
    Puppet consists of a custom declarative language to describe system configuration, distributed using the client–server       paradigm, and a library to realize the configuration. The resource abstraction layer enables administrators to describe      the configuration in high-level terms,such as users, services and packages. Puppet will then ensure the server's state       matches the description.

- #####Rex
    Rex is a remote execution system with integrated configuration management and software deployment capabilities. The admin     provides configuration instructions via so-called Rexfiles. They are written in a small DSL but can also contain             arbitrary Perl.

There are many more configuration management tools available and only few are listed above. To learn more [click here](https://en.wikipedia.org/wiki/Comparison_of_open-source_configuration_management_software)


[**NEXT**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_Introduction.md)     

[**BACK TO CONTENTS**](https://github.com/pkdevaraj/Presentations/blob/gh-pages/Chef_Readme.md)

