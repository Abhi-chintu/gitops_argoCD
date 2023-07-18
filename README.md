# gitops_argoCD

<img width="752" alt="image" src="https://github.com/Abhi-chintu/gitops_argoCD/assets/94033251/a5e3fe05-f2ad-4d46-81b3-597646dd8871">
------------------------------------------------------------------------------------------------------------------------------------

<img width="875" alt="image" src="https://github.com/Abhi-chintu/gitops_argoCD/assets/94033251/2ac2454e-1ee5-4ab9-949d-5b85a3578fc2">

    Repo server: which is having comminication with the git repositarty
    Application Controller: Which is having communication with the kubernetes.
      These two gets the information with the two entities and try to compare the state.
      Application Controller communicates with Repo server and try to see state in git and kubernetes is same or what.
    API server: Which is used for UI/CLI authentication
    DES: which adds SSO cabilities 
    Redis: used for caching. Because these use statefull sets. So need to cache the information.

1. Install Argo CD:
All the components of Argo CD can be installed using a manifest provided by the Argo Project. Note the outputs below that you should see.

       kubectl create namespace argocd
2. Apply the manifest to install required Argo CD kubernetes objects
   
       kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
3. Download With Curl

        curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
        sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
        rm argocd-linux-amd64

4. Access the argoCd app via Load Balancer

        kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

4.1 Accessing the application using nodeport 

        kubectl get svc -n argocd
        kubectl edit svc argocd-server -n argocd

<img width="269" alt="image" src="https://github.com/Abhi-chintu/gitops_argoCD/assets/94033251/2cabe367-c2f2-4778-bf36-767bf972da59">

4.2 Open the ports in worker node and check in browser to see argocd in UI

5. To list all the clusters
 
        kubectl config get-contexts -o name

6. Login to Argocd UI

       kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
       echo <password> | base64 --decode

7. Connect your git-repo to the argocd application in UI
8. Apply application.yaml file in ec2-instance

       kubectl apply -f application.yaml 
       

        

