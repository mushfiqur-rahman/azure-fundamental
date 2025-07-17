# [Unit 9 of 14 - Exercise](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/9-exercise-configure-network-access) - Configure network access

# Azure VM HTTP Access Setup Guide

This guide demonstrates how to retrieve the public IP of a virtual machine, configure network security group (NSG) rules, and test HTTP access using `curl`.

---

### 📌 1. Get the Public IP of the VM

```bash
IPADDRESS="$(az vm list-ip-addresses \
  --resource-group "learn-d38d3411-0b33-4628-ab4b-a6961289da3a" \
  --name my-vm \
  --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
  --output tsv)"

```

### 🧪 2. Test HTTP Access to the VM

```bash
curl --connect-timeout 5 http://$IPADDRESS
```

Expected output (if HTTP access is not yet enabled):

```bash
curl: (28) Connection timed out after 5002 milliseconds

```

### 📥 3. Verify the Public IP

```bash
echo $IPADDRESS
```

Example output:

```bash
20.66.110.132
```

### 🔍 4. Check Existing NSGs

```bash
az network nsg list \
  --resource-group "learn-d38d3411-0b33-4628-ab4b-a6961289da3a" \
  --query '[].name' \
  --output tsv

```

Example output:

```bash
my-vmNSG

```

### 5. Check Existing NSG Rules

```bash
az network nsg rule list \
  --resource-group "learn-d38d3411-0b33-4628-ab4b-a6961289da3a" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table

```

Example output:

```bash
Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow

```

### 6. Add NSG Rule to Allow HTTP (Port 80)

```bash
az network nsg rule create \
  --resource-group "learn-d38d3411-0b33-4628-ab4b-a6961289da3a" \
  --nsg-name my-vmNSG \
  --name allow-http \
  --protocol tcp \
  --priority 100 \
  --destination-port-range 80 \
  --access Allow
```

### 7. Verify NSG Rules Again

```bash
az network nsg rule list \
  --resource-group "learn-d38d3411-0b33-4628-ab4b-a6961289da3a" \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table

```

Expected output:

```bash
Name               Priority    Port    Access
-----------------  ----------  ------  --------
default-allow-ssh  1000        22      Allow
allow-http         100         80      Allow
```

### 🌐 8. Test HTTP Access Again

```bash
curl --connect-timeout 5 http://$IPADDRESS
```

Expected output:

```bash
<html><body><h1>Hello from my-vm</h1></body></html>
```

### Open browser and hit the IP to see html page
