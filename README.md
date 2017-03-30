# libredte-webapp-docker

Esta imagen Docker contiene una instalación básica de LibreDTE, construida
siguiendo los pasos descritos en el repositorio oficial de LibreDTE.

La configuración utilizada es la que viene por defecto (`libredte/website/Config/core.php`).
El archivo `core.php` esta modificado para aceptar configuraciones definidas como variables de entorno.

Docker Hub: https://hub.docker.com/r/mibanez/libredte/

Configuración
-------------

Configuración para la base de datos postgres

DB_HOST: default 'db'
DB_PORT: default '5432'
DB_USER: default 'postgres'
DB_PASS: default ''
DB_NAME: default 'libredte'

Configuración para el correo electrónico

EMAIL_TYPE: default 'smtp'
EMAIL_HOST: default 'ssl://smtp.gmail.com'
EMAIL_PORT: default 465
EMAIL_USER: default ''
EMAIL_PASS: default ''
EMAIL_FROM_EMAIL: default ''
EMAIL_FROM_NAME: default 'LibreDTE'
EMAIL_TO: default ''

Contraseña que se usará para encriptar datos sensibles en la BD (DEBE ser de 32 chars)

DTE_PKEY: default ''

Configuración para firma electrónica

ESIGN_FILE: default 'default.p12' (archivo debe estar ubicado en /data/firma_electronica)
ESIGN_PASS: default ''

Volumenes

En LibreDTE se deben configurar los directorios "logos" y "firma_electronica".
Por defecto en esta imagen estos directorios son /data/logos y /data/firma_electronica respectivamente.


Ejemplo de uso
--------------

1 - Levantar postgres y configurarlo (https://hub.docker.com/_/postgres/)
```bash
docker run -v /my/psql/data:/var/lib/postgresql/data --name mypostgres -d postgres:latest
```

2 - Crear base de datos y tablas siguiendo las indicaciones oficiales (https://github.com/LibreDTE/libredte-webapp/blob/master/INSTALL.md)

3 - Levantar libredte linkeado a postgres y con la configuracion deseada
```bash
docker run -d -p 8080:80 --link mypostgres:db \
  -v /my/libredte/data/logos:/data/logos \
  -v /my/libredte/data/firma_electronica/:/data/firma_electronica/ \
  -e DB_HOST=db \
  -e DB_USER=libredte \
  -e DB_PASS=libredte \
  -e DB_NAME=libredte \
  -e EMAIL_USER=foo@gmail.com \
  -e EMAIL_PASS=foopass \
  -e EMAIL_FROM_EMAIL=foo@gmail.com \
  -e EMAIL_FROM_NAME=Foo \
  -e EMAIL_TO=foo@gmail.com \
  -e DTE_PKEY=12345cmvn2345678qsed567812345678 \
  -e ESIGN_FILE=default.p12 \
  -e ESIGN_PASS=myesignpassword mibanez/libredte:latest
```

5 - En este ejemplo, libredte estará disponible en localhost:8080/libredte

Términos y condiciones de uso
-----------------------------

Al utilizar este proyecto, total o parcialmente, automáticamente se acepta
cumplir con los [términos y condiciones de uso](https://wiki.libredte.cl/doku.php/terminos)
que rigen a LibreDTE. La [Licencia Pública General Affero de GNU (AGPL)](https://raw.githubusercontent.com/LibreDTE/libredte-lib/master/COPYING)
sólo aplica para quienes respeten los términos y condiciones de uso. No existe
una licencia comercial de LibreDTE, por lo cual no es posible usar el proyecto
si no aceptas cumplir dichos términos y condiciones.

La versión resumida de los términos y condiciones de uso de LibreDTE que
permiten utilizar el proyecto, son los siguientes:

- Tienes la libertad de: usar, estudiar, distribuir y cambiar LibreDTE.
- Si utilizas LibreDTE en tu software, el código fuente de dicho software deberá
  ser liberado de manera pública bajo licencia AGPL.
- Si haces cambios a LibreDTE deberás liberar de manera pública el código fuente
  de dichos cambios bajo licencia AGPL.
- Debes hacer referencia de manera pública en tu software al proyecto y autor
  original de LibreDTE, tanto si usas LibreDTE sin modificar o realizando
  cambios al código.

Es obligación de quienes quieran usar el proyecto leer y aceptar por completo
los [términos y condiciones de uso](https://wiki.libredte.cl/doku.php/terminos).
# Docker LibreDTE
