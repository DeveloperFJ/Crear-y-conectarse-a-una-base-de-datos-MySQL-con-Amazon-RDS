# Crear y conectarse a una base de datos MySQL con Amazon-RDS
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

_____________________________________________________________________________________________________________________________________________________________________

f. Se está creando su instancia de base de datos.  Haga clic en View Your DB Instances (Ver sus instancias de base de datos).

Nota: Dependiendo de la clase de la instancia de base de datos y el almacenamiento asignado, la nueva instancia de base de datos podría tardar varios minutos en estar disponible.

   La nueva instancia de base de datos aparece en la lista de instancias de base de datos en la consola de RDS. La instancia de base de datos se encontrará en estado 
   creating (creándose) hasta que esté creada y lista para utilizar.  Cuando el estado cambie a available (disponible), podrá conectarse a una base de datos de la 
   instancia de base de datos. 

Si lo desea, puede pasar al siguiente paso mientras espera a que la instancia de base de datos esté disponible.![7](https://user-images.githubusercontent.com/112997883/204109375-a0ee8d9c-1ef4-44e3-83f8-486e880de1d7.png)
_____________________________________________________________________________________________________________________________________________________________________

Paso 2: Descargar un cliente SQL
Una vez que se haya creado la instancia de base de datos y se encuentre en estado "available", puede conectarse a una base de datos de la instancia de base de datos con cualquier cliente SQL estándar. En este paso, descargaremos MySQL Workbench, que es un cliente SQL popular.

a. Vaya a la página de Download MySQL Workbench (Descargar MySQL Workbench) para descargar e instalar MySQL Workbench. Para obtener más información sobre el uso de MySQL, consulte la documentación de MySQL.

Nota: Recuerde ejecutar MySQL Workbench en el mismo dispositivo con el que ha creado la instancia de base de datos. El grupo de seguridad en el que se encuentra su base de datos está configurado para permitir solamente la conexión del dispositivo en el que ha creado la instancia de base de datos.
![8](https://user-images.githubusercontent.com/112997883/205104154-5079dd9c-0443-4024-83ee-5a1f839f3add.png)
_____________________________________________________________________________________________________________________________________________________________________


b. Se le preguntará si desea iniciar sesión, registrarse o comenzar la descarga.  Puede hacer clic en No thanks, just start my download  (No, gracias, comenzar la descarga) para realizar la descarga con rapidez.
![9](https://user-images.githubusercontent.com/112997883/205104479-37e3f598-5495-494b-a0dc-0eba20a15842.png)
_____________________________________________________________________________________________________________________________________________________________________


Paso 3: Conectarse a la base de datos MySQL
En este paso, nos conectaremos a la base de datos que ha creado con MySQL Workbench.

_____________________________________________________________________________________________________________________________________________________________________


a. Inicie la aplicación MySQL Workbench y vaya a Database > Connect to Database (Base de datos > Conectar con base de datos) (Ctrl+U) desde la barra de menú.

![10](https://user-images.githubusercontent.com/112997883/205104872-bcadf8db-401f-4942-b68c-4b52def1ba30.png)
_____________________________________________________________________________________________________________________________________________________________________

b. Aparecerá un cuadro de diálogo.  Escriba lo siguiente:

Hostname (Nombre de host): puede encontrar su nombre de host en la consola de Amazon RDS, tal y como se muestra en la imagen de la derecha.  
Port (Puerto): el valor predeterminado debería ser 3306.
Username (Nombre de usuario): escriba el nombre de usuario que ha creado para la base de datos de Amazon RDS.  En este tutorial, es “masterUsername“.
Password (Contraseña): haga clic en Store in Vault (o Store in Keychain en MacOS) e introduzca la contraseña que usó al crear la base de datos de Amazon RDS.
Haga clic en OK.
![11](https://user-images.githubusercontent.com/112997883/205105053-524fa600-8391-4e4a-8218-1db6950ddf03.png)

_____________________________________________________________________________________________________________________________________________________________________

c. ¡Ya se ha conectado a la base de datos! En MySQL Workbench, verá varios objetos de esquema disponibles en la base de datos. Ya puede comenzar a crear tablas, introducir datos y realizar consultas.
_____________________________________________________________________________________________________________________________________________________________________

Paso 4: Eliminar la instancia de base de datos
Puede eliminar con facilidad la instancia de base de datos MySQL desde la consola de Amazon RDS. Se recomienda eliminar las instancias que ya no utilice para que no le sigan cobrando por ellas.
_____________________________________________________________________________________________________________________________________________________________________
a. Vuelva a la consola de Amazon RDS. Seleccione Databases (Base de datos), elija la instancia que desee eliminar y luego seleccione Delete (Eliminar) en el menú desplegable Actions (Acciones).
![13](https://user-images.githubusercontent.com/112997883/205105497-77d6233b-94d6-40f6-b3c1-9c601390882c.png)
_____________________________________________________________________________________________________________________________________________________________________
b. Deberá crear una captura de imagen final y confirmar la eliminación. En nuestro ejemplo, no cree una captura de imagen final, confirme que desea eliminar la instancia y luego haga clic en Delete. 

    Nota: La eliminación de la instancia de base de datos puede tardar unos minutos.
    
![14](https://user-images.githubusercontent.com/112997883/205105742-63fd9bcf-17ba-4b7f-9a32-b9abb025abcf.png)
_____________________________________________________________________________________________________________________________________________________________________
¡Felicitaciones!
Ha creado una instancia de base de datos MySQL, se ha conectado a ella y la ha eliminado con Amazon RDS.  Amazon RDS facilita las tareas de configuración, utilización y escalado de bases de datos relacionales en la nube. Proporciona capacidad rentable y de tamaño modificable y, al mismo tiempo, se encarga de las tediosas tareas de administración de la base de datos, lo que le permite centrarse en sus aplicaciones y en su negocio.
