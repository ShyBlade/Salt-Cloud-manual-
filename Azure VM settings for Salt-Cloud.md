## azure VM settings

make sure your Azure vm has the following settings when trying Salt-Cloud


   # The virtual network
   az network vnet subnet create \
  --name minionSubnet \
   --address-prefix 10.0.2.0/24 \
  --vnet-name saltVnet \
  --resource-group saltGroup

# The network security group
az network nsg create \
    --resource-group saltGroup \
    --name minionSecurityGroup 

# The network security group rule
az network nsg rule create \
    --resource-group saltGroup \
    --nsg-name minionSecurityGroup \
    --name minionSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow

# The virtual NIC 
 az network nic create \
    --resource-group saltGroup \
    --name minionNIC \
    --subnet minionSubnet \
    --private-ip-address 10.0.2.4 \
    --vnet-name saltVnet  
