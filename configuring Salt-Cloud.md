# Configuring Salt cloud 

## Pre-requisites

- 1 host with salt-master software installed in azure 

## installing Salt-Cloud software 
   
   for managing puproses it is better to install salt-master on the salt-master 
   you can install Salt-Cloud on ubuntu with the following commands: 
   
       sudo add-apt-repository ppa:saltstack/salt
       sudo apt-get update
       sudo apt-get install salt-cloud
       
 ## adding cloud provider to salt-Cloud  
   
 Salt-Cloud is Capable of connecting to multiple cloud providers. in this tutorial we are going to try to connect to azure.
  
  
  after installing salt cloud uncomment the following lines from /etc/salt/master:
             file_roots:
              base:
            -/srv/salt
            
      
  next step create the folder /srv/salt:
      mkdir /srv/salt
    
 
 in order to use salt-cloud and connect to azure we need to create an azure provider configuration. open /etc/salt/cloud.providers.d/azure.conf and add the following lines:
       
     my-azure-provider:
     driver: azure
     subscription_id: 332b184f-faaf-455d-a1d8-0110e1131ab
     certificate_path: /etc/salt/azure.pem

     minion:
    master: mysaltmaster.eastus.cloudapp.azure.com
    
   you need to adjust this configuration file to your case (subscription id,master DNS)
    
   
   ## creating Cer. and pem. file and uploading to azure 
   
     you need to create the .pem file. Execute the following command on your master VM: 
    
   openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout /etc/salt/azure.pem -out /etc/salt/azure.pem
  
      create the cer file using the follwing command:
      openssl x509 -inform pem -in /etc/salt/azure.pem -outform der -out /etc/salt/azure.cer 
    
    
 to allow saltstack to manage Azute resources we need to uplaod the .cer file to the azure subscription manager. Find this in the list of all services then click on your subscription id and choose to upload a new certificate 
     
    
    
    
    
    
    
    
    
    
    
    
 
