# kubernets dashboard deployment
Clone the git project with below URL

https://github.com/nagarajcapgemini/kubernets.git/


1. Creating dashboard namespace using below.

   Kubectl create ns dashboard

2. Deploy dashboard using below.

  Kubectl apply -f dashboard_deployement.yaml -n dashboard

3. Deploy dashboard proxy and dashboard proxy service for upsteam.

  Kubectl apply -f dashboard-proxy-Deployment.yaml -n dashboard

  Kubectl apply -f dashboard-proxy-svc.yaml -n dashboard

4. Deploying admin and read-only user access for Dashboard

  kubectl apply -f rbac.yaml -n dashboard

  kubectl apply -f sa-cluster-admin.yaml -n dashboard

  kubectl apply -f service-account.yaml -n dashboard

  kubectl apply -f dashboard-read-only.yaml -n dashboard

  kubectl apply -f dashboard-admin.yaml -n dashboard

5. Deploying ingress Route with certificate termination for Dashboard

  kubectl apply -f dashboard_ingressroute_middleware.yaml -n dashboard

6. Get readonly and admin users token using below tokens.

  kubectl -n dashboard describe secret $(kubectl -n dashboard get secret | grep admin-user | awk '{print $1}')

  kubectl -n dashboard describe secret $(kubectl -n dashboard get secret | grep read-only-user | awk '{print $1}')
