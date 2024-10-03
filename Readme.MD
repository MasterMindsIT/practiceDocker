Que soluciona Docker con la virtualización
Soluciona: 
Entorno de desarrollo
Distribuir 
Ejecutar
docker -v #Muestra la versión instalada
docker images #Muestra las imagenes  descargadas
docker ps #Muestra contenedores vivos
docker ps -a #Muestra todos corriendo o no
docker inspect ID #Muestra amplia info del contenedor
docker run --name miHiWorld hello-world #Personaliza el nombre conteneder 
docker rename nombreAnterior nuevoNombre #Cambiar el nombre de un contenedor
docker rm name o ID #Elimina el contenedor por nombre o ID
docker container prune #Elimina todos los contenedores detenidos
docker rm ID1 ID3 ID4 #Elimina el listado de contenedores
docker run contenedor #Lo descarga y finaliza al instante 
docker run -it ubuntu #Queda interactivo el contenedor deja abierto la linea de comandos en el caso de ubuntu salir del proceso muere en contenedor
docker run --name miUbu -d ubuntu tail -f /dev/null #Crea el contenedor con un nombre en modo detach(ejecutar en segundo plano) y nuevo proceso principal y mientras ese nuevo proceso no se detiene sigue y seguira vivo
docker exec -it miUbu bash #Accede al modo interactivo del contenedor miUbu
docker stop miUbu #Detiene el contenedor miUbu
docker run --name proxi nginx #Corre Nginx deja el proceso corriendo y sin terminar se puede salir con ctrl c
docker run -d --name proxi nginx #En modo detach sigue corriendo en segundo plano
docker logs proxi #Puedo ver todos los logs de mi contenedor proxi
docker stop proxi lo termina ya que con rm no se puede porque esta corriendo
docker run -d --name minginx -p 8081:80 nginx #Mi puerto donde expondre los servicios de mi contenedor y despues de los 2 puntos en puerto del contenedor.. Por lo tanto desde el navegador puedo acceder mediante localhost:8081 al nginx
docker logs -f minginx #Deja los logs abiertos para ver en tiempo real los mensajes
docker logs --tail 10 -f minginx #Muestra las 10 últimas lineas del logs
docker stop contenedor primero y docker rm contenedor segundo para matar todo
docker rm -f minginx #Forza terminar todo en 1 solo comando
docker container run -d -p8080:80 nginx
docker exec -it namecontainer bash #Modo interactivo sesion tipo putty con bash que suele venir en la mayoria o sh que es otra terminal

docker volume create nombre-volume
docker volume ls
docker volume inspect
docker run -d --name mysql-volume -v docker-curso:/var/lib/msql -p 3311:3306 MYSQL_ROOT_PASSWORD=ADMIN mysql
VOLUMENES ADMINISTRADOS DE FORMA MANUAL
Crear carpeta e ingresar a ella:
mkdir curso docker
con pwd obtenemos el path /c/Personal/Docker
docker run -dit -v /c/Personal/Docker:/docker-curso -p 3311:3306 MYSQL_ROOT_PASSWORD=ADMIN mysql
crear el archivo Dockerfile
FROM ubuntu
RUN apt-get update && apt-get install -y \  #El comando RUN solo funciona a la hora de compilar
     python3 \
     curl \
     nano
-t es el tag o nombre el PUNTO del final indica que dockerfile esta en la misma carpeta
docker build -t ubuntu-with-python .
docker run -it ubuntu-with-python #abre sesion de ubuntu por linea edcomandos con las instalaciones que habiamos indicado

Copiando archivos 
COPY . /app #copia todos los archivos de donde estamos a la carpeta app
WORKDIR /app #deja el directorio de traabjoautomaticamente en app
ENV DEBIAN_BACKEND=ADMIN #define una variable de entorno no editable
ENV version=1.0

ARG TEXT_EDITOR=nano #crea un argumento para poder dejar por sdefecto a instalar nano o hacer build-args para en vez de nano vim
CMD ["nginx", "-g", "daemon off;"]#ejecuta luego de inicializada la imgen es como una tarea programada al iniciar la imagen
docker run -it ubuntu-with-python:v5
docker ps #para ver el id
docker exec -it id bash #levanta la sesion por terminal 
curl localhost #dedvuelve el servicio de nginx
ingresando dentro de la -it con curl localhost podemos ver que si esta corriendo nginx
ENTRYPOINT ["nginx", "-g", "daemon off;"]#HACE LO MISMO QUE cmd PERO NO ES SOBRE ESCRITO POR LA LINEA DE COMANDOS

Para publicar nuestras imagenes a equipos de trabajo :
Ingresamos a docker hub y ceramos un repositorio quedando miUser/nomnreImage
docker login #ingresamos el user y la pass
docker image tag ubuntu-with-nginx miUser/nomnreImage:v1
docker push miUser/nomnreImage:v1

