Pour la tâche 2 du challenge 4, j'ai suivi les instructions et à la fin la commande "kubectl top nodes", me donnait le résultat suivant:

NAME             CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
docker-desktop   181m         9%     1515Mi          80%

Il y a une capture d'écran du dashboard dans ce dossier.

Pour la tâche 3 du challenge 4, après avoir suivi les instructions et avant de lancer la boucle infinie, j'avais le résultat suivant avec la commande "kubectl get hpa":

NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   0%/50%    1         10        1          6d2h

Vu que je load n'augmentait pas avec la commande "kubectl run -it --rm load-generator --image=k8s.gcr.io/busybox" + "while true; do wget -q -O- http://php-apache; done",
j'ai utilisé la commande indiquée sur le site de Kubernetes:
kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"

j'ai alors obtenu pour la commande "kubectl get hpa" :

NAME         REFERENCE               TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   250%/50%   1         10        1          6d3h

et pour la commande "kubectl get deployment php-apache" :

NAME         READY   UP-TO-DATE   AVAILABLE   AGE
php-apache   5/5     5            5           6d3h

C'est revenu à 0%/50% et 1/1 quelques minutes après avoir arrêté le load.
