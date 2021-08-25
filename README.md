# IBM Cloud - PostgreSQL Despliegue ☁🚀📚
*IBM® Cloud Databases for PostgreSQL* es una poderosa base de datos relacional de código abierto, que es altamente personalizable. Es una base de datos empresarial rica en funciones con soporte JSON, que le brinda lo mejor de los mundos SQL y NoSQL. Adicionalmente, puede hacer uso de *pgAdmin* una plataforma de administración de código abierto para PostgreSQL que proporciona diversas herramientas para gestionar los datos y las bases de datos.

La presente guía esta enfocada en crear un despliegue de *IBM® Cloud Databases for PostgreSQL* y sobre la base de datos aprovisionada realizar operaciones de inserción, actualización y eliminación de datos.

<br />

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Crear Base de datos PostgreSQL](#Crear-Base-de-datos-PostgreSQL-floppy_disk)
3. [Conexión con IBM Cloud Shell](#Conexión-con-IBM-Cloud-Shell-electric_plug)
4. [CRUD en la base de datos con IBM Cloud Shell](#CRUD-en-la-base-de-datos-con-IBM-Cloud-Shell-hammer)
5. [Conexión con pgAdmin](#Conexión-con-pgAdmin-electric_plug)
6. [CRUD en la base de datos con pgAdmin](#CRUD-en-la-base-de-datos-con-pgAdmin-hammer)
7. [Referencias](#Referencias-mag)
8. [Autores](#Autores-black_nib)
<br />

## Pre Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>.
* Contar con un grupo de recursos específico para la implementación de los recursos.
* Instalación de <a href="https://www.pgadmin.org/download/"> pgAdmin 4</a>. 
<br />

## Crear Base de datos PostgreSQL :floppy_disk:
Para realizar el ejercicio lo primero que debe hacer es crear una *Base de datos PostgreSQL* en su cuenta de *IBM Cloud*. Para ello, siga los pasos que se indican a continuación:
1. Con <a href="https://cloud.ibm.com/catalog/services/databases-for-postgresql">Databases for PostgreSQL</a>, automaticamente será redirigido a la creación de la base de datos.
2. Una vez le aparezca la ventana para la configuración y creación de la *Base de Datos*, complete lo siguiente:
* ```Ubicación```: seleccione la ubicación en la cual desea implementar la *Base de Datos*.
* ```Plan de precios```: Standard
* ```Nombre```: asigne un nombre exclusivo para la *Base de Datos*.
* ```Grupo de recursos```: seleccione el grupo de recursos en el cual va a trabajar.

Las demás caracteristicas se seleccionan por defecto. 

Cuando ya tenga todos los campos configurados de click en el botón ```Crear```.

<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/CrearDB.gif"></p>
<br />

## Conexión con IBM Cloud Shell :electric_plug:
<br />

## CRUD en la base de datos con IBM Cloud Shell :hammer:
<br />

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

Por último, para obtener la constraseña, dirijase a ```Settings``` > ```Change Database Admin Password``` y siga los pasos a continuación:
* Seleccione la opción  ```Generate Password```
* Una vez sea generada, guardela.
* De clik en ```Change Password```
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/IBM-Cloud-PostgreSQL-Despliegue/blob/main/Im%C3%A1genes/Password.PNG"></p>

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
*  ```Password```: Indique la ```Password``` guardada en el paso anterior.
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
a. Teniendo en cuenta que ya existe la base de datos (*ibmclouddb* - creada al conectar el servidor), se debe crear la tabla en la cual se van a almacenar los datos. Para ello, asegurándose de tener seleccionada la base de datos en la cual va a trabajar, de click en la pestaña ```Tools``` y luego seleccione la opción ```Query Tool```. 

<br />


b. Posteriormente, en el ```Query Editor``` coloque el siguiente comando:
```
CREATE TABLE nombre_tabla (id serial, columna_1 tipo_dato, columna_2 tipo_dato, ... , columna_n tipo_dato, primary key (id));
```

> NOTA: los valores ```id serial``` y ```primary key (id)``` se utilizan para generar el ID de la transacción de forma automática. Reemplace las variables correspondientes a cada columna y asigne el tipo de dato a cada una. En la imagen puede ver un ejemplo con más detalle que incluye difentes variables con sus tipos de datos.
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

> NOTA: recuerde reemplazar las variables de cada columna junto con el respectivo valor. Si trabaja con datos de tipo varchar o tipo date, coloque el valor en comillas sencillas (ejemplo: 'teamcloud'). En la imagen puede ver un ejemplo más detallado.
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

> NOTA: para este caso cambie el valor ```columna_1``` con el nombre de la variable que desea modificar, adicionalmente asigne el valor que desea visualizar ahora en dicha variable. Por otro lado, se utiliza el ```id``` para identificar a que transacción se le desea realizar la modificación (en este caso el id de la transacción 1). En la imagen puede ver un ejemplo más detallado.
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

> NOTA: para este caso cambie el valor ```nombre_tabla``` con el nombre de la tabla en la que desea eliminar datos. Adicionalmente, utilice el ```id``` para identificar que transacción se desea eliminar(en este caso el id de la transacción 1). En la imagen puede ver un ejemplo más detallado.
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
