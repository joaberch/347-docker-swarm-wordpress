# 347-docker-swarm-wordpress
[Planification](https://github.com/users/joaberch/projects/2/views/1)
[GitHub](https://github.com/joaberch/347-docker-swarm-wordpress)
## Déploiement :  
Connection SSH :  
```bash
ssh *username*@172.26.1.23
```
Dans ce cas ce serait admin347 <br>
Cette étape est déjà faite, mais dans le cas où tout serait réinitialisé, voici comment créer les machines :  
```bash
cd scripts
```  
```bash
sh init-docker-vm.sh manager1
```  
```bash
sh init-docker-vm.sh worker1
```  
```bash
sh init-docker-vm.sh worker2
```  
Récupérer les adresses IP des machines :  
```bash
multipass list
```  
Connexion au machines distantes :  
```bash
multipass shell manager1
multipass shell worker1
multipass shell worker2
```  
## Suppression du swarm
Lorsque vous êtes connectez à la machine distante avec la commande :
```bash
ssh *username*@172.26.1.23
```  
Faites cette commande pour accéder au manager : 
```bash
multipass sh manager1
``` 
Pour voir les stacks actifs :
```bash
docker stack ls
```
Cela vous répondra quelque chose comme la suivante:
```bash
  Name
Nom_stack
```
Avec ce nom faites un
```bash
docker stack rm *nom_stack*
```
```bash
docker system prune
```
```bash
docker volume rm *nom_volume*
```
## Création de la stack
Vérifier qu'il y a vraiment aucun service qui tourne en faisant :
```bash
docker service ls
```
Ensuite pour déployer la stack, allez dans la racine où il y a le docker.yaml pour swarm et faites la commande suivante :
```bash
docker stack deploy -c compose.yaml *nom_stack*
```
Vous pouvez choisir le nom de la stack