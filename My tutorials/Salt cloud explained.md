# Salt cloud explained 


Salt Cloud is a configuration management tool that allows users to provision systems on cloud hosts or hypervisors. During installation, Salt Cloud installs Salt on all provisioned systems by default. This enables the user to put systems into the desired state during provisioning.


Salt Cloud:

- Helps gather information on your systems and manage their lifecycle through a Command Line Interface (CLI).
- Supports Linode as a provider out of the box. You do not have to install any additional plugins.



Salt Cloud provides a powerful interface to interact with cloud hosts. This interface is tightly integrated with Salt, and new virtual machines are automatically connected to your Salt master after creation.

Since Salt Cloud is designed to be an automated system, most configuration is done using the following YAML configuration files.


 
## installing Salt-Cloud software 

Pre-requisites:

- 1 host with salt-master software

   
   for managing puproses it is better to install salt-master on the salt-master 
   you can install Salt-Cloud on ubuntu with the following commands: 
   
       sudo add-apt-repository ppa:saltstack/salt
       sudo apt-get update
       sudo apt-get install salt-cloud
       
