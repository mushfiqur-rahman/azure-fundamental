## After applied the 3.14 [command](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/3-exercise-create-azure-virtual-machine), you need to use below command

```bash
mushfiqur-rahman [ ~ ]$ az vm show \
  --resource-group "learn-57256d73-61a0-4aa4-96ef-2e9103ce51c7" \
  --name my-vm \
  --show-details \
  --query publicIps \
  --output tsv
20.245.142.194
```

```bash
mushfiqur-rahman [ ~ ]$ ssh azureuser@20.245.142.194
```

```bash
azureuser@my-vm:~$ man sudo_root
```

```bash
azureuser@my-vm:~$ sudo su
```

```bash
root@my-vm:/home/azureuser# sudo apt-get update
root@my-vm:/home/azureuser# sudo add-apt-repository main
root@my-vm:/home/azureuser# sudo add-apt-repository universe
root@my-vm:/home/azureuser# sudo add-apt-repository restricted
root@my-vm:/home/azureuser# sudo add-apt-repository multiverse
root@my-vm:/home/azureuser# sudo apt-get install -y nginx
```

```bash
root@my-vm:/home/azureuser# echo "<html><body><h2>Welcome to Azure! My name is $(hostname).</h2></body></html>" | sudo tee -a /var/www/html/index.html
<html><body><h2>Welcome to Azure! My name is my-vm.</h2></body></html>
root@my-vm:/home/azureuser# cat /var/www/html/index.html
<html><body><h2>Welcome to Azure! My name is my-vm.</h2></body></html>
<html><body><h2>Welcome to Azure! My name is my-vm.</h2></body></html>
```
