# Add stable to helm

```sh
helm repo add stable https://charts.helm.sh/stable

helm repo search stable

# Plane to pull the new configuration of a service 
helm install repo stable/<chartname> <releasename>


# helm search repo stable/mysql 
# helm install repo stable/mysql 
# helm pull stable/mysql

helm pull <chartname>
  
helm package <chartname>

helm uninstall RELEASE_NAME
```
