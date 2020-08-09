# Refactor Udagram App into Microservices and Deploy


## Docker Images
https://hub.docker.com/r/bh0na/reverseproxy
https://hub.docker.com/r/bh0na/udacity-frontend
https://hub.docker.com/r/bh0na/udacity-restapi-feed
https://hub.docker.com/r/bh0na/udacity-restapi-user

## Set the following environment variables
To run in k8: add them in env-config.yaml and env-secret.yaml / aws-secret.yaml (values in base64) - note that these values aren’t committed to GitHub
To run locally: add them in `~/.profile` & source ~/.profile

      POSTGRESS_USERNAME: $POSTGRESS_USERNAME
      POSTGRESS_PASSWORD: $POSTGRESS_PASSWORD 
      POSTGRESS_DATABASE: $POSTGRESS_DATABASE 
      POSTGRESS_HOST: $POSTGRESS_HOST 
      AWS_REGION: $AWS_REGION  
      AWS_PROFILE: $AWS_PROFILE 
      AWS_MEDIA_BUCKET: $AWS_MEDIA_BUCKET
      JWT_SECRET: $JWT_SECRET
      URL: "http://localhost:8100"

## Repository
https://github.com/Bhona/cloud-developer

## Screenshots
`App Running`: https://drive.google.com/open?id=1L021gTkKk3rezAerHwnAB4-YbpYCu_T0
`kubectl get nodes`: https://share.getcloudapp.com/E0uqjPPw
`kubectl get pods`: https://drive.google.com/open?id=10WGDr4IXGF4lCxip5G6WelJxO0FFjnSD
`kubectl get service`: https://drive.google.com/open?id=1Z4XQl3Mq1WCPsDj4VwOJ6fRW6GXYTV0Q
`port-forward-reverseproxy`: https://drive.google.com/open?id=1sSxtjFQkFTOv-PdgCnSn5JziX3Q12gqB 
`port-forward-frontend`: https://drive.google.com/open?id=1kHCTBOGqxp4DNajV1GoS_wiqmx4pI7OC

## Running K8s cluster on AWS using Kubeone:
1. https://github.com/kubermatic/kubeone/blob/master/docs/quickstart-aws.md
2. After Infrastructure is created on aws cd into k8s directory and execute the following:
    1. `kubectl apply env-configmap.yaml`
    2. `kubectl apply -f env-secret.yaml`
    3. `kubectl apply -f aws-secret.yaml`
    4. `kubectl apply -f backend-feed-deployment.yaml`
    5. `kubectl apply -f backend-feed-service.yaml`
    6. `kubectl apply -f backend-user-deployment.yaml`
    7. `kubectl apply -f backend-user-service.yaml`
    8. `kubectl apply -f frontend-deployment.yaml`
    9. `kubectl apply -f frontend-service.yaml`
    10. `kubectl apply -f reverseproxy-deployment.yaml`
    11. `kubectl apply -f reverseproxy-service.yaml`
3. Port-forwarding 8080 (reverse proxy for services) and 8100 (frontend)
	`kubectl port-forward service/frontend 8100:80 &
  	  kubectl port-forward service/reverseproxy 8080:8080 &`

## Running app locally using docker-compose
1. `cd udacity-c3-deployment/docker/`
2. Build images: `docker-compose -f docker-compose-build.yaml build --parallel`
3. Push images up to registry: `docker-compose -f docker-compose-build.yaml push`
4. Run the images in docker container: `docker-compose up`

## App Updates
1. New version image with new tag: https://drive.google.com/open?id=1VLdMkerNG6-UtO3A70kNi_2ywivlofiP 
2. Updated the deployment file and kubectl apply -f ${deployment}.yaml 
3. `Deployment ussign new image`: https://drive.google.com/open?id=1VLdMkerNG6-UtO3A70kNi_2ywivlofiP

## Travis CI/CD
1. See `.travis.yml`
2. travis working: https://drive.google.com/open?id=1Pwz923MApaoeOfipbx7y-2EEwFWqmznM 
                   https://drive.google.com/open?id=1z4QW8Xzyqhb6cMIljHJ9mOaCBObwxjLj