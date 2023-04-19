# kubernetes-dashboard



# Deploying the Dashboard UI 
The Dashboard UI is not deployed by default. To deploy it, run the following command:

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml



<<< this command will create a namespace with the name of kubernetes-dashboard and deploy every thing inside it >>>
 the kubernetes dashboard service by default is clusterip edit that to nodeport to access in the browser
 
 
 # use this command to edit the service
 kubectl edit service/kubernetes-dashboard -n kubernetes-dashboard
 
 type: NodePort
 
<<-----------open browser and copy the publicip and nodeport portno paste it in new tab-------------------------->>

give https://<publicip:nodeport portno>

click on < continue unsafe >

# now you can see kubernetes dashboard but you need to provide the token to login 


# Creating a Service Account and cluster role binding 

# make a file service-account.yml and paste below content

---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
  
  

# use this command to describe the service accont 

kubectl describe sa kubernetes-dashboard -n kubernetes-dashboard


# use this command to get the token from the secret 

kubectl describe secret kubernetes-dashboard-token-wvdnm -n kubernetes-dashboard




<<< copy the token and paste it in the kubernetes dashboard token text feild  >>


# yes u did it .. now you can access the kubernetes dashboard 
