<center>

# TRABAJO CON VIRTUAL HOSTS


</center>

***Nombre:Bruno Amancio González Gorrín***
***Curso:*** 2º de Ciclo Superior de Administración de Sistemas Informáticos en Red.

### ÍNDICE

+ [Introducción](#id1)
+ [Objetivos](#id2)
+ [Material empleado](#id3)
+ [Desarrollo](#id4)
+ [Conclusiones](#id5)


#### ***Introducción***. <a name="id1"></a>

El objetivo de la práctica es crear 4 webs en nuestro servidor de Nginx. Para esto se nos dan los siguientes objetivos.

#### ***Objetivos***. <a name="id2"></a>

Los objetivos a cumplir son los siguientes:

    +Acceder mediante http://imw.nombre_alumno.me
        Debe mostrar una página con la imagen del "Diagrama de unidades de trabajo" de IMW"
    
    -La imagen no debe ser enlazada en remoto, sino  que se debe descargar al directorio de trabajo en la máquina de producción, y luego usar un tag <img> apuntando a la ruta local.

    +Acceder mediante http://imw.nombre_alumno.me/mec/
        No utilizar un location.
        Debe mostrar una página con un enlace al Real decreto del título de Administración de Sistemas Informáticos en Red - MEC (ver moodle de la asignatura).

    +Acceder mediante http://varlib.nombre_alumno.me:9000
    Debe mostrar el listado de ficheros y directorios de /var/lib de la máquina de producción.
    Pensar qué root definir para conseguir el objetivo planteado.

    +Acceder mediante https://ssl.nombre_alumno.me/students/ (ojo, es https!)
    Debe pedir usuario/clave. Los datos son:
        USUARIO: usuario1
        CLAVE: 2asir
    Debe mostrar una página web con el nombre de todo el alumnado de clase.
    Se debe prohibir explícitamente el acceso al fichero htpasswd

    +Acceder mediante http://redirect.nombre_alumno.me

    Se debe redirigir cualquier petición de este dominio a http://target.aluXXXX.me
        http://redirect.nombre_alumno.me/test/ -> http://target.nombre_alumno.me
        http://redirect.nombre_alumno.me/probando/ -> http://target.nombre_alumno.me
        http://redirect.nombre_alumno.me/hola/ -> http://target.nombre_alumno.me
        ...

    Al acceder a http://target.nombre_alumno.me se debe mostrar la página web que se adjunta en el archivo initializr-verekia-4.0.zip.
        Para copiar y descomprimir el fichero initializr.zip se recomienda usar alguna de las siguientes herramientas: curl, wget, scp, unzip.

    Los logfiles deben ser:
        /var/log/nginx/redirect/access.log
        /var/log/nginx/redirect/error.log


#### ***Material empleado***. <a name="id3"></a>

En esta práctica se usa una máquina virtual con entorno de terminal, a la que accedemos mediante ssh.

#### ***Desarrollo***. <a name="id4"></a>

Para la primera web tenemos que crear una nueva carpeta en webapps, donde guardaremos todo lo relacionado con nuestra página (index y la foto).
En la carpeta /nginx/sites-available tenemos que crear un archivo, en este caso imw.bruno.me y dentro ponemos lo siguiente.

![](img/b.png)

Tenemos que conseguir la imagen.

Despueś de hacer esto hacemos el enlace simbólico hacia la carpeta sites-enabled.

![](img/c.png)

Nuestro index queda de la siguiente manera.

![](img/d.png)

Nuestra página quedaría de la siguiente manera, después de finalizar lo anterior.

![](img/a.png)

Pasamos a la segunda página web. En este caso tendremos que generar una página que nos rediriga a un enlace del BOE sobre el CFGS ASIR.
Nuestro index quedaría de la siguiente manera.

![](img/e.png)

Si entramos mediante la dirección imw.bruno.me/mec, llegamos a los siugiente.

![](img/f.png)

En la tercera página web tenemos que generar una página que nos muestre una lista de ficheros del directorio 
/var/lib. El archivo de Nginx que creamos es el siguiente.

![](img/g.png)

El resultado es el siguiente.

![](img/i.png)

Como se puede ver, hemos accedido mediante el puerto 9000 (:9000). Para especificar un puerto en concreto tenemos que añadir lo siguiente en nuestro archivo de Nginx.

![](img/j.png)

La siguiente página nos requiere que se nos pregunte contraseña y usuario al entrar.
El archivo que generamos en Nginx es el siguiente.

![](img/l.png)

El index es este. Generamos un listado de alumnos.

![](img/m.png)

Intentamos acceder.

![](img/k.png)

Es importante haber editado el archivo htpasswd, y cifrar la contraseña, de lo contrario no funcionará.
Vemos que podemos entrar.

![](img/o.png)

Cambiamos los permisos de htpasswd para que nadie pueda acceder a él, o editarlo. Solo el usuario root.

![](img/p.png)

La última web se basa en una redireccionadora a otra web llamada target.bruno.me. Primero nos descargamos la página objetivo, que será la que se alojará en target. La pasamos por ssh de la máquina local a la remota de la siguiente manera.

![](img/q.png)

El archivo Nginx para redireccionar es este.

![](img/x.png)

Y el target este.

![](img/y.png)

El directorio Webapps queda de la siguiente manera.

![](img/w.png)

Entramos y podremos ver que nos redirige correctamente.

![](img/r.png)

![](img/s.png)

Y entramos correctamente.

![](img/t.png)

Si intentamos acceder con una ruta alterna a la original, como en la primera página web, nos redirige de la misma manera.

![](img/u.png)

![](img/v.png)



> ***IMPORTANTE:*** si estamos capturando una terminal no hace falta capturar todo el escritorio y es importante que se vea el nombre de usuario.

Si encontramos dificultades a la hora de realizar algún paso debemos explicar esas dificultades, que pasos hemos seguido para resolverla y los resultados obtenidos.

#### ***Conclusiones***. <a name="id5"></a>

Hemos logrado profundizar en las funcionalidades de Nginx, pudiendo crear directorios de ficheros, redireccionamientos, etc.