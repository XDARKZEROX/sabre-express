# Sabre Connector Express [![][project-version]][npm-url]
> Un servicio REST construido en NodeJS y el framework ExpressJS4

Un servicio REST que permite la búsqueda de vuelos utilizando el motor de Sabre (SOAP).

- [Introducción](#introduccion)
- [Caracteristicas:](#caracteristicas)
- [Estructura del Proyecto:](#estructura-del-proyecto)
- [Enviroments:](#enviroments)
- [Servicios:](#servicios)
    - [SessionCreate](#SessionCreate)
    - [SessionClose](#SessionClose)
    - [BargainFinderMax](#BargainFinderMax)

## Introducción

En desarrollo.

## Características

* Una API muy simple de manipular
* Permite la opción de despleglarse como un servicio REST o SOAP (véase branch sabre-connector-rest)

## Estructura del Proyecto

![Alt text](https://cloud.githubusercontent.com/assets/4942140/16822753/4c37e56e-4924-11e6-881e-33efbdb7d81e.png "Sabre Connector Express Structure")

 - **app:** Contiene la estructura principal del proyecto basado en el modelo MVC.
 - **bin:** Contiene el archivo de configurador del servidor.
 - **config:** Archivos de configuracion para librerias.
 - **lib:** Librerias adicionales que no vienen directamente del package manager.
 - **logs:** (solo usar en Development) Carpeta que contiene los logs.
 - **middlewares:** 
 - **routes:** 
 - **test:** Archivos de testing usando la libreria mocha.

En desarrollo.

## Enviroments
El proyecto posee constantes que serán cargadas dependiendo del Enviroment ('developtment' o 'production').
Por defecto el proyecto se inicia siempre en development mode.

Para cambiar de entorno de desarrollo:
* Abrir la consola y ubicarse en el proyecto.
* Digitar 'set NODE_ENV=production' o set 'NODE_ENV=development' segun el entorno en que usará (digitarlo sin comillas)
* Levantar el proyecto digitando: node app.js

```
  set NODE_ENV=production o NODE_ENV=development
```

## Servicios
### SessionCreate:
Este servicio permite la autenticación a Sabre para poder generar los demás servicios (búsqueda, reserva, cancelación, etc) retornando un token de sesión que se utilizará al momento de invocar a los demás servicios.

En SOAP este servicio solo permite una cantidad de limitada de sesiones activas por lo que cada vez que se llame este servicio posteriormente deberá invocarse el servicio de `SessionClose` para liberar la sesión y evitar la sobrecarga. 

### SessionClose:
Este servicio permite liberar la sesión activa o en uso para evitar la sobrecarga de user tokens (recordar que SessionCreate tiene un número limitado de conexiones abiertas).

Este servicio debe ser ejecutado despues de llamar al servicio `SessionCreate` y recibiendo como parámetro el token de sesión que SessionCreate otorga en su response.

### BargainFinderMax:
En desarrollo.

## Información adicional:

### Códigos de estados de los segmentos antes de reservar

```
HK = "Held Confirmed" (reservation but not ticketed)
OK = "OK" (ticketed and confirmed)
SS = "Seat Saved" (reservation with seat assignment)
RQ = Waitlisted
NN = "Need/Need" (seat requested)
CV = "Checked In/Virtual" (checked in via internet)
```

[project-version]: https://img.shields.io/badge/version-1.0.1-brightgreen.svg
[npm-url]: https://npmjs.org/package/soap
