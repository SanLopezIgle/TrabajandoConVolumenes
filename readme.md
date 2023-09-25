# Tarea trabajando con volumenes

1. Descarga la imagen 'httpd' y comprueba que está en tu equipo.
```
docker pull httpd
docker image ls
```
2. Crea un contenedor con el nombre 'dam_httpd'.
```
docker run -dit --name dam_httpd httpd:2.4
```
3. Mapea el puerto 80 del contenedor con el puerto 8000 de tu máquina.

Primero tenemos que parar y borrar el contenedor anterior ya que después de crearlo ya no hay forma de mapear los puertos.
```
docker stop dam_httpd
docker rm dam_httpd
docker run -d --name dam_httpd -p 8000:80 httpd:2.4
```

4. Utiliza bind mount para que el directorio del apache2 'htdocs' este montado un directorio que tu elijas.

        Utiliza -v "$PWD"/htdocs:/usr/local/apache2/htdocs/

Primero creamos el repositorio que queremos:
```
mkdir htdocs
```
Para mapear los directorios ponemos esto (primero paramos y borramos el contenedor como hicimos antes)
```
docker run -d --name dam_httpd -p 8000:80 -v /home/dam2/Documentos/sxe/tarea2/TrabajandoConVolumenes/htdocs:/usr/local/apache2/htdocs httpd:2.4
```

5. Realiza un 'hola mundo' en html y comprueba que accedes desde el navegador.
6. Crea un volumen para este mismo fin.
7. Crea un contenedor 'dam_web1' que use este volumen para el 'htdocs'
8. Utiliza Code para hacer un hola mundo en html
9. Crea otro contenedor 'dam_web2' con el mismo volumen y a otro puerto, por ejemplo 9080.
10. Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador:
        http://localhost:9080 
        http://localhost:8000
11. Tienen que salir la misma página web
