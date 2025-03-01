# NodePort service - minikube cluster

This is an example how to access application/deployment exposed on nodeport service in minikube cluster.

## Steps

1. Install the minikube on windows or linux machine and start it. - [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)
2. Create a YAML file containing the deployment and NodePort service to expose the application. You can find the YAML file in the project.
   Name of deployment: nginx-deployment , Name of nodeport service: nginx-deployment-service , NodePort: 32000
4. Deploy the application:
   kubectl apply -f deployment.yaml
5. Access the application :
    1. Using port forwarding:
       
       kubectl port-forward service/nginx-deployment-service 8888:8080   
       browse --> http//:127.0.0.1:8888  
    3. Using minikube service command - This command provides a url to browse the application. It will open a port on local machine.
       
       minikube service nginx-deployment-service --url  
       browse --> http//:127.0.0.1:local-port  
    5. Using another similar minikube service command - This will create a temporary network route from your local machine to the Minikube cluster, enabling direct access to the specified service.
       
       minikube service nginx-deployment-service  
   6. In non minikube k8s cluster, application can we accesesed  
      curl node-ip:nodeport       ---> From command line  
      http://node-ip:nodeport     ---> From browser
      wget node-ip:nodeport       ---> To download the content from URL

