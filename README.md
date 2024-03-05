# argocd-app-deployment
Deploy Application using Argo CD for GitOps continuous delivery and Apps lifecycle.


## Description
This repository provides a demonstration of how to install Argo CD in a Kubernetes cluster and deploy an application using Argo CD

## Prerequisites
Before you begin, ensure you have the following prerequisites:

- Access to a Kubernetes cluster
- kubectl command-line tool installed and configured to access your cluster

## Completion steps
- 1. Install [Argo CD](https://argo-cd.readthedocs.io/en/stable/getting_started/)
- 2. Create a sample application and sync it.


### Installation
To install Argo CD in your Kubernetes cluster, follow these steps:

- 1. Apply the Argo CD manifests using the following command:
     
bash```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
```
 
- 2. Wait for all Argo CD pods to be in a Running state:
bash```
kubectl wait --for=condition=Ready pod -l app.kubernetes.io/name=argocd-server -n argocd
```

- 3. Retrieve the Argo CD server password:
bash```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode
```

- 4. Access the Argo CD UI by port-forwarding the Argo CD server service to your local machine:
bash```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

> Then, open your browser and navigate to https://localhost:8080 and log in using the username admin and the password retrieved in step 3.

### Deploying an Application
To deploy an application using Argo CD, follow these steps:

- Log in to the Argo CD UI as admin with the password retrieved during installation.

- Click on New App in the UI.

- Fill in the application details including the Git repository URL, target cluster, and namespace.

- Click on Sync to deploy the application.

- Monitor the application deployment status in the Argo CD UI.

### Cleanup
To uninstall Argo CD from your Kubernetes cluster, simply delete the Argo CD namespace:

bash```
kubectl delete namespace argocd

## Conclusion

In summary, Argo CD offers a robust and user-friendly solution for deploying applications in Kubernetes clusters. With its intuitive UI and declarative approach, managing application deployments becomes seamless and efficient. By leveraging Argo CD, teams can automate the deployment process, ensure consistency across environments, and maintain a reliable and scalable infrastructure. Harness the power of Argo CD to streamline your deployment workflows and accelerate your development lifecycle.

## Author
[Mansour KA](https://github.com/mansourka06)
