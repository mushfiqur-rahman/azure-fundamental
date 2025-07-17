# [Unit 9 of 14 - Exercise](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/9-exercise-configure-network-access) - Configure network access

Before using `curl`, we need to open port. Port open command

```bash
az vm open-port \
  --resource-group "learn-57256d73-61a0-4aa4-96ef-2e9103ce51c7" \
  --name my-vm \
  --port 80

```

> N.B Don't copy paste. **resource-group** name should be your's. Here, I am using mine.
