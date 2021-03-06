# IBM Cloud - PostgreSQL Despliegue 鈽侌煔?馃摎
*IBM庐 Cloud Databases for PostgreSQL* es una poderosa base de datos relacional de c贸digo abierto, que es altamente personalizable. Es una base de datos empresarial rica en funciones con soporte JSON, que le brinda lo mejor de los mundos SQL y NoSQL. Adicionalmente, puede hacer uso de *pgAdmin* una plataforma de administraci贸n de c贸digo abierto para PostgreSQL que proporciona diversas herramientas para gestionar los datos y las bases de datos.

La presente gu铆a esta enfocada en crear un despliegue de *IBM庐 Cloud Databases for PostgreSQL* y sobre la base de datos aprovisionada realizar operaciones de inserci贸n, actualizaci贸n y eliminaci贸n de datos.

<br />

## 脥ndice  馃摪
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Crear Base de datos PostgreSQL](#Crear-Base-de-datos-PostgreSQL-floppy_disk)
3. [Generar contrase帽a en servicio PostgreSQL](#Generar-contrase帽a-en-servicio-PostgreSQL-closed_lock_with_key)

#### OPCI脫N PRUEBA 1 - IBM Cloud Shell
4. [Conexi贸n con IBM Cloud Shell](#Conexi贸n-con-IBM-Cloud-Shell-electric_plug)
5. [CRUD en la base de datos con IBM Cloud Shell](#CRUD-en-la-base-de-datos-con-IBM-Cloud-Shell-pick)

#### OPCI脫N PRUEBA 2 - pgAdmin
6. [Conexi贸n con pgAdmin](#Conexi贸n-con-pgAdmin-electric_plug)
7. [CRUD en la base de datos con pgAdmin](#CRUD-en-la-base-de-datos-con-pgAdmin-hammer)
8. [Importar/Exportar datos con CSV en pgAdmin](#importarexportar-datos-con-csv-en-pgadmin-pagefacingup)
8. [Referencias](#Referencias-mag)
9. [Autores](#Autores-black_nib)
<br />

## Pre Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>.
* Contar con un grupo de recursos espec铆fico para la implementaci贸n de los recursos.
* Instalaci贸n de <a href="https://www.pgadmin.org/download/"> pgAdmin 4</a> (en caso de optar por implementar la opci贸n de prueba 2). 
<br />

## Crear Base de datos PostgreSQL :floppy_disk:
Para realizar el ejercicio lo primero que debe hacer es crear una *Base de datos PostgreSQL* en su cuenta de *IBM Cloud*. Para ello, siga los pasos que se indican a continuaci贸n:
1. Con <a href="https://cloud.ibm.com/databases/databases-for-postgresql/createl">Databases for PostgreSQL</a>, automaticamente ser谩 redirigido a la creaci贸n de la base de datos.
2. Una vez le aparezca la ventana para la configuraci贸n y creaci贸n de la *Base de Datos*, complete lo siguiente:
</br>

#### Service Details

* ```Service name```: asigne un nombre exclusivo para la *Base de Datos*. 
* ```Resource group```: seleccione el grupo de recursos en el cual va a trabajar.
* ```Location```: .seleccione la ubicaci贸n en la cual desea implementar la *Base de Datos*.
</br>

#### Resource Allocation

1.  ```Templates```: 
Puede elegir entre cuatro perfiles pre configurados Small- Medium - Large - Extra Large.

2.  ```Custom```:

* ```RAM```:  indique la capacidad de RAM en GB. Por ejemplo: 4 GB.
* ```Dedicated Cores```: indique la capacidad de cores dedicados que desea.  Por ejemplo: 0.
* ```Disk Usage```: indique la capacidad de CPU en GB. Por ejemplo: 20 GB.


Las dem谩s caracteristicas se seleccionan por defecto. 

Cuando ya tenga todos los campos configurados de click en el bot贸n ```Crear/Create```.
<br />
<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/crearDB.gif"></p>
<br />

## Generar contrase帽a en servicio PostgreSQL :closed_lock_with_key:
Para realizar la conexi贸n con la base de datos deber谩 generar una constrase帽a en el servicio. Para ello, de click en la pesta帽a ```Settings``` 鉃? ```Change Database Admin Password``` y siga los pasos a continuaci贸n:
1. Seleccione la opci贸n  ```Generate Password```.

2. Una vez sea generada, guardela.

3. De clik en ```Change Password```.
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Password.PNG"></p>
<br />

## OPCI脫N PRUEBA 1 - IBM Cloud Shell

## Conexi贸n con IBM Cloud Shell :electric_plug:
Para realizar la conexi贸n y prueba de la base de datos con el Shell de *IBM* realice lo siguiente:

1. Dentro de su cuenta de *IBM Cloud* acceda al ```IBM Cloud Shell``` dando click en la pesta帽a <a href="https://cloud.ibm.com/shell"> <img width="25" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Shell_IBM.PNG"></a>, que se ubica en la parte superior derecha del portal. 
<br />

2. Aseg煤rese de estar en la regi贸n en donde tiene desplegada su base de datos. Si debe cambiar la regi贸n utilice el comando:
```
ibmcloud target -r <region>
```

> NOTA: Reemplace el par谩metro \<region> con su respetiva informaci贸n. Por ejemplo: ```us-south``` para Dallas y ```us-east``` para Washington.
<br />

3. Aseg煤rese de tener seleccionado el grupo de recursos en donde tiene desplegada su base de datos. Para ello, utilice el comando:
```
ibmcloud target -g <grupo_recursos>
```

> NOTA: Reemplace el par谩metro \<grupo_recursos> con su respetiva informaci贸n. 
<br />
 
4. Luego de establecer la regi贸n y el grupo de recursos, coloque el siguiente comando para instalar el plugin ***ibmcloud cdb***:
```
ibmcloud plugin install cloud-databases
```
<br />

5. Cuando le pregunte si desea actualizar el plugin, coloque ```y```.
<br />

6. Para conectarse con el deployment de la base de datos en *IBM Cloud Shell*, copie el endpoint que sale en la secci贸n ```Overview``` del servicio 鉃? ```Endpoints``` 鉃? ```Quick start``` 鉃? ```2. Connect to your deployment``` y coloquelo en el shell de *IBM*.
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CopiarEndpoint.PNG"></p>
<br />

7. Escriba la contrase帽a establecida en el paso [Generar contrase帽a en servicio PostgreSQL](#Generar-contrase帽a-en-servicio-PostgreSQL-closed_lock_with_key) y presione enter.
<br />

<p align="center"><img width="1000" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Acceso_IBM_Cloud_Shell_Final.PNG"></p>
<br />

## CRUD en la base de datos con IBM Cloud Shell :pick:
Una vez se ha creado y conectado el servicio de base de datos con *IBM Cloud Shell*, se contin煤a el ejercicio con las operaciones del CRUD (Create, Read, Update & Delete). Para ello, se presentan a continuaci贸n los pasos que se deben realizar para llevar a cabo cada una de estas operaciones:
<br />

### 1. Crear instancia de base de datos
Para crear una instancia del servicio de base de datos implementada, complete los siguientes pasos:
<br />

a. En el *IBM Cloud Shell* cree una instancia con el comando:
```
create database nombre_instancia;
```
<br />

Ejemplo:
```
create database ccedb;
```
<br />

b. Genere el listado de instancias existentes de la base de datos con el comando ```\l```.

<br />

c. Mu茅vase a la instancia creada anteriormente, para ello utilice:
```
\c nombre_instancia
```
<br />

Ejemplo:
```
\c ccedb;
```
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CrearDB_Final.PNG"></p>
<br />

### 2. Crear tabla
Teniendo en cuenta que ya se encuentra dentro de la base de datos, se debe crear la tabla en la cual se van a almacenar los datos. Para ello, realice lo siguiente:
<br />

a.  En el *IBM Cloud Shell* cree la tabla mediante el comando:
<br />

```
CREATE TABLE nombre_tabla (id serial, columna_1 tipo_dato, columna_2 tipo_dato, ... , columna_n tipo_dato, primary key (id));
```
<br />

Ejemplo:
```
CREATE TABLE transacciones (id serial, nombre varchar(30), apellido varchar(30), ciudad varchar(30), direccion varchar(30), cedula integer, fecha date, valor integer, tipo varchar(30), primary key (id));
```
<br />

b. Para ver la lista de las tablas creadas utilice el comando ```\dt```
<br />

<p align="center"><img width="1000" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CrearTabla_IBM_Shell_Final.PNG"></p>
<br />

### 3. Agregar y visualizar datos
El paso siguiente consiste en insertar datos en la tabla que se acaba de crear, para ello realice lo siguiente:
<br />

a. Coloque el siguiente comando en el *IBM Cloud Shell*:
```
INSERT INTO nombre_tabla (columna_1, columna_2, ... , columna_n) VALUES(valor_1, valor_2, ... , valor_n);
```
<br />

Ejemplo:
```
INSERT INTO transacciones (nombre, apellido, ciudad, direccion, cedula, fecha, valor, tipo) VALUES('Diana', 'Espitia', 'Bogot谩', 'Cra. 53 No. 100- 25', 1234567890, '03/08/2021', 200000, 'Consignaci贸n');
```
<br />

b. Para ver la informaci贸n de la tabla con los datos insertados utilice el comando:
```
select * from nombre_tabla;
```
<br />

Ejemplo:
```
select * from transacciones;
```
<br />

<p align="center"><img width="1000" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Insertar_IBM_Shell_Final.PNG"></p>
<br />

### 4. Actualizar y visualizar datos
Para actualizar los datos registrados en la tabla, realice lo siguiente:

<br />

a. Coloque el siguiente comando en el *IBM Cloud Shell*:
```
UPDATE nombre_tabla set columna_1=valor_nuevo where id=1;
```
<br />

Ejemplo:
```
UPDATE transacciones set nombre='Andrea' where id=1;
```
<br />

> NOTA: utilice el ```id``` para identificar que transacci贸n desea modificar (en este caso el id de la transacci贸n 1). 
<br />

b. Para ver la informaci贸n de la tabla con las modificaciones realizadas utilice el comando:
```
select * from nombre_tabla;
```
<br />

Ejemplo:
```
select * from transacciones;
```
<br />

<p align="center"><img width="800" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Actualizar_IBM_Shell_Final.PNG"></p>
<br />

### 5. Eliminar datos
Para eliminar los datos registrados en la tabla, realice lo siguiente:

<br />

a. Coloque el siguiente comando en el *IBM Cloud Shell*:
```
DELETE FROM nombre_tabla WHERE id=1;
```
<br />

Ejemplo:
```
DELETE FROM transacciones WHERE id=1;
```
<br />

> NOTA: utilice el ```id``` para identificar que transacci贸n desea eliminar (en este caso el id de la transacci贸n 1). 
<br />

b. Para ver las modificaciones realizadas en la tabla utilice el comando:
```
select * from nombre_tabla;
```
<br />

Ejemplo:
```
select * from transacciones;
```
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Eliminar_IBM_Shell_Final.PNG"></p>
<br />

## OPCI脫N PRUEBA 2 - pgAdmin

## Conexi贸n con pgAdmin :electric_plug:
1. Cuando abra *pgAdmin* por primera vez, se le solicita establecer una contrase帽a primaria, la cual ser谩 requerida cada vez que abra la aplicaci贸n.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Password_inicio_pgadmin.PNG"></p>
<br />

2. Consulte la informaci贸n relevante del servicio de *Databases for PostgreSQL* creado en *IBM*, la cual ser谩 requerida en el paso siguiente.

* Ingrese a  ```Overview```, despl谩cese hasta el final de la p谩gina ```Endpoints``` > ```PostgreSQL```.
* Identifique el ```Hostname```
* Identifique el ```Port```
* Identifique el ```SSL Mode```
* Descargue el ```TLS certificate```
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Credenciales.PNG"></p>
<br />

3. En *pgAdmin*, ```Dashboard``` seleccione ```Add New Server```. A continuaci贸n se desplegar谩 una ventana en donde debe llenar los siguientes campos:

En la pesta帽a ```General```:

* ```Name```: asigne un nombre exclusivo para el servicio.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Conexion_pgAdmin_parte1.PNG"></p>

En la pesta帽a ```Connection```:

* ```Host name/address```: Indique el ```Hostname``` de la informaci贸n relevante de la base de datos.
* ```Port```: Indique el ```Port``` de la informaci贸n relevante de la base de datos.
* ```Maintenance database```: postgres
* ```Username```: admin
*  ```Password```: Indique la contrase帽a establecida en el paso [Generar contrase帽a en servicio PostgreSQL](#Generar-contrase帽a-en-servicio-PostgreSQL-closed_lock_with_key).
* Los campos ```Role``` y ```Service``` pueden quedar vacios.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Conexion_pgAdmin_parte2.PNG"></p>

En la pesta帽a ```SSL```:

* ```SSL Mode```: indique el ```SSL Mode``` de la informaci贸n relevante de la base de datos.
* ```Root Certificate```: cargue el archivo del certificado descargado en el paso anterior.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Conexion_pgAdmin_parte3.PNG"></p>
<br />

Cuando tenga todas las pesta帽as configuradas, de click en ```Save``` para que *pgAdmin* se conecte a su implementaci贸n.

<br />

## CRUD en la base de datos con pgAdmin :hammer:
Una vez se ha creado y conectado la base de datos con *pgAdmin*, se contin煤a el ejercicio con las operaciones del CRUD (Create, Read, Update & Delete). Para ello, se presentan a continuaci贸n los pasos que se deben realizar para llevar a cabo cada una de estas operaciones:
<br />

### 1. Crear Tabla:
a. Teniendo en cuenta que ya existe la base de datos (*ibmclouddb* - creada al conectar el servidor), se debe crear la tabla en la cual se van a almacenar los datos. Para ello,    asegur谩ndose de tener seleccionada la base de datos en la cual va a trabajar, de click en la pesta帽a ```Tools``` y luego seleccione la opci贸n ```Query Tool```. 
<br />


b. Posteriormente, en el ```Query Editor``` coloque el siguiente comando:
 ```
CREATE TABLE nombre_tabla (id serial, columna_1 tipo_dato, columna_2 tipo_dato, ... , columna_n tipo_dato, primary key (id));
```
<br />

Ejemplo:
```
CREATE TABLE transacciones (id serial, nombre varchar(30), apellido varchar(30), ciudad varchar(30), direccion varchar(30), cedula integer, fecha date, valor integer, tipo varchar(30), primary key (id));
```

> NOTA: los valores ```id serial``` y ```primary key (id)``` se utilizan para generar el ID de la transacci贸n de forma autom谩tica. 
<br />

c. Para crear la tabla, de click en el bot贸n 鈻? (*Execute/Refresh F5*).

<br />

d. Para observar la tabla que acaba de crear, de click derecho sobre el servidor conectado y seleccione la opci贸n ```Refresh```. Por 煤ltimo, dentro de la base de datos en las opciones ```Schemas/public/Tables``` de click derecho sobre la tabla creada y seleccione la opci贸n ```View/Edit Data``` 鉃? ```All Rows```. All铆 puede visualizar la tabla y en la pesta帽a ```Data Output``` puede observar que aparecen las respectivas columnas con sus tipos de datos.

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CrearTabla.gif"></p>

<br />
 
### 2. Agregar y visualizar datos
El paso siguiente consiste en insertar datos en la tabla que se acaba de crear, para ello realice lo siguiente:

<br />

a. Dir铆jase nuevamente al ```Query Editor``` y coloque el siguiente comando:
```
INSERT INTO nombre_tabla (columna_1, columna_2, ... , columna_n) VALUES(valor_1, valor_2, ... , valor_n);
```
<br />

Ejemplo:
```
INSERT INTO transacciones (nombre, apellido, ciudad, direccion, cedula, fecha, valor, tipo) VALUES('Diana', 'Espitia', 'Bogot谩', 'Cra. 53 No. 100- 25', 1234567890, '03/08/2021', 200000, 'Consignaci贸n');
```
<br />

b. De click en el bot贸n 鈻? (*Execute/Refresh F5*) para agregar los datos a la tabla.

<br />

c. Para observar los datos en la tabla, regrese nuevamente a ```View/Edit Data``` 鉃? ```All Rows```. De click en el bot贸n 鈻? (*Execute/Refresh F5*) y a continuaci贸n podr谩 visualizar la informaci贸n que acaba de registrar. 

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/InsertarDatos.gif"></p>

<br />

### 3. Actualizar datos
Para actualizar los datos ya registrados en la tabla, realice los siguientes pasos:

<br />

a. Dir铆jase nuevamente al ```Query Editor``` y coloque el siguiente comando:
```
UPDATE nombre_tabla set columna_1=valor_nuevo where id=1;
```
<br />

Ejemplo:
```
UPDATE transacciones set nombre='Andrea' where id=1;
```
<br />

> NOTA: utilice el ```id``` para identificar que transacci贸n desea modificar (en este caso el id de la transacci贸n 1). En la imagen puede ver un ejemplo m谩s detallado.
<br />

b. De click en el bot贸n 鈻? (*Execute/Refresh F5*) para aplicar los cambios y actualizar los datos en la tabla.

<br />

c. Para observar los datos en la tabla, regrese nuevamente a ```View/Edit Data``` 鉃? ```All Rows``` en la tabla respectiva. De click en el bot贸n 鈻? (*Execute/Refresh F5*) y a continuaci贸n podr谩 visualizar la informaci贸n que acaba de modificar. 

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/ActualizarDatos.gif"></p>

<br />

### 4. Eliminar datos
Para eliminar los datos ya registrados en la tabla, realice lo siguiente:

<br />

a. Dir铆jase nuevamente al ```Query Editor``` y coloque el siguiente comando:
```
DELETE FROM nombre_tabla WHERE id=1;
```
<br />

Ejemplo:
```
DELETE FROM transacciones WHERE id=1;
```
<br />

> NOTA: utilice el ```id``` para identificar que transacci贸n desea eliminar (en este caso el id de la transacci贸n 1). En la imagen puede ver un ejemplo m谩s detallado.
<br />

b. De click en el bot贸n 鈻? (*Execute/Refresh F5*) para aplicar los cambios y actualizar la informaci贸n en la tabla.

<br />

c. Para observar nuevamente la tabla, regrese a ```View/Edit Data``` 鉃? ```All Rows```. De click en el bot贸n 鈻? (*Execute/Refresh F5*) y a continuaci贸n podr谩 visualizar que la informaci贸n eliminada ya no aparece. 

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/EliminarDatos.gif"></p>

<br />

## Importar/Exportar datos con CSV en pgAdmin :page_facing_up:
En el repositorio podr谩 encontrar el archivo ```datos.csv```, el cual contiene las mismas columnas de las tablas creadas previamente en este repositorio, sin encabezados ni IDs.

Para importar datos aseg煤rese de seleccionar la base de datos y tabla en la cual quiere trabajar, en este caso ser谩 en *ibmclouddb*, la tabla con nombre *transacciones*. En la pesta帽a *tools* seleccione la opci贸n ```Import/Export data``` y complete la siguiente informaci贸n:

* Seleccione la opci贸n ```Import```
* ```Filename```: Navegue hasta la ubicaci贸n de su archivo CSV y selecci贸nelo
* ```Format```: csv
* ```Encoding```: El formato de codificaci贸n de caracteres de su archivo, en este caso UTF8
* ```Header```: Si su archivo tiene encabezados active esta opci贸n, en este caso no debe ser activada
* ```Delimiter```: Seleccione el delimitador de su archivo, en este caso la coma ```,```
* En la pesta帽a ```Columns``` seleccione todas las columnas de la tabla en ```Columns to import```, excepto la columna *id*, para esto puede utilizar la tecla espacio repetidas veces para incluirlas todas y luego eliminar *id*

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/ImportarCSV.gif"></p>

Para exportar una tabla ingrese nuevamente a la pesta帽a *tools*, opci贸n ```Import/Export data``` y complete la informaci贸n:

* Seleccione la opci贸n ```Export```
* ```Filename```: Navegue hasta la ubicaci贸n de su archivo CSV y selecci贸nelo, o escriba el nombre para un archivo nuevo
* ```Format```: csv
* ```Encoding```: El formato de codificaci贸n de caracteres, en este caso UTF8
* ```Header```: Si desea exportar el archivo con encabezados active esta opci贸n, en este caso no fue activada
* ```Delimiter```: Seleccione el delimitador para su archivo, en este caso la coma ```,```
* En la pesta帽a ```Columns``` seleccione todas las columnas de la tabla en ```Columns to export```, excepto la columna *id*, para esto puede utilizar la tecla espacio repetidas veces para incluirlas todas y luego eliminar *id*

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/ExportarCSV.gif"></p>

## Referencias :mag:
* <a href="https://cloud.ibm.com/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started"> Get Started PostgreSQL</a>.


<br />


## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />
