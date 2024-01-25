ops-sre
Observabilité
L’objectif de ce projet est d’utiliser l’infrastructure créé pour le projet strapi (docker, prometheus, etc).

Pour simuler différents scénarios et détecter les limites de perfomances du projet.

Rappel de l’infrastructure
L’infrastructure du projet doit comporter un strapi (le coeur du système) et sa base de données. Au déploiement les deux doivent être séparés pour pouvoir monter en charge indépendamment.

Il faut aussi ajouter un système pour récupérer les logs: prometheus/grafana. Afin d’enregistrer les différentes variations de l’application (nombre d’appel, delai des requêtes, mémoire, etc).

Il est également possible d’ajouter les statistiques des conteneurs docker dans le prometheus : https://docs.docker.com/config/daemon/prometheus/

Scénarios intéressants
Ressources allouées
Pour obtenir des résultats réalistes et intéressants on veut limiter les ressources de conteneurs. En effet dans le cas de déploiement sur des serveurs dans le cloud ou chez un fournisseurs de machine virtuelle les machines ont rarement autant de ressources que nos ordinateurs.

Par exemple les VM d’aws EC2 de base ont 2 giga de ram et 1 seul CPU. On veut donc limiter de la même manière les ressources données à strapi et à sa base à l’aide de docker.

Charge
L’autre chose que l’on veut simuler c’est l’utilisation de l’application, et donc simuler des utilisateurs qui se connectent et utilise le strapi. Pour ça le plus simple et de créer un script (bash, python ou js) qui lance des requêtes HTTP sur le endpoint du strapi.

Pensez bien à varier les types d’utilisations : Le comportement du strapi et de sa base peuvent varier si les utilisateurs font seulement de la lecture ou si il y a également des écritures en base de données. Pour ça veillez bien à utiliser les différents endpoints du strapi (create, request, update, delete).

Monté à l’échelle
Lorsque que le strapi est beaucoup sollicité il est possible de dupliquer l’instance de conteneur du strapi. Il est possible de le faire manuellement ou avec une configuration qui l’automatise avec docker-compose. (Il est très interessant d’observer quelles conditions d’utilisations déclenchent ce genre de monté à l’échelle automatique).

Rendu attendu
Il est attendu un rapport mettant en forme les résultats de vos observations de différents scénarios que vous trouvez pertinents. Un soin particulier doit être porté à la présentation des résultats (graphiques scientifiques, explicitation du contexte du scénario).

De plus il est important d’y ajouter votre analyse et déductions par rapport au comportement observé.

Le rendu attendu concerne plus les résultats obtenus par différents scénario plutot que la configuration du code.

Cependant il est utile aussi de joindre ces configurations de code pour expliciter les scénarios lancés.

Exemple de graphiques qui pourrait être pertinent :

charge limite de l’application : (pour des ressources données, trouver le nombre et type d’appel par secondes maximum)

charge optimal : (comportement jugé comme optimal : temps de réponses minimum, pas d’erreur du système, avec un maximum d’utilisateurs par secondes)

montée à l’échelle : (comportement lors de la création d’un nouveau conteneur)

Vous pouvez ajouter tout les autres scénarios que vous trouvez pertinent.