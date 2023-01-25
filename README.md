Reference - https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/#apply-and-verify

It creates wordpress deployment and mysql db statfulset. The wordpress app is accessible from outside via a loadbalancer resource service


   az login
   az account set --subscription 7ecaa18c-98ad-4f96-b828-5082a224f4c6
   az aks get-credentials --resource-group srikanth-ak_group --name srikanth-aks
   kubectl
   cd multi-tier-app-k8s/
   kubectl get pods
   kubectl get deployments
   kubectl get service
   wget https://kubernetes.io/examples/application/wordpress/mysql-deployment.yaml
   wget https://kubernetes.io/examples/application/wordpress/wordpress-deployment.yaml
  vim mysql-deployment.yaml 
  vim wordpress-deployment.yaml 
  cat <<EOF >./kustomization.yaml
secretGenerator:
- name: mysql-pass
  literals:
  - password=mysql_password
EOF

  cat <<EOF >>./kustomization.yaml
resources:
  - mysql-deployment.yaml
  - wordpress-deployment.yaml
EOF

  kubectl apply -k ./
# k8s-container
