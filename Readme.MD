Que soluciona Docker con la virtualización
<br>
Soluciona: 
Entorno de desarrollo
Distribuir 
Ejecutar
<br>
docker -v #Muestra la versión instalada<br>
docker images #Muestra las imagenes  descargadas<br>
docker ps #Muestra contenedores vivos<br>
docker ps -a #Muestra todos corriendo o no<br>
docker inspect ID #Muestra amplia info del contenedor<br>
docker run --name miHiWorld hello-world #Personaliza el nombre conteneder <br>
docker rename nombreAnterior nuevoNombre #Cambiar el nombre de un contenedor<br>
docker rm name o ID #Elimina el contenedor por nombre o ID<br>
docker container prune #Elimina todos los contenedores detenidos<br>
docker rm ID1 ID3 ID4 #Elimina el listado de contenedores<br>
docker run contenedor #Lo descarga y finaliza al instante <br>
docker run -it ubuntu #Queda interactivo el contenedor deja abierto la linea de comandos en el caso de ubuntu salir del proceso muere en contenedor<br>
docker run --name miUbu -d ubuntu tail -f /dev/null #Crea el contenedor con un nombre en modo detach(ejecutar en segundo plano) y nuevo proceso principal y mientras ese nuevo proceso no se detiene sigue y seguira vivo<br>
docker exec -it miUbu bash #Accede al modo interactivo del contenedor miUbu<br>
docker stop miUbu #Detiene el contenedor miUbu<br>
docker run --name proxi nginx #Corre Nginx deja el proceso corriendo y sin terminar se puede salir con ctrl c<br>
docker run -d --name proxi nginx #En modo detach sigue corriendo en segundo plano<br>
docker logs proxi #Puedo ver todos los logs de mi contenedor proxi<br>
docker stop proxi lo termina ya que con rm no se puede porque esta corriendo<br>
docker run -d --name minginx -p 8081:80 nginx #Mi puerto donde expondre los servicios de mi contenedor y despues de los 2 puntos en puerto del contenedor.. Por lo tanto desde el navegador puedo acceder mediante localhost:8081 al nginx<br>
docker logs -f minginx #Deja los logs abiertos para ver en tiempo real los mensajes<br>
docker logs --tail 10 -f minginx #Muestra las 10 últimas lineas del logs<br>
docker stop contenedor primero y docker rm contenedor segundo para matar tod<br>o
docker rm -f minginx #Forza terminar todo en 1 solo comando<br>
docker container run -d -p8080:80 nginx<br>
docker exec -it namecontainer bash #Modo interactivo sesion tipo putty con bash que suele venir en la mayoria o sh que es otra terminal<br>

docker volume create nombre-volume<br>
docker volume ls<br>
docker volume inspect<br>
docker run -d --name mysql-volume -v docker-curso:/var/lib/msql -p 3311:3306 MYSQL_ROOT_PASSWORD=ADMIN mysql<br>
VOLUMENES ADMINISTRADOS DE FORMA MANUAL<br>
Crear carpeta e ingresar a ella:<br>
mkdir curso docker<br>
con pwd obtenemos el path /c/Personal/Docker<br>
docker run -dit -v /c/Personal/Docker:/docker-curso -p 3311:3306 MYSQL_ROOT_PASSWORD=ADMIN mysql<br>
crear el archivo Dockerfile<br>
FROM ubuntu<br>
RUN apt-get update && apt-get install -y \  #El comando RUN solo funciona a la hora de compilar<br>
     python3 \
     curl \
     nano
-t es el tag o nombre el PUNTO del final indica que dockerfile esta en la misma carpeta<br>
docker build -t ubuntu-with-python .<br>
docker run -it ubuntu-with-python #abre sesion de ubuntu por linea edcomandos con las instalaciones que habiamos indicado
<br>
Copiando archivos <br>
COPY . /app #copia todos los archivos de donde estamos a la carpeta app<br>
WORKDIR /app #deja el directorio de traabjoautomaticamente en app<br>
ENV DEBIAN_BACKEND=ADMIN #define una variable de entorno no editable<br>
ENV version=1.0<br>

ARG TEXT_EDITOR=nano #crea un argumento para poder dejar por sdefecto a instalar nano o hacer build-args para en vez de nano vim<br>
CMD ["nginx", "-g", "daemon off;"]#ejecuta luego de inicializada la imgen es como una tarea programada al iniciar la imagen<br>
docker run -it ubuntu-with-python:v5<br>
docker ps #para ver el id<br>
docker exec -it id bash #levanta la sesion por terminal <br>
curl localhost #dedvuelve el servicio de nginx<br>
ingresando dentro de la -it con curl localhost podemos ver que si esta corriendo nginx<br>
ENTRYPOINT ["nginx", "-g", "daemon off;"]#HACE LO MISMO QUE cmd PERO NO ES SOBRE ESCRITO POR LA LINEA DE COMANDOS
<br>
Para publicar nuestras imagenes a equipos de trabajo :<br>
Ingresamos a docker hub y ceramos un repositorio quedando miUser/nomnreImage<br>
docker login #ingresamos el user y la pass<br>
docker image tag ubuntu-with-nginx miUser/nomnreImage:v1<br>
docker push miUser/nomnreImage:v1<br>

