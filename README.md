# 347-docker-swarm-wordpress
[Planification](https://github.com/users/joaberch/projects/2/views/1)
[GitHub](https://github.com/joaberch/347-docker-swarm-wordpress)
### Prerequis
<ul>
  <li>Donner des rôles <a href="https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/">aux noeuds</a> (manager ou worker)
  </li>
  <li>Configurer <a href="https://docs.docker.com/engine/swarm/swarm-tutorial">docker pour swarm</a>
  </li>
  <li>Avoir <a href="https://docs.docker.com/engine/install/">docker daemon</a> sur chaque machine
  </li>
  <li>Donner des rôles <a href="https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/">aux noeuds</a> (manager ou worker)
  </li>
  <li>Un serveur</li>
</ul>

## Déploiement :  
Pour commencer il faut se connecter à la machine distante, pendant notre projet nous avons eu besoin d'un VPN pour se connecter au serveur et ensuite nous faisons une commande pour la connection SSH :  
```bash
ssh *username*@172.26.1.23
```
Dans notre cas ce serait admin347 <br>
L'étape suivante est déjà faite, mais dans le cas où tout serait réinitialisé, voici comment créer les machines :  
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
Dans cette étape on nous a déjà donné tous les scripts, il faut juste les exécuter <br>

Pour ce connecter ensuite aux noeuds, il faut avoir leur informations donc nous voulons récupérer les adresses IP des machines :  
```bash
multipass list
```  
Selon notre besoin on peut se connecter en utilisant le nom de la machine, voici les différentes commandes :  
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
Cela vous répondra quelque chose comme suivant:
```bash
  Name
Nom_stack
```
Avec ce nom faire: :
```bash
docker stack rm *nom_stack*
```
Cette commande effacera toute la stack<br>

La commande ci-dessous pruneras tous les containers, networks et images qui sont stockés dans docker
```bash
docker system prune
```
Il nous restera à supprimer les volumes donc voici la commande
```bash
docker volume rm *nom_volume*
```
ou
```bash
docker volume prune
```
## Création de la stack
Vérifier qu'aucun service ne tourne en faisant :
```bash
docker service ls
```
Assurez-vous ensuite que vous avez le docker-compose avec les secrets suiants dans le même répertoire :
<ul>
<li> DB_ROOT_PWD
</li>
<li> DB_PWD
</li>
</ul>
Il manque encore le fichier nginx.conf qui va servir à la configuration du nginx. Ce fichier sera dans le répertoire nginx lorsque vous êtes à côté du fichier .yaml.

Ensuite pour déployer la stack, allez dans la racine où il y a le docker.yaml pour swarm et faites la commande suivante :
```bash
docker stack deploy -c compose.yaml *nom_stack*
```
Vous pouvez choisir le nom de la stack

# Authors

| <h3><a href="https://github.com/LucasSimoesPolvora">@LucasSimoesPolvora</a></h3> | <h3><a href="https://github.com/JoaBerch">@JoaBerch</a></h3> |
| ------------- | ------------- |
| <img src="https://avatars.githubusercontent.com/u/122774951?v=4" style="width: 250"/>  | <img src="https://avatars.githubusercontent.com/u/122774888?v=4" style="width: 250" /> |