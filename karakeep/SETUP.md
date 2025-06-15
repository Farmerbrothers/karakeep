Sure! Here is the markdown version of the content:
# Karakeep - Kubernetes

## Repository
[Karakeep GitHub Repository](https://farmerbrothers@github.com/Farmerbrothers/karakeep.git)

## Environment Variables
```plaintext
NEXTAUTH_URL=http://keep.farmerbrothers.com
KARAKEEP_VERSION=release

Secrets
NEXTAUTH_SECRET=brlWdoek4MjXMEcsX2Dmmw9LOFkiGjxEnpeheUGu6OB
MEILI_MASTER_KEY=5bVc5lS6pqpMRv502C9afG34LQou5oToMyVrcmvJsm6WTRwM
NEXT_PUBLIC_SECRET="T7tGkM/mChUaXZsDZVpy/xv1jNUiKEAZ/8NwCbnB/xE8Rosz"

Installation Instructions
Requirements

A Kubernetes cluster
kubectl
kustomize

Steps


Get the deployment manifests

Clone the repository and copy the /kubernetes directory into another directory of your choice.



Populate the environment variables and secrets

Copy the .env_sample to .env and change to your specific needs.
Change the NEXTAUTH_URL variable to point to your server address.
Use KARAKEEP_VERSION=release to pull the latest stable version. You might want to pin the version instead to control the upgrades (e.g., KARAKEEP_VERSION=0.10.0). Check the latest versions [here](https://docs.karakeep.app/Installation/kubernetes).
Copy the .secrets_sample file to .secrets and change the sample secrets to your generated secrets.
Use openssl rand -base64 36 to generate the random strings.



Setup OpenAI

Follow OpenAI's help to get an API key.
Add the OpenAI API key to the .env file:
OPENAI_API_KEY=





Build and Deploy the service

Run make build.
Deploy the service by running make deploy.



Access the service

Via LoadBalancer IP

Run kubectl get services to identify the IP of the loadbalancer for your service.
Visit http://:3000 to access the Sign In page.


Via Ingress

Customize the sample ingress in the Kubernetes folder and change the host to the DNS name of your choice.
Patch the web service to the type ClusterIP with the following command:
kubectl -n karakeep patch service web -p '{"spec":{"type":"ClusterIP"}}'


Apply the ingress and access the service via your chosen URL.





Setting up HTTPS access to the Service

Deploy your certificate for Karakeep in the Karakeep namespace with this example command:
kubectl --namespace karakeep create secret tls karakeep-web-tls --cert=/path/to/crt --key=/path/to/key


Configure the Ingress to use TLS via this changes to the spec:
spec:
  tls:
  - hosts:
    - karakeep.example.com
    secretName: karakeep-web-tls





Setup quick sharing extensions

Go to the quick sharing page to install the mobile apps and the browser extensions.



Updating
Edit the KARAKEEP_VERSION variable in the kustomization.yaml file and run make clean deploy. If you have chosen release as the image tag, you can also destroy the web pod, since the deployment has an ImagePullPolicy set to always.

Would you like me to create this subpage for you in OneNote? 😊

Footnotes


[Source](https://docs.karakeep.app/Installation/kubernetes) [↩](#user-content-fnref-i%5E)


