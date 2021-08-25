# IBM Cloud - PostgreSQL Despliegue ☁🚀📚
*IBM® Cloud Databases for PostgreSQL* es una poderosa base de datos relacional de código abierto, que es altamente personalizable. Es una base de datos empresarial rica en funciones con soporte JSON, que le brinda lo mejor de los mundos SQL y NoSQL. Adicionalmente, puede hacer uso de *pgAdmin* una plataforma de administración de código abierto para PostgreSQL que proporciona diversas herramientas para gestionar los datos y las bases de datos.

La presente guía esta enfocada en crear un despliegue de *IBM® Cloud Databases for PostgreSQL* y sobre la base de datos aprovisionada realizar operaciones de inserción, actualización y eliminación de datos.

<br />

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Crear Base de datos PostgreSQL](#Crear-Base-de-datos-PostgreSQL-floppy_disk)
3. [Generar contraseña en servicio PostgreSQL](#Generar-contraseña-en-servicio-PostgreSQL-closed_lock_with_key)

#### OPCIÓN PRUEBA 1
4. [Conexión con IBM Cloud Shell](#Conexión-con-IBM-Cloud-Shell-electric_plug)
5. [CRUD en la base de datos con IBM Cloud Shell](#CRUD-en-la-base-de-datos-con-IBM-Cloud-Shell-pick)

#### OPCIÓN PRUEBA 2
6. [Conexión con pgAdmin](#Conexión-con-pgAdmin-electric_plug)
7. [CRUD en la base de datos con pgAdmin](#CRUD-en-la-base-de-datos-con-pgAdmin-hammer)
8. [Referencias](#Referencias-mag)
9. [Autores](#Autores-black_nib)
<br />

## Pre Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>.
* Contar con un grupo de recursos específico para la implementación de los recursos.
* Instalación de <a href="https://www.pgadmin.org/download/"> pgAdmin 4</a>. 
<br />

## Crear Base de datos PostgreSQL :floppy_disk:
Para realizar el ejercicio lo primero que debe hacer es crear una *Base de datos PostgreSQL* en su cuenta de *IBM Cloud*. Para ello, siga los pasos que se indican a continuación:
1. Con <a href="https://cloud.ibm.com/databases/databases-for-postgresql/createl">Databases for PostgreSQL</a>, automaticamente será redirigido a la creación de la base de datos.
2. Una vez le aparezca la ventana para la configuración y creación de la *Base de Datos*, complete lo siguiente:
</br>

#### Service Details

* ```Service name```: asigne un nombre exclusivo para la *Base de Datos*. 
* ```Resource group```: seleccione el grupo de recursos en el cual va a trabajar.
* ```Location```: .seleccione la ubicación en la cual desea implementar la *Base de Datos*.
</br>

#### Resource Allocation

1.  ```Templates```: 
Puede elegir entre cuatro perfiles pre configurados Small- Medium - Large - Extra Large.

2.  ```Custom```:

* ```RAM```:  Elija la capacidad de RAM en GB.
* ```Dedicated Cores```: Elija la capacidad de cores dedicados que desea. 
* ```Disk Usage```: Elija la capacidad de CPU en GB. 


Las demás caracteristicas se seleccionan por defecto. 

Cuando ya tenga todos los campos configurados de click en el botón ```Crear```.
<br />
<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/crearDB.gif"></p>
<br />

## Generar contraseña en servicio PostgreSQL :closed_lock_with_key:
Para realizar la conexión con la base de datos deberá generar una constraseña en el servicio. Para ello, de click en la pestaña ```Settings``` ➡ ```Change Database Admin Password``` y siga los pasos a continuación:
1. Seleccione la opción  ```Generate Password```.

2. Una vez sea generada, guardela.

3. De clik en ```Change Password```.
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Password.PNG"></p>
<br />

## OPCIÓN PRUEBA 1

## Conexión con IBM Cloud Shell :electric_plug:
Para realizar la conexión y prueba de la base de datos con el Shell de *IBM* realice lo siguiente:

1. Dentro de su cuenta de *IBM Cloud* acceda al ```IBM Cloud Shell``` dando click en la pestaña <a href="https://cloud.ibm.com/shell"> <img width="25" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Shell_IBM.PNG"></a>, que se ubica en la parte superior derecha del portal. 
<br />

2. Asegúrese de estar en la región en donde tiene desplegada su base de datos. Si debe cambiar la región utilice el comando:
```
ibmcloud target -r <region>
```

> NOTA: Reemplace el parámetro \<region> con su respetiva información. Por ejemplo: ```us-south``` para Dallas y ```us-east``` para Washington.
<br />

3. Asegúrese de tener selccionado el grupo de recursos en donde tiene desplegada su base de datos. Para ello, utilice el comando:
```
ibmcloud target -g <grupo_recursos>
```

> NOTA: Reemplace el parámetro \<grupo_recursos> con su respetiva información. 
<br />
 
4. Luego de establecer la región y el grupo de recursos, coloque el siguiente comando para instalat el plugin ```ibmcloud cdb```:
```
ibmcloud plugin install cloud-databases
```
<br />

5. Cuando le indique si desea actualizar el plugin (en caso de estar instalado) coloque ```y```.
<br />

6. Para conectarse con el deployment de la base de datos en *IBM Cloud Shell* copie el endpoint que sale en la sección ```Overview``` del servicio ➡ ```Endpoints``` ➡ ```Quick start``` ➡ ```2. Connect to your deployment``` y coloquelo en el shell de *IBM*.
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CopiarEndpoint.PNG"></p>
<br />

7. Escriba la contraseña establecida en el paso [Generar contraseña en servicio PostgreSQL](#Generar-contraseña-en-servicio-PostgreSQL-closed_lock_with_key) y presiones enter.
<br />

<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Acceso_IBM_Cloud_Shell.gif"></p>
<br />

## CRUD en la base de datos con IBM Cloud Shell :pick:
Una vez se ha creado y conectado el servicio de base de datos con *IBM Cloud Shell*, se continúa el ejercicio con las operaciones del CRUD (Create, Read, Update & Delete). Para ello, se presentan a continuación los pasos que se deben realizar para llevar a cabo cada una de estas operaciones:
<br />

### 1. Crear Database
<br />

<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CrearDB_IBM_Shell.gif"></p>
<br />

### 2. Crear tabla
<br />

<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CrearTabla_IBM_Shell.gif"></p>
<br />

### 3. Agregar y visualizar datos
<br />

<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Insertar_IBM_Shell.gif"></p>
<br />

### 4. Actualizar y visualizar datos
<br />

<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Actualizar_IBM_Shell.gif"></p>
<br />

### 5. Eliminar datos
<br />

<p align="center"><img width="900" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Eliminar_IBM_Shell.gif"></p>
<br />

## OPCIÓN PRUEBA 2

## Conexión con pgAdmin :electric_plug:
1. Cuando abra *pgAdmin* por primera vez, se le solicita establecer una contraseña primaria, la cual será requerida cada vez que abra la aplicación.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Password_inicio_pgadmin.PNG"></p>
<br />

2. Consulte la información relevante del servicio de *Databases for PostgreSQL* creado en *IBM*, la cual será requerida en el paso siguiente.

* Ingrese a  ```Overview```, desplácese hasta el final de la página ```Endpoints``` > ```PostgreSQL```.
* Identifique el ```Hostname```
* Identifique el ```Port```
* Identifique el ```SSL Mode```
* Descargue el ```TLS certificate```
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Credenciales.PNG"></p>
<br />

3. En *pgAdmin*, ```Dashboard``` seleccione ```Add New Server```. A continuación se desplegará una ventana en donde debe llenar los siguientes campos:

En la pestaña ```General```:

* ```Name```: asigne un nombre exclusivo para el servicio.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Conexion_pgAdmin_parte1.PNG"></p>

En la pestaña ```Connection```:

* ```Host name/address```: Indique el ```Hostname``` de la información relevante de la base de datos.
* ```Port```: Indique el ```Port``` de la información relevante de la base de datos.
* ```Maintenance database```: postgres
* ```Username```: admin
*  ```Password```: Indique la contraseña stablecida en el paso [Generar contraseña en servicio PostgreSQL](#Generar-contraseña-en-servicio-PostgreSQL-closed_lock_with_key).
Los campos ```Role``` y ```Service``` pueden quedar vacios.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Conexion_pgAdmin_parte2.PNG"></p>

En la pestaña ```SSL```:

* ```SSL Mode```: Inidque el ```SSL Mode``` de la información relevante de la base de datos.
* ```Root Certificate```: Cargue el archivo del certificado descargado en el paso anterior.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Conexion_pgAdmin_parte3.PNG"></p>
<br />

Cuando tenga todas las pestañas configuradas, de click en ```Save``` para que *pgAdmin* se conecte a su implementación.

<br />

## CRUD en la base de datos con pgAdmin :hammer:
Una vez se ha creado y conectado la base de datos con *pgAdmin*, se continúa el ejercicio con las operaciones del CRUD (Create, Read, Update & Delete). Para ello, se presentan a continuación los pasos que se deben realizar para llevar a cabo cada una de estas operaciones:
<br />

### 1. Crear Tabla:
a. Teniendo en cuenta que ya existe la base de datos (*ibmclouddb* - creada al conectar el servidor), se debe crear la tabla en la cual se van a almacenar los datos. Para ello,    asegurándose de tener seleccionada la base de datos en la cual va a trabajar, de click en la pestaña ```Tools``` y luego seleccione la opción ```Query Tool```. 
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

> NOTA: los valores ```id serial``` y ```primary key (id)``` se utilizan para generar el ID de la transacción de forma automática. 
<br />

c. Para crear la tabla, de click en el botón ▶ (*Execute/Refresh F5*).

<br />

d. Para observar la tabla que acaba de crear, de click derecho sobre el servidor conectado y seleccione la opción ```Refresh```. Por último, dentro de la base de datos en las opciones ```Schemas/public/Tables``` de click derecho sobre la tabla creada y seleccione la opción ```View/Edit Data``` ➡ ```All Rows```. Allí puede visualizar la tabla y en la pestaña ```Data Output``` puede observar que aparecen las respectivas columnas con sus tipos de datos.

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CrearTabla.gif"></p>

<br />
 
### 2. Agregar y visualizar datos
El paso siguiente consiste en insertar datos en la tabla que se acaba de crear, para ello realice lo siguiente:

<br />

a. Diríjase nuevamente al ```Query Editor``` y coloque el siguiente comando:
```
INSERT INTO nombre_tabla (columna_1, columna_2, ... , columna_n) VALUES(valor_1, valor_2, ... , valor_n);
```
<br />

Ejemplo:
```
INSERT INTO transacciones (nombre, apellido, ciudad, direccion, cedula, fecha, valor, tipo) VALUES('Diana', 'Espitia', 'Bogotá', 'Cra. 53 No. 100- 25', 1234567890, '03/08/2021', 200000, 'Consignación');
```
<br />

b. De click en el botón ▶ (*Execute/Refresh F5*) para agregar los datos a la tabla.

<br />

c. Para observar los datos en la tabla, regrese nuevamente a ```View/Edit Data``` ➡ ```All Rows```. De click en el botón ▶ (*Execute/Refresh F5*) y a continuación podrá visualizar la información que acaba de registrar. 

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/InsertarDatos.gif"></p>

<br />

### 3. Actualizar datos
Para actualizar los datos ya registrados en la tabla, realice los siguientes pasos:

<br />

a. Diríjase nuevamente al ```Query Editor``` y coloque el siguiente comando:
```
UPDATE nombre_tabla set columna_1=valor_nuevo where id=1;
```
<br />

Ejemplo:
```
UPDATE transacciones set nombre='Andrea' where id=1;
```
<br />

> NOTA: utilice el ```id``` para identificar que transacción desea modificar (en este caso el id de la transacción 1). En la imagen puede ver un ejemplo más detallado.
<br />

b. De click en el botón ▶ (*Execute/Refresh F5*) para aplicar los cambios y actualizar los datos en la tabla.

<br />

c. Para observar los datos en la tabla, regrese nuevamente a ```View/Edit Data``` ➡ ```All Rows``` en la tabla respectiva. De click en el botón ▶ (*Execute/Refresh F5*) y a continuación podrá visualizar la información que acaba de modificar. 

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/ActualizarDatos.gif"></p>

<br />

### 4. Eliminar datos
Para eliminar los datos ya registrados en la tabla, realice lo siguiente:

<br />

a. Diríjase nuevamente al ```Query Editor``` y coloque el siguiente comando:
```
DELETE FROM nombre_tabla WHERE id=1;
```
<br />

Ejemplo:
```
DELETE FROM transacciones WHERE id=1;
```
<br />

> NOTA: utilice el ```id``` para identificar que transacción desea eliminar (en este caso el id de la transacción 1). En la imagen puede ver un ejemplo más detallado.
<br />

b. De click en el botón ▶ (*Execute/Refresh F5*) para aplicar los cambios y actualizar la información en la tabla.

<br />

c. Para observar nuevamente la tabla, regrese a ```View/Edit Data``` ➡ ```All Rows```. De click en el botón ▶ (*Execute/Refresh F5*) y a continuación podrá visualizar que la información eliminada ya no aparece. 

<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/EliminarDatos.gif"></p>

<br />

## Referencias :mag:
* <a href="https://cloud.ibm.com/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started"> Get Started PostgreSQL</a>.


<br />


## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
<br />
