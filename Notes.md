 Q) 2. Based on the initial iBased on the initial implementation in step 1, either implement 
a. How do you make the service scalable?
b. What CI/CD pipeline would you use (if not done in code, please describe every
step from the commit of new code until the new code is running in production)?
c. How would you store and deploy secrets (such as API keys)?
d. How do you test how well your infrastructure scales (when many requests come
in)?
e. How do you provide an SSL certificate for your service?

Answers: 

 a) To make the service scalable we can use HorizontalPodAutoscaler (HPA) to automatically adjust the number of pods based on CPU, memory, or custom metrics. 

 b)  I would use ArgoCD for CI/CD. GitOps-based Continuous Deployment tool for Kubernetes, ensures that the state of your Kubernetes cluster matches the state specified in our Git repository
       1. Code Commit: Developer pushes code to main branch.
       2. Build & Push: CI/CD builds Docker image and pushes to registry.
       3. Update Manifest: CI/CD updates deployment.yaml with new image tag.
       4. ArgoCD Sync: ArgoCD detects changes and synchronizes.
       5. Deploy & Validate: ArgoCD deploys to Kubernetes and monitors health.

 c) To deploy secrets like password and Api keys We can use AWS secrets manager to store the credentials
	 In a Kubernetes environment, we can implement this by deploying tools like Cluster Secrets Store and External Secrets to  integrate and retrieve secrets from AWS Secrets Manager within our cluster.

 d)  To test infrastructure scaling, simulate high traffic using tools like k6 or Postman. Temporarily lower the HPA target CPU utilization (e.g., to 20%) for quicker scaling observation. Monitor pod behavior as the cluster adjusts dynamically to handle the increased API load

 e) For SSL Certificate we can use 
     1. Using a Self-Signed Certificate  - Generate a self-signed certificate using Let’s Encrypt or OpenSSL.
            Upload the certificate and key to your application or a secret in Kubernetes.
     
     2. Using AWS ACM with an LoadBalancer for managed, auto-renewing certificates.



