# 347-docker-swarm-wordpress
[Planification](https://github.com/users/joaberch/projects/2/views/1)
[GitHub](https://github.com/joaberch/347-docker-swarm-wordpress)
## Déploiement :  
Connection SSH :  
```cmd
ssh *username*@172.26.1.23
```
Création des machines :  
```cmd
cd scripts
```  
```cmd
sh init-docker-vm.sh manager1
```  
```cmd
sh init-docker-vm.sh worker1
```  
```cmd
sh init-docker-vm.sh worker2
```  
Récupérer les adresses IP des machines :  
```cmd
multipass list
```  
Connexion au machines distantes :  
```cmd
multipass shell manager1
multipass shell worker1
multipass shell worker2
```  
## Suppression du swarm
Lorsque vous êtes connectez à la machine distante avec la commande :
```cmd
ssh *username*@172.26.1.23
```  
Faites cette commande pour accéder au manager : 
```cmd
multipass sh manager1
``` 
Pour voir les stacks actifs :
```cmd
docker stack ls
```
Cela vous répondra quelque chose comme la suivante:
```cmd
  Name
Nom_stack
```
Avec ce nom faites un
```cmd
docker stack rm *nom_stack*
```