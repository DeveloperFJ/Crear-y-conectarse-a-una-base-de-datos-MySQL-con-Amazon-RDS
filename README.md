# Crear-y-conectarse-a-una-base-de-datos-MySQL-con-Amazon-RDS
En este tutorial, aprenderá a crear un entorno para ejecutar su base de datos MySQL (a este entorno lo denominamos una instancia), conectarlo a su base de datos y eliminar la instancia de base de datos.  Para llevar adelante este proceso, utilizaremos Amazon Relational Database Service (Amazon RDS). Todos los recursos que utilizamos en este tutorial son elegibles para la capa gratuita.

Cuando haga clic aquí, se abrirá la consola de administración de AWS en una ventana nueva del navegador para que pueda seguir teniendo abierta esta guía paso a paso. Cuando se cargue esta pantalla, busque RDS en Database (Base de datos) y haga clic para abrir la consola de Amazon RDS.
_____________________________________________________________________________________________________________________________________________________________________
![1](https://user-images.githubusercontent.com/112997883/204103597-8f95fdcf-ea39-48c1-aafe-c9f3345ad09a.png)

Paso 1: Crear una instancia de base de datos MySQL
En este paso, utilizaremos Amazon RDS para crear una instancia de base de datos MySQL con una instancia de base de datos de clase db.t2.micro, 20 GB de almacenamiento y backups automatizados activados con un periodo de retención de un día. Recuerde que todo esto incluye el derecho a uso de una capa gratuita.
_____________________________________________________________________________________________________________________________________________________________________
a. En la esquina superior derecha de la consola de Amazon RDS, seleccione la región en la que desea crear la instancia de base de datos.

Nota: Los recursos en la nube de AWS se alojan en centros de datos de alta disponibilidad en distintas partes del mundo. Cada región contiene varias ubicaciones distintas denominadas zonas de disponibilidad. Puede elegir en qué región desea alojar su actividad de Amazon RDS. 
![2](https://user-images.githubusercontent.com/112997883/204104417-9611030b-eb73-4660-a0b0-4b55edb1dae8.png)
_____________________________________________________________________________________________________________________________________________________________________

b.   En la sección Create database (Crear una base de datos), seleccione Create database.
![3](https://user-images.githubusercontent.com/112997883/204104503-dbb0853d-13f2-4c2d-8b2b-bc5a6fa4c305.png)

_____________________________________________________________________________________________________________________________________________________________________

c.  Ahora dispone de varias opciones de motor.  Para este tutorial, haga clic en el ícono de MySQL, seleccione Only enable options eligible for RDS Free Usage Tier (Permitir solo opciones elegibles para la capa de uso gratuita de RDS) y luego haga clic en Next (Siguiente)
![4](https://user-images.githubusercontent.com/112997883/204104542-aa3a1b5b-b09b-4ed1-82e7-5714ff33121a.png)
