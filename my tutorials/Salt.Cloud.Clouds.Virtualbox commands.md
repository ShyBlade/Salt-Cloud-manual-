# salt.Cloud.Clouds.virtualbox commandlist


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
