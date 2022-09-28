# importing digitalcloud module for Salt-Cloud


A salt cloud provider that lets you use virtualbox on your machine and act as a cloud.


## Dependencies
- digitalocean website account 
- DigitalCloud personal access token
- SSH keys
- python library requests https://pypi.org/project/requests/ 



## making the personal access token 

before we can import the cloud driver we have to make a access token first. 

go to the digitalocean website https://docs.digitalocean.com/reference/api/create-personal-access-token/ and follow these steps to create a access token


## making a ssh key pair

now that the access token is created it is time to create ssh keys. 

follow the steps on https://docs.digitalocean.com/products/droplets/how-to/add-ssh-keys/create-with-openssh/ to create the keys



## importing the module 

go to the /etc/salt/cloud.providers or any file in the  /etc/salt/cloud.providers.d/ directory and create a vim file and put in the following commands in it:
      
    # Note: This example is for /etc/salt/cloud.providers or any file in the
    # /etc/salt/cloud.providers.d/ directory.
    my-digital-ocean-config:
      personal_access_token: xxx
      ssh_key_file: /path/to/ssh/key/file
      ssh_key_names: my-key-name,my-key-name-2
      driver: digitalocean
      :depends: requests
      """
      
      
      



     
