Para poder hacer un Blue Green Deployment, debemos preparar dos deployment, y un service. Uno sera el blue y el otro el green. De esta forma podremos hacer un swithc entre los dos sabiendo que el segundo funciona.

El primer deployment serà el blue, el cual tendrà el cual se puede ver en el fuchero blue.yaml. En ese caso, como se puede ver en el label del selectro está la versión, que inicialmente es la 1.19.4, y de momento este serà el blue. Todo seguido, corremos este objeto con:
kubectl apply -f blue.yaml

En segundo lugar creamos el service, como se puede observar en el fichero blue_service.yaml. En el selector del service, le añadimos la version, en este caso, 1.19.4, ya que se trata de la versión del fichero blue, que es el que actualmente esta en servicio. A continuación, creamos este objecto con:
kubectl apply -f blue_service.yaml.

Apartir de aquí, es donde empieza el ejercicio. Hemos de crear otro deployment que nos permita cambiar de version siguiendo la idea de blue green deployment. Por eso crearemos el fichero green.yaml. En este tendremos lo mismo que en el fichero blue.yaml, pero con la version mejorada de nginx, en nuestro caso, la 1.20. Podemos ver como queda el codigo en el fichero green.yaml
A continuación, ejecutamos ese fichero y comprovamos que funcione con:
kubectl apply -f green.yaml
Si aplicamos kubectl get pods, podremos ver las dos versiones, y que las dos funcionan, pero la unica que esta conectada a un servicio es la 1.19 (Imagen_12.png).
Como ahora sabemos que la versión 1.20 funciona, podemos pasarla a ser la nueva blue cambiando el label versiona del service a 1.20. Cuando apliquemos kubectl apply -f blue_service.yaml, este reemplazará el anterior y ya tendremos la nueva versión fucionando sin que los usuarios se den cuenta.
Para comprovarlo, nos fijamos en los endpoints del servicio nginx con:
k get endpoints nginx. Nos da la siguiente información (Imagen_13.png). A continuación, miramos la infoamación de uno de los dos pods con version 1.20, y comporvamos que concuerde la IP con la del endpoint del servicio. Esto con:
kubectl describe pods (nombre pod).
Como podemos ver en la (Imagen_14.png) las IP coinciden, lo que quiere decir que el proceso ha funcionado.
