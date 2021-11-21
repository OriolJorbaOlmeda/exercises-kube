Construcción del Pod: Para construir un Pod, siempre son necesarios el apiversion, kind, metadata y spec. Dentro del metadata y el spec irán especificadas las especificaciones del ejercicio. En primer lugar, el name = nginx y dentro de label el app = nginx-server. A continuació hace falta rellenar la parte de spec, la que envuelve los containers y sus condiciones. Este tendrá el nombre name=nginx, y provendrá de la imagen de nginx versión 1.19.4 (image= nginx:1.19.4). A continuación, y dentro de container, solo falta decir los limites y request de las resources. Tanto en limits como en request, sera cp: "100" y memory= "256Mi". En el fichero pod.yaml se puede ver perfectamente como ha quedado la configuración. Para levantar este Pod, solo hace falta escribir el siguiente comando des de la misma carpeta donde se encuentra el fichero(para hacerlo más sencillo): kubectl create -f pod.yaml (Imagen_1.png).

Pregunta 1: Para poder ver las últimas 10 lineas de los logs solo hace falta una linea de comando para poder verlo, que es la siguiente:
kubectl logs --tail=10 nginx. Donde tail nos especifica los el número de logs que queremos ver empezando por la cola y nginx es el nombre de nuestro pod.

Pregunta 2: Para poder obtener la IP interna del Pod, se puede ver accediendo a la descripción del propio Pod con:
kubectl describe pod nginx. Donde nginx es el nombre del Pod. Un vez ejecutado el comando, nos aparecerá una listado con toda la información y especificaciones de ese Pod. Si nos fijamos en el apartado Ip nos aparecerá la IP interna del Pod (Imagen_2.png).

Pregunta 3: Para poder entrar dentro del Pod, son necesarios el comando exec con los flags --stdin y --tty, de la siguiente forma:
k exec --stdin --tty nginx /bin/bash. Una vez ejecutado, estaremos dentro del Pod como se puede ver en la (Imagen_3.png).

Pregunta 4: Para poder visualizar el contendio que expone NGINX con este Pod se tiene que hacer uso del comando port-forward e indicando el puerto 8080 de la siguiente forma:
k port-forward nginx 8080:80. Una vez ejecutado, si nos dirigimos al navegador y buscamos el localhost:8080, nos aparecerá el mensage de Welcome to NGINX (Imagen_4.png).
