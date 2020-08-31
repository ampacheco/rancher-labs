

az group create -l eastus -n rancher-lab--rg
az configure --defaults location=eastus group=rancher-lab--rg

az network vnet create --resource-group RancherK3sResourceGroup --name RancherK3sVnet --subnet-name RancherK3sSubnet

az network public-ip create --resource-group RancherK3sResourceGroup --name RancherK3sPublicIP1 --sku standard

az network public-ip create --resource-group RancherK3sResourceGroup --name RancherK3sPublicIP2 --sku standard

az network nsg create --resource-group RancherK3sResourceGroup --name RancherK3sNSG1

az network nsg rule create -g RancherK3sResourceGroup --nsg-name RancherK3sNSG1 -n NsgRuleSSH --priority 100 \
--source-address-prefixes '*' --source-port-ranges '*' \
--destination-address-prefixes '*' --destination-port-ranges 22 --access Allow \
--protocol Tcp --description "Allow SSH Access to all VMS."
