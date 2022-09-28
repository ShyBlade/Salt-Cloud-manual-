# salt.Cloud.Clouds.virtualbox commandlist

## salt.cloud.clouds.virtualbox.start(name, call=None)
Start a machine.
	

## salt.cloud.clouds.virtualbox.stop(name, call=None)
Stop a running machine


## salt.cloud.clouds.virtualbox.create(vm_info)
Creates a virtual machine from the given VM information

This is what is used to request a virtual machine to be created by the cloud provider, wait for it to become available, and then (optionally) log in and install Salt on it.


## salt.cloud.clouds.virtualbox.destroy(name, call=None)
This function irreversibly destroys a virtual machine on the cloud provider. Before doing so, it should fire an event on the Salt event bus.

The tag for this event is salt/cloud/<vm name>/destroying. Once the virtual machine has been destroyed, another event is fired. The tag for that event is salt/cloud/<vm name>/destroyed.

Dependencies:
list_nodes

## salt.cloud.clouds.virtualbox.get_configured_provider()
Return the first configured instance.

  
## salt.cloud.clouds.virtualbox.list_nodes(kwargs=None, call=None)
This function returns a list of nodes available on this cloud provider, using the following fields:

id (str) image (str) size (str) state (str) private_ips (list) public_ips (list)

No other fields should be returned in this function, and all of these fields should be returned, even if empty. The private_ips and public_ips fields should always be of a list type, even if empty, and the other fields should always be of a str type. This function is normally called with the -Q option.
           
  
       salt-cloud -Q
  
  
## salt.cloud.clouds.virtualbox.list_nodes_full(kwargs=None, call=None)
All information available about all nodes should be returned in this function. The fields in the list_nodes() function should also be returned, even if they would not normally be provided by the cloud provider.

This is because some functions both within Salt and 3rd party will break if an expected field is not present. This function is normally called with the -F option:
	
      salt-cloud -F
	
	
## salt.cloud.clouds.virtualbox.list_nodes_select(call=None)
Return a list of the VMs that are on the provider, with select fields
	
## salt.cloud.clouds.virtualbox.map_clonemode(vm_info)
Convert the virtualbox config file values for clone_mode into the integers the API requires
	
	
## salt.cloud.clouds.virtualbox.show_image(kwargs, call=None)
Show the details of an image 
	

	
	
	
	
