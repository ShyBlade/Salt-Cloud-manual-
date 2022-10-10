# Salt cloud explained 


Salt Cloud is a configuration management tool that allows users to provision systems on cloud hosts or hypervisors. During installation, Salt Cloud installs Salt on all provisioned systems by default. This enables the user to put systems into the desired state during provisioning.


Salt Cloud:

- Helps gather information on your systems and manage their lifecycle through a Command Line Interface (CLI).
- Supports Linode as a provider out of the box. You do not have to install any additional plugins.



Salt Cloud provides a powerful interface to interact with cloud hosts. This interface is tightly integrated with Salt, and new virtual machines are automatically connected to your Salt master after creation.

Since Salt Cloud is designed to be an automated system, most configuration is done using the following YAML configuration files.



## how the configuration works 

Salt Cloud provides an interface to interact with cloud Hosts. This interface is intergrated with salt, and new virtual machines are automatically connected to your Salt master after creation.

Since salt Cloud is designed to be a automated system, most configuration is done using the follwing YAML configuration files.

- /etc/salt/cloud: The main configuration file, contains global settings that apply to all cloud hosts
- /etc/salt/cloud.providers.d/*.conf: Contains settings that configure a specific cloud host, such as credentials, region settings, and so on. Since configuration varies significantly between each cloud host, a separate file should be created for each cloud host. In Salt Cloud, a provider is synonymous with a cloud host (Amazon EC2, Google Compute Engine, Rackspace, and so on).

- /etc/salt/cloud.profiles.d/*.conf: Contains settings that define a specific VM type. A profile defines the systems specs and image, and any other settings that are specific to this VM type. Each specific VM type is called a profile, and multiple profiles can be defined in a profile file. Each profile references a parent provider that defines the cloud host in which the VM is created (the provider settings are in the provider configuration explained above). Based on your needs, you might define different profiles for web servers, database servers, and so on.


 
## installing Salt-Cloud software 

Pre-requisites:

- 1 host with salt-master software

   
   for managing puproses it is better to install salt-master on the salt-master 
   you can install Salt-Cloud on ubuntu with the following commands: 
   
       sudo add-apt-repository ppa:saltstack/salt
       sudo apt-get update
       sudo apt-get install salt-cloud
       
