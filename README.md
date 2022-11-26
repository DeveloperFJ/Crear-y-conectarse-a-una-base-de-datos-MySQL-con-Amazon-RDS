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
_____________________________________________________________________________________________________________________________________________________________________

d. Ahora debe configurar su instancia de base de datos. La siguiente lista muestra un ejemplo de la configuración que puede utilizar para este tutorial:

Especificaciones de la instancia:

Modelo de licencia: seleccione la licencia pública general predeterminada para usar el acuerdo de licencia general para MySQL. MySQL tiene solamente un modelo de licencia.
Versión del motor de la base de datos: seleccione la versión predeterminada de MySQL. Tenga en cuenta que Amazon RDS admite múltiples versiones de MySQL en determinadas regiones.
Clase de la instancia de base de datos: seleccione db.t2.micro --- 1vCPU, 1 GIB RAM.  Eso equivale a 1 GB de memoria y 1 vCPU. Para ver una lista de clases de instancias compatibles, consulte los detalles del producto de Amazon RDS.
Implementación Multi-AZ: tenga en cuenta que las implementaciones Multi-AZ conllevan un cargo. Usar una implementación Multi-AZ aprovisionará y mantendrá automáticamente una réplica en espera síncrona en una zona de disponibilidad distinta.  Para obtener más información, consulte Implementación de alta disponibilidad.
Tipo de almacenamiento: seleccione General Purpose (SSD) (Uso general, SSD). Para obtener más información acerca del almacenamiento, consulte Almacenamiento para Amazon RDS.
Almacenamiento asignado: seleccione el valor predeterminado 20 para asignar 20 GB de almacenamiento a su base de datos.  Puede escalar hasta un máximo de 16 TB con Amazon RDS for MySQL.
Habilitar el escalado automático del almacenamiento: si la carga de trabajo es cíclica o impredecible, debe habilitar el escalado automático del almacenamiento para permitir que RDS aumente automáticamente su almacenamiento cuando sea necesario. Esta opción no se aplica a este tutorial.
Configuración:

Identificador de instancias de base de datos: escriba un nombre para la instancia de base de datos que sea exclusivo para su cuenta en la región que haya seleccionado. En este tutorial, elegiremos el nombre rds-mysql-10minTutorial.
Nombre de usuario maestro: escriba el nombre de usuario que utilizará para iniciar sesión en su instancia de base de datos. En este ejemplo, usaremos masterUsername.
Contraseña maestra: escriba una contraseña que contenga entre 8 y 41 caracteres ASCII imprimibles (excluidos /," y @) para la contraseña del usuario maestro.
Confirmar contraseña: vuelva a escribir la contraseña.
Almacenamiento asignado: escriba 5 para asignar 5 GB de almacenamiento a su base de datos. Si desea obtener más información acerca de la asignación de almacenamiento, consulte las características de Amazon Relational Database Service (pedido de cambio, su tipo de almacenamiento posterior)
Haga clic en Next (Siguiente).
![5](https://user-images.githubusercontent.com/112997883/204104638-d61c3e97-5bc2-453d-b058-df3ddff8737e.png)
_____________________________________________________________________________________________________________________________________________________________________

e. Ahora se encuentra en la página Configure Advanced Settings (Configuración avanzada), donde puede proporcionar información adicional que RDS necesita para implementar la instancia de base de datos MySQL. La siguiente lista muestra la configuración de nuestra instancia de base de datos de ejemplo.
Red y seguridad
Virtual Private Cloud (VPC): seleccione Default VPC (VPC predeterminada). Para obtener más información sobre las VPC, consulte Amazon RDS y Amazon Virtual Private Cloud (VPC).
Subnet group (Grupo de subred): elija el grupo de subred predeterminado. Para obtener más información sobre los grupos de subred, consulte Trabajo con grupos de subred de base de datos.
Public accessibliity (Accesibilidad pública): seleccione Yes (Sí). Se asignará una dirección IP para su instancia de base de datos de forma que pueda conectarse directamente a la base de datos desde su propio dispositivo.
Availability zone (Zona de disponibilidad): elija No Preference (Sin preferencias). Para obtener más información, consulte Regiones y zonas de disponibilidad.
VPC security groups (Grupos de seguridad de VPC): seleccione Create new VPC security group (Crear nuevo grupo de seguridad de VPC). Se creará un grupo de seguridad que permitirá la conexión de la dirección IP del dispositivo que está utilizando en la actualidad a la base de datos creada.
Opciones de base de datos

Database name (Nombre de la base de datos): escriba un nombre de la base de datos que contenga entre 1 y 64 caracteres alfanuméricos. Si no introduce un nombre, Amazon RDS no creará una base de datos automáticamente en la instancia de base de datos que está creando.
Port (Puerto): deje el valor por defecto, 3306.
DB parameter group (Grupo de parámetros de la base de datos): deje el valor por defecto, default.mysql5.6. Para obtener más información, consulte Trabajo con los grupos de parámetros de base de datos.
Option group (Grupo de opciones): seleccione el valor predeterminado, default.mysql5.7. Amazon RDS usa grupos de opciones para habilitar y configurar características adicionales.  Para obtener más información, consulte Trabajo con grupos de opciones.
Autenticación de base de datos IAM: seleccione Disable (Deshabilitar). Esta opción le permite administrar las credenciales de la base de datos usando los grupos y usuarios de AWS IAM.
Cifrado

Esta opción no está disponible en la capa gratuita. Para obtener más información, consulte Cifrado de recursos de Amazon RDS.

Copia de seguridad

Periodo de retención del backup: puede elegir la cantidad de días que se retiene el backup que realice. Para este tutorial, elija el valor 1 día.
Ventana de backup: seleccione el valor predeterminado, No Preference (Sin preferencias).
Monitorización

Monitorización mejorada: seleccione Disable enhanced monitoring (Deshabilitar monitorización mejorada) para permanecer dentro de la capa gratuita. La monitorización mejorada le aporta métricas en tiempo real del sistema operativo (SO) en el que se ejecuta su instancia de base de datos. Para obtener más información, consulte Ver métricas de instancia de base de datos.
Información sobre rendimiento

Seleccione Disable Performance Insights (Deshabilitar información sobre rendimiento) para este tutorial.

Mantenimiento

Actualización de versión secundaria automática: seleccione Enable auto minor version upgrade (Habilitar actualización de versión secundaria automática) para obtener actualizaciones automáticas cuando estén disponibles.
Ventana de mantenimiento: seleccione No Preference (Sin preferencias).
Protección ante eliminaciones

Elimine Enable deletion protection (Habilitar protección de eliminación) para este tutorial. Cuando esta opción está habilitada, no puede eliminar la base de datos.
 

Haga clic en Create database (Crear base de datos).

![6](https://user-images.githubusercontent.com/112997883/204104809-401f6d2e-f045-4861-be77-dd305c9b9479.png)





