### K8s-docker-evaluation

-- Il faut récupérer le fichier kubeconfig.yml pour déployer le cluster distant

### Déploiement des images

-- Pour le cluster, nous dévons déployer deux environnements distants grace aux serveurs:

redis 
cloud.canister.io:5000/arhturescriou/node-redis

  ### Configuration des déploiements.yaml
!!!Attention!!!

Pour l'utilisation de ces serveurs, nous devons utilier une image privé :

spec:
 imagePullSecrets:
    - name: regcred

  ### Variables d'environnement 
  Pour le serveur node-redis, nous utilisons des variables d'environnement dont le port sera configuré par 3000
  ``` 
            env:
            - name: ADDRESS
              value: 'noderedis:3000'
            - name: PORT
              value: '8080'
 ```
  Pour le serveur redis, nous utilisons le port 5379
          env:
            - name: ADDRESS
              value: 'redis:6379'
            - name: PORT
              value: '6379'
  
  Tout d'abord, nous élaborons des fichiers déploiement pour que le serveur et l'utilisation de l'image fonctionne grace aux commandes ci-dessous.
  
```
kubectl create -f kevindeploymentredis.yaml
kubectl "create -f kevincloudredisdeployment.yaml
kubectl apply -f kevindeploymentredis.yaml
kubectl apply -f kevincloudredisdeployment.yaml 
``` 

Pour vérifier que les déploiement s'exécutent, nous utiliserons cette commande:

```
kubectl get deployments
```

### Déploiement du service

Pour déployer un service, nous utilserons une commande pour créer un fichier service et de configurer sur le cluster en faisant kubectl create -f kevinredisservices.yaml concernant le serveur redis. 

Meme démarche pour le serveur node-redis cloud.

Dans Kubernetes, un service est une environnement qui représente un ensemble de pods par laquelle y accéder.

Pour configurer le service sur le cluster, nous utiliserons kubectl apply -f kevinredisservices.yaml et kubectl apply -f kevincouldredisservice.yaml  

```
kubectl create -f kevincouldredisservice.yaml
kubectl "create -f kevinredisservices.yaml
kubectl apply -f kevinredisservices.yaml
kubectl apply -f kevincouldredisservice.yaml 
``` 
Et ensuite pour vérifier que le service a bien été créer, nous utilisons la commande "kubectl get services" pour que les services sont bien crées

```
kubectl get services
```

### Déploiement du pods

Pour déployer des pods, nous utilserons la commande "kubectl create -f kevinredispod.yaml" pour créer un fichier pod et de configurer sur le cluster en faisant kubectl "create -f kevinredispod.yaml".
Meme chose pour le serveur node-redis.

```
kubectl create -f kevinredispod.yaml
kubectl "create -f kevincloudredispod.yaml
kubectl apply -f kevincloudredispod.yaml
kubectl apply -f kevinredispod.yaml 
``` 
Il faudra appliquer entre trois et cinq pods avec leur identifiant pour vérifier qu'il fonctionne simulatement.

Pour vérifier que chaque de ces pods s'exécutent, nous utiliserons la meme syntase que la commande précédente.

```
kubectl get pods
```

### Vérification des adresses

Pour vérifier que les ids des pogs fonctionne, une commande est utilisable pour cela

```
kubectl logs redis-cloud-kevin pour le serveur node-redis
kubectl logs redis-kevin pour le serveur redis
```
