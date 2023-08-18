## Deploy react app to K8S

## Implementation plan

 ## prerequisites 
  1. Docker Desktop installed
  2. Minikube installed and runing in docker desktop
## Step 1
 Build you 2 images i.e. backend and client images and push them to docker-hub.
## Step 2 
Create you deployment files for both the backend and client 
## Step 3
Create 2 services for both the backend and client services
## Step 4
Create a secret file to hold you mongodb url (if using a remote connection no need)
if you are using a deployed mongodb in K8S  like mine create the Deployment and service files and also add secrets for mongo username and password.
## Step 5
Deploy the file using below command

`
kubectl apply -f <filename>
`

in below order

1. secrets file
2. Deployment files
3. Service files

## Step 6

So that you can be able to access the service you will need to port forward for both the the backend and client services

For backend use below command

`
kubectl port-forward service/yolo-backend-service 5050:5050
`
For client to be able to access the client service in your browser

`
kubectl port-forward service/frontend-service 3000:3000
`

Challenge faced -- for the client app. I tried to store the base url of the backend service to be used in the client app but faced a dependecy issue since the Yolo app was build with a previos version of react that may not support env variables and might required extra configs.

## Step 7

Access the client app using this [url](http://localhost:3000) and you can add, edit, delete and view the products.


## Choice of kubernetes Objects
I used deployments for both the backend and client application.
This is because Deployments are suitable for stateless apps where individual instances can be easily scaled horizontally.

I used statefulset for mongodb service together with a persistence volume. This is because StatefulSets are more suitable for stateful applications that require stable network identities and persistent storage.

## Expose pods to the internet

To make sure my pods are excessible via the internet i used port-forwading on my services so that i can access both the backend services and the fronted yolo service. However i had tried to use ENV variables to access the backend in the frontend but this failed. i result to user the port-forwarded service to access the backend in the client application.


## Persistence Volume

I only used persistence volume on the mongodb since i need to persist the data to be diplayed on the client application. However i ended up not using the deployed MongoDB due to some authentication issues despite passing all required parameters.






