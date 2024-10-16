# Mongodb
kubectl apply -f deploymongo.yml
kubectl get deployments

# BE
docker build . -t us.icr.io/$MY_NAMESPACE/giftapp
docker push us.icr.io/$MY_NAMESPACE/giftapp
kubectl port-forward deployment.apps/giftapp 3060:3060

# FE
npm run build  (githublink-fe)

# giftwebsite
docker build . -t us.icr.io/$MY_NAMESPACE/giftwebsite 
docker push us.icr.io/$MY_NAMESPACE/giftwebsite
docker run -p 9000:9000 us.icr.io/$MY_NAMESPACE/giftwebsite

# Deploy the giftwebsite application on Code Engine
ibmcloud ce application create --name giftwebsite --image us.icr.io/${SN_ICR_NAMESPACE}/giftwebsite --registry-secret icr-secret --port 9000