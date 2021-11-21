Pregunta 1: Para poder crear un replicaSet con 3 replicas, primero debemos crear un fichero .yaml, con el codigo necesario para crear tres pods identicos a los de la pregunta anterior, tal y como se puede ver en la (Imagen_5.png). La metadata será igual que en el pod anterior, y la información del caontainer tambien. En el campo replicas de spec: indicamos que queremos 3, como pide el enunciado.
Una vez creado, lo levantamos con el comando:
kubectl apply -f .\replica.yaml. Si después miramos los pods que tenemos con: kubectl get pods. Veremos que se han levantado 3 pdos con el nombre nginx (Imagen_6.png).

Pregunta 2: Para poder escalar las replicas de 3 a 10, es tn sencillo como aplicar el siguiente comando:
kubectl scale --replicas=10 rs nginx. De esta forma pasamos de 3 copias a 10, como podemos ver en la (Imagen_7.png). Como se puede ver, 3 se quedan en pending, pero es debido a que se reservan X recursos y no se pueden crear más.

Pregunta 3: Se adaptarái mejor un Deployment que un replicaSet, ya que puede poseer replicaSets y actualizarlos igual que sus Pods. Estos gestionan los replicaSets y hace mucho más fàcil a la hora de orquestrarlos.
