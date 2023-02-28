# These are the steps to run the chat app https://github.com/JFabianMM/Chat-App-Minikube
# in minikube.


# Enter to folder BackEnd-microservice
cd BackEnd-microservice
      
# Create the backend26 image
docker build -t backend26:1 .

# push the image to a repository, as example: 
docker tag backend26:1 fabianmm34/chatapp:backend26
docker push fabianmm34/chatapp:backend26   

# Enter to folder UI-microservice-back
cd UI-microservice-back     
	
# Create the graphql26 image
docker build -t graphql26:1 .

# push the image to a repository, as example: 
docker tag graphql26:1 fabianmm34/chatapp:graphql26
docker push fabianmm34/chatapp:graphql26   

# Enter to the file UI-microservice-front
cd UI-microservice-front    

# Create the frontend26 image
docker build -t frontend26:1 .

# push the image to a repository, as example: 
docker tag frontend26:1 fabianmm34/chatapp:frontendl26
docker push fabianmm34/chatapp:frontend26   

# start minikube
minikube start 

# Add an add-on                	
minikube addons enable ingress-dns

# Apply the nextmanifests
kubectl apply -f mongodb1-pod.yaml
kubectl apply -f mongodb2-pod.yaml
kubectl apply -f backend-pod.yaml 
kubectl apply -f frontend-pod.yaml
kubectl apply -f graphql-pod.yaml
kubectl apply -f example-ingress.yaml   


# Add the following line to the bottom of the /etc/hosts file on your computer (you will need administrator access):
# nano /etc/hosts 
# 127.0.0.1       chat-app.version1

# Run a tunnel
minikube tunnel


Access to the app at:
http://chat-app.version1/
