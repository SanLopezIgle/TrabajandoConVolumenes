# Tarea trabajando con volumenes

1. Descarga la imagen 'httpd' y comprueba que está en tu equipo.
```
docker pull httpd
docker image ls
```
2. Crea un contenedor con el nombre 'dam_web1'.
```
docker run -dit --name dam_web1 httpd:2.4
```
3. Si quieres poder acceder desde el navegador de tu equipo, ¿qué debes hacer?

Primero paro y borro el contenedor creado antes y vuelvo a crearlo mapeando los puertos para poder acceder desde el navegador.
```
docker stop dam_web1
docker rm dam_web1
docker run -d --name dam_web1 -p 8000:80 httpd:2.4
```
**En el navegador:**
```
IP:puertoHost (10.0.9.14:8000)
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

Dentro del directorio que creamos antes, **htdocs**, creamos nuestro archivo .html y para acceder desde el navegor escribimos: 

**IP:puertoHost/hola.html** (http://10.0.9.14:8000/hola.html)

6. Crea otro contenedor 'dam_web2' con el mismo volumen y a otro puerto, por ejemplo 9080.
```
docker run -d --name dam_httpd -p 9080:80 -v /home/dam2/Documentos/sxe/tarea2/TrabajandoConVolumenes/htdocs:/usr/local/apache2/htdocs httpd:2.4
```
7. Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador:

    http://localhost:9080

    http://localhost:8000

8. Realiza modificaciones de la página y comprueba que los dos servidores 'sirven' la misma página



