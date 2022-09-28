# Use Salt with VirtualBox

## Dependencies 
- Salt-Cloud Software installed


- The virtualbox module  requires the Virtualbox SDK which is contained in a virtualbox installation from

https://www.virtualbox.org/wiki/Downloads


## configuration 
The Virtualbox cloud module needs to use the virtualbox driver. Virtualbox will be run as the running user.

go into /etc/salt/cloud.providers or create directory /etc/salt/cloud.profiles.d/virtualbox.conf and put in the following: 


      virtualbox-config:
      driver: virtualbox
      
      
  ## configuring the profiles 
  Set up an initial profile at /etc/salt/cloud.profiles or /etc/salt/cloud.profiles.d/virtualbox.conf
          
          virtualbox-test:
           provider: virtualbox-config
           clonefrom: VM_to_clone_from
           
           # Optional
           power_on: True
            deploy: True
            ssh_username: a_username
            password: a_password
           sudo: a_username
           sudo_password: a_password
           # Example minion config
           minion:
           master: localhost
            make_master: True
            
  
  clonefrom Mandatory
      Enter the name of the VM/template to clone from 
      so far only machines can only be cloned and automatically provisioned by Salt-Cloud
      
      
  ## provisioning
  in order to provison when creating a new VM "power_on" and "deploy" have to be True
  
  Furthermore to connect to the VM ssh_username and password will have to be set.
   
   sudo and sudo_password are the credentials for getting root access in order to deploy salt.
   
   
   
 actions


 start
Attempt to boot a VM by name. VMs should have unique names in order to boot the correct one.

stop
Attempt to stop a VM. This is akin to a force shutdown or 5 second press.


 # functions
show_image
Show all available information about a VM given by the image parameter

     $ salt-cloud -f show_image virtualbox image=my_vm_name  
    
    
    
  
