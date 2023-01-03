# Helm CLI instructions 

helm repo add stable https://charts.helm.sh/stable

helm repo add brigade https://brigadecore.github.io/charts
# brigade" has been added to your repositories
helm search repo mysql

helm install repo stable/<chartname> <releasename>
  
helm pull <chartname>
  
helm package <chartname>

helm uninstall RELEASE_NAME