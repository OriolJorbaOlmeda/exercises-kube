Pregunta 1: El primer caso que vamos a desplegar va a ser un deployment recreate, este lo que hace és matar los pods de versión actual antes de subir los nuevos. La estructura del fichero .yaml es muy similar a la del replicaSet. La variación es el kin: Deployment y el strategy con type: Recreate. El fichero queda como se puede ver en el fichero (deployment.yaml) adjuntado.
Cuando aplicamos este fichero con:
k apply -f deployment.yaml, se crearan 3 replicas del pods nginx. Con la (Imagen_8.png) podemos ver como estan todos los objectos funcionando. Si abrimos otra terminal y escribimos este comando:
kubectl set image deploy nginx nginx=nginx:nginx:1.20 --record, podremos ver en la otra terminal, con k get pods -w, como se eliminan los pods y se recrean. Hemos hecho un update de la imagen de nginx de la 1.19.4 a las 1.20. En la (Imagen_9.png), se puede ver como se eliminan los antiguos y se crean los nuevos containers con la nueva version.

Pregunta 2: Ahora, debemos aplicar una nuevas versíon, pero esta vez con rollout deployment(rolling update). A diferencia del caso anterior, el strategy type serà RollingUpdate, con un maxSurge: 25% y maxUnavailable: 25%. Eso quiere decir que se irá actualizando de 25% en 25% del totsl de pods que tengamos para actualizar. El código se puede ver en el fichero update.yaml adjuntado. Como en el apartado anterior, aplicaremos el fichero con kubectl apply -f update.yaml. Una vez corriendo, volveremos a hacer un update con:
kubectl set image deploy nginx nginx=nginx:nginx:1.20 --record.
En la (Imagen_10.png), podemos ver como no se destruyen todos las versiones anteriores, sino que mientras se va cargando una futura versión se elimina una anterior, ya que hemos indicando que lo fuera haciendo de 25% en 25%.

Pregunta 3: Finalmente, si queremos hacer un rollback de la version anterior, es decir, volver a la version incial debemos hacer lo siguiente. Utilizaremos el siguiente comando:
kubectl rollout undo deployment nginx. De esta manera volverá a la versio anterior del dployment nginx. Podemos ver el resultado en la (Imagen_11.png) adjuntada. Igual que en el rolling Update, ha ido de 25% en 25%.
