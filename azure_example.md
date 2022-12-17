#!/bin/bash

# Modify for your environment.
# ACR_NAME: The name of your Azure Container Registry
# SERVICE_PRINCIPAL_NAME: Must be unique within your AD tenant
#ACR_NAME=<container-registry-name>
ACR_NAME=acrdemo2ss
SERVICE_PRINCIPAL_NAME=acr-sp-demo

# Obtain the full registry ID for subsequent command args
ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME --query id --output tsv)

# Create the service principal with rights scoped to the registry.
# Default permissions are for docker pull access. Modify the '--role'
# argument value as desired:
# acrpull:     pull only
# acrpush:     push and pull
# owner:       push, pull, and assign roles
SP_PASSWD=$(az ad sp create-for-rbac --name http://$SERVICE_PRINCIPAL_NAME --scopes $ACR_REGISTRY_ID --role acrpull --query password --output tsv)
SP_APP_ID=$(az ad sp show --id http://$SERVICE_PRINCIPAL_NAME --query appId --output tsv)

# Output the service principal's credentials; use these in your services and
# applications to authenticate to the container registry.
echo "Service principal ID: $SP_APP_ID"
echo "Service principal password: $SP_PASSWD"


=============================================


# Template
kubectl create secret docker-registry <secret-name> \
    --namespace <namespace> \
    --docker-server=<container-registry-name>.azurecr.io \
    --docker-username=<service-principal-ID> \
    --docker-password=<service-principal-password>

# Replace
kubectl create secret docker-registry acrdemo2ss-secret \
    --namespace default \
    --docker-server=acrdemo2ss.azurecr.io \
    --docker-username=80beacfe-7176-4ff5-ad22-dbb15528a9a8 \
    --docker-password=0zjUzGzSx3_.xi1SC40VcWkdVyl8Ml8QNj    

# List Secrets
kubectl get secrets    