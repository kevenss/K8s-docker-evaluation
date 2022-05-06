# K8s-docker-evaluation

-- Il faut récupérer le fichier kubeconfig.yml pour déployer le cluster distant

# Déploiement des images

-- Pour le cluster, nous dévons déployer deux environnements distants grace aux serveurs:

redis 
cloud.canister.io:5000/arhturescriou/node-redis

  # Configuration des serveurs
!!!Attention!!!

Pour l'utilisation de ces serveurs, nous devons utilier une image privé :

spec:
  imagePullSecrets:
    - name: regcred

  # Variables d'environnement 
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


### Install dependencies

```
yarn
```

or

```
npm install
```

### Start worker

```bash
node main
```

Add new worker

```sh
curl -X POST localhost:3000/register  -H "Content-Type: application/json"  -d '{"url": "http://localhost:8080"}'
