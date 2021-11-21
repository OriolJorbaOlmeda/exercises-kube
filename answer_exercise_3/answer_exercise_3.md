Pregunta 1: Para poder exponer el servicio al exterior, lo que debemos utilizar es un LoadBalancer. Crearemos el fichero service1.yaml, donde type: LoadBalancer, y el puerto serà el 8080 y el target port el mismo. La app serà nginx-server para poder accerder a todos esos Pods con el mismo label.
En el fichero service1.yml adjuntado se puede observar como ha quedado el codigo.

Pregunta 2: Para tener un acceso solo interno, y que no se pueda acceder de forma externa, se hará uso del ClusterIP, este es el servicio predeterminado que ofrece Kubernetes. Solo hay que indicar el tipo, type:ClusterIP. y concretar el puerto. Para poder acceder a el hay que hacer uso de un proxy.
En el fichero service2.yml adjuntado se puede observar como ha quedado el codigo

Pregunta 3: Para poder exponer el servicio al exterior y solo abriendo un puerto en especifico de la VM, primero debemos crear un fichero service3.yaml con el type: NodePort, app: neginx-server, de esta forma escogerá todos los Pods con ese mismo label. Le indicamos el puerto de acceso externo, que en este caso será noePort:30000, el puerto expuesto internamente, que es port: 8080 y el purto del container que es targetPort: 8080. Si ponemos a correr el replica set anterior y a la vez este servicio con:
k apply -f service1.yaml, estaremos exponiendo el servicio en la IP de minikube y el puerto 30000.
En el fichero service3.yml adjuntado se puede observar como ha quedado el codigo.
