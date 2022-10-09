# salt Cloud VM commands 


To create 4 VMs named web1, web2, db1, and db2 from specified profiles:


salt-cloud -p fedora_rackspace web1 web2 db1 db2
To read in a map file and create all VMs specified therein:

salt-cloud -m /path/to/cloud.map
To read in a map file and create all VMs specified therein in parallel:

salt-cloud -m /path/to/cloud.map -P
To delete any VMs specified in the map file:

salt-cloud -m /path/to/cloud.map -d
To delete any VMs NOT specified in the map file:

salt-cloud -m /path/to/cloud.map -H
To display the status of all VMs specified in the map file:

salt-cloud -m /path/to/cloud.map -Q
SEE ALSO
