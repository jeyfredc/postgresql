# Jerarquía de Bases de Datos

Toda jerarquía de base de datos se basa en los siguientes elementos:

- **Servidor de base de datos:** Computador que tiene un motor de base de datos instalado y en ejecución.

- **Motor de base de datos:** Software que provee un conjunto de servicios encargados de administrar una base de datos.

- **Base de datos:** Grupo de datos que pertenecen a un mismo contexto.

- **Esquemas de base de datos en PostgreSQL:** Grupo de objetos de base de datos que guarda relación entre sí (tablas, funciones, relaciones, secuencias).

- Tablas de base de datos: Estructura que organiza los datos en filas y columnas formando una matriz.

**PostgreSQL es un motor de base de datos.**

La estructura de la base de datos diseñada para el reto corresponde a los siguientes
elementos:

![/assets/1.png](/assets/1.png)

El esquema public contiene las siguientes tablas:

- Estación

- Pasajero

- Tren

Y las tablas de relaciones entre cada uno de los elementos anteriores son:

- Trayecto

- Viaje

El esquema relacional entre las tablas corresponde al siguiente diagrama:

![/assets/2.png](/assets/2.png)

**Estación**

Contiene la información de las estaciones de nuestro sistema, incluye datos de nombre con tipo de dato texto y dirección con tipo de dato texto, junto con un número de identificación único por estación.

**Tren**

Almacena la información de los trenes de nuestro sistema, cada tren tiene un modelo con tipo de dato texto y una capacidad con tipo de dato numérico que representa la cantidad de personas que puede llevar ese tren, también tiene un ID único por tren.

**Trayecto**

Relaciona los trenes con las estaciones, simula ser las rutas que cada uno de los trenes pueden desarrollar entre las estaciones

**Pasajero**

Es la tabla que contiene la información de las personas que viajan en nuestro sistema de transporte masivo, sus columnas son nombre tipo de dato texto con el nombre completo de la persona, direccion_residencia con tipo de dato texto que indica dónde vive la persona, fecha_nacimiento tipo de dato texto y un ID único tipo de dato numérico para identificar a cada persona.

**Viaje**

Relaciona Trayecto con Pasajero ilustrando la dinámica entre los viajes que realizan las personas, los cuales parten de una estación y se hacen usando un tren.

___

## Modificaciones a una tabla

Continenen acciones:

- CREATE -> Crear

- ALTER -> Modificar

- DROP -> Borrar

### Creacion de la base de datos

- Seleccionar Databases, click derecho , Create, Database

- En el campo Database se deja el nombre de la tabla, si no hay que hacer alguna modificación mas se da click en guardar

![/assets/3.png](/assets/3.png)


### Creación de la tabla

- Cuando aparece el nombre de la tabla creada, en este caso transporte se selecciona y se despliega

- Seleccionar Schemas, por defecto se crea el esquema public, desplegarlo

- Buscar la parte que dice Tables, click derecho Create, Table

- Pestaña General, va el nombre de la tabla que en este caso es pasajero, Owner es el propietario de la tabla y el Schema que va a contener la tabla

![/assets/4.png](/assets/4.png)

- Pestaña Columns va la informacion de las columnas que quiero crear, el tipo de datos que se va a manejar, configuración en el caso que se quiera restringir un numero entero, caracteres u otras cosas, not NUll significa que el campo esta obligado a ponerse, Primary Key, si es un campo de tipo primario que sirve para vincular con otras tablas

![/assets/5.png](/assets/5.png)

- Pestaña Constraints, si ya tengo definidas las relaciones de las tablas puedo indicar la relacion de la columna que va a ser a traves del id porque la seleccionecomo Primary Key y el nombre usualmente es el nombre de la tabla + `_pkey`

![/assets/6.png](/assets/6.png)

Al final siempre va a aparecer la pestaña SQL que indica cuales son las sentencias o comandos que se hacen por ejemplo en la consola para crear la tabla 

![/assets/7.png](/assets/7.png)

Cuando se crea la tabla, esta va a aparecer debajo de Tables, y en este caso se puede hacer la incersion de los datos, podemos dar click derecho sobre la tabla pasajero, dar click en Scripts, y luego dar click en INSERT Script

![/assets/8.png](/assets/8.png)

Luego va a aparecer una pantalla en el Query Editor indicando la sentencia SQL y los datos que podemos insertar en signo de pregunta

![/assets/9.png](/assets/9.png)

como el campo id es autoincremental se puede quitar y solamente insertar lo que seria el nombre, direccion_residencia y fecha_nacimiento, como no se sabe como trae la fecha por defecto SQL entonces se puede hacer una funcion independiente, se selecciona de inicio a fin con el mouse y se ejecuta la function **SELECT current_date;**, esta trae la fecha del dia de hoy pero da un indicio de como debe ir la fecha en el campo fecha_nacimiento

![/assets/10.png](/assets/10.png)

Luego se selecciona la parte de creacion de la tabla y en la parte de Messages cuando se ejecuta el query o sentencia debe salir un mensaje como este 

```
INSERT 0 1

Query returned successfully in 812 msec.
```

![/assets/11.png](/assets/11.png)

Existe una pagina llamada mockaroo, que sirve para generar datos aleatorios automaticos y sirven de prueba puedes visitarla en el siguiente [enlace](https://mockaroo.com/)

## Cruzar tablas: SQL JOIN

![/assets/12.png](/assets/12.png)

___

## Grupo de comandos SQL

![/assets/13.png](/assets/13.png)

## Clausulas 

![/assets/14.png](/assets/14.png)

**Intruccion SQL**

consiste en el uso de:

**Comando + Clausula + Operadores + Funciones**

No es necesario que lleve los 4 elementos, esto dependera de la complejidad de la consulta o lo que se quiere hacer

Primero creamos una base de datos en postgresql

CREATE DATABASE Curso_SQL;

Despues creamos la tabla de clientes

```
CREATE TABLE public.clientes
(
    codigocliente text COLLATE pg_catalog."default" NOT NULL,
    empresa character varying COLLATE pg_catalog."default",
    direccion character varying COLLATE pg_catalog."default",
    poblacion character varying COLLATE pg_catalog."default",
    telefono numeric,
    responsable character varying COLLATE pg_catalog."default",
    historial character varying COLLATE pg_catalog."default",
    CONSTRAINT clientes_pkey PRIMARY KEY (codigocliente)
)
```

Ahora hacemos la insercion de los datos

```
INSERT INTO public.'CLIENTES'(
	'CODIGO_CLIENTE', 'EMPRESA', 'DIRECCION', 'POBLACION', 'TELEFONO', 'RESPONSABLE', 'HISTORIAL')
	VALUES ('CT01','BELTRÁN E HIJOS','LAS FUENTES 78','MADRID',914456435,'ANGEL MARTÍNEZ'),
('CT02','LA MODERNA','LA PALOMA 123','OVIEDO',985323434,'JUAN GARCÍA'),
('CT03','EL ESPAÑOLITO','MOTORES 34','BARCELONA',934565343,'ANA FERNÁNDEZ'),
('CT04','EXPORTASA','VALLECAS 34','MADRID',913452378,'ELVIRA GÓMEZ'),
('CT06','CONFECCIONES AMPARO','LOS MOROS 23','GIJÓN',985754332,'LUÍS ÁLVAREZ'),
('CT07','LA CASA DEL JUGUETE','AMÉRICA 45','MADRID',912649987,'ELÍAS PÉREZ'),
('CT08','JUGUETERÍA SUÁREZ','PARIS 123','BARCELONA',933457866,'JUAN GARCÍA'),
('CT09','ALMACÉN POPULAR','LAS FUENTES 124','BILBAO',942347127,'JOSÉ ÁLVAREZ'),
('CT10','FERETERÍA EL CLAVO','PASEO DE ÁLAMOS 78','MADRID',914354866,'MANUEL MENÉNDEZ'),
('CT11','JUGUETES MARTÍNEZ','VIA LAYETANA 245','BARCELONA',936628554,'FRANCISCO CUEVAS'),
('CT12','FERNÁNDEZ SL','PASEO DEL MAR 45','SANTANDER',942049586,'ELISA COLLADO'),
('CT13','CONFECCIONES ARTÍMEZ','GENERAL PERÓN 45','A CORUÑA',981345239,'ESTEBAN PASCUAL'),
('CT14','DEPORTES GARCÍA','GUZMÁN EL BUENO 45','MADRID',913299475,'ANA JIMÉNEZ'),
('CT15','EXCLUSIVAS FERNÁNDEZ','LLOBREGAT 250','BARCELONA',939558365,'LUISA FERNÁNDEZ'),
('CT16','DEPORTES MORÁN','AUTONOMÍA 45','LUGO',982986944,'JOSÉ MANZANO'),
('CT17','BAZAR FRANCISCO','CARMEN 45','ZAMORA',980495288,'CARLOS BELTRÁN'),
('CT18','JUGUETES LA SONRISA','LA BAÑEZA 67','LEÓN',987945368,'FAUSTINO PÉREZ'),
('CT19','CONFECCIONES GALÁN','FUENCARRAL 78','MADRID',913859234,'JUAN GARCÍA'),
('CT20','LA CURTIDORA','OLIVARES 3','MÁLAGA',953756259,'MARÍA GÓMEZ'),
('CT21','LÍNEA JOVEN','SIERPES 78','SEVILLA',953452567,'ASUNCIÓN SALADO'),
('CT22','BAZAR EL BARAT','DIAGONAL 56','BARCELONA',936692866,'ELISA DAPENA'),
('CT23','EL PALACIO DE LA MODA','ORTEGA Y GASSET 129','MADRID',927785235,'LAURA CARRASCO'),
('CT24','SÁEZ Y CÍA','INFANTA MERCEDS 23','SEVILLA',95486923,'MANUEL GUERRA'),
('CT25','DEPORTES EL MADRILEÑO','CASTILLA 345','ZARAGOZA',976388934,'CARLOS GONZÁLEZ'),
('CT26','FERRETERÍA LA ESCOBA','ORENSE 7','MADRID',918459346,'JOSÉ GARCÍA'),
('CT27','JUGUETES EL BARATO','VÍA AUGUSTA 245','BARCELONA',933486984,'ELVIRA IGLESIAS'),
('CT28','CONFECCIONES HERMINIA','CORRIDA 345','GIJÓN',985597315,'ABEL GONZÁLEZ'),
('CT30','BAZAR EL ARGENTINO','ATOCHA 55','MADRID',912495973,'ADRIÁN ÁLVAREZ'),
('CT31','LA TIENDA ELEGANTE','EL COMENDADOR 67','ZARAGOZA',975694035,'JOSÉ PASCUAL'),
('CT32','DEPORTES NAUTICOS GARCÍA','JUAN FERNÁNDEZ 89','ÁVILA',920268648,'JUAN CONRADO'),
('CT33','CONFECCIONES RUIZ','LLOBREGAT 345','BARCELONA',934587615,'CARLOS SANZ'),
('CT34','BAZAR LA FARAONA','CASTILLA Y LEÓN 34','MADRID',915483627,'ANGEL SANTAMARÍA'),
('CT35','FERRETERÍA EL MARTILLO','CASTELLANOS 205','SALAMANCA',923548965,'JOAQUÍN FERNANDEZ'),
('CT36','JUGUETES EDUCATIVOS SANZ','ORENSE 89','MADRID',916872354,'PEDRO IGLESIAS'),
('CT37','ALMACENES FERNANDEZ','ANTÓN 67','TERUEL',978564025,'MARIA ARDANZA'),
('CT38','CONFECCIONES MÓNICA','MOTORES 67','BARCELONA',935681245,'PEDRO SERRANO'),
('CT39','FERRETERÍA LIMA','VALLECAS 45','MADRID',913532785,'LUIS GARCÍA');
```

Despues creamos la tabla de productos

```
CREATE TABLE public.productos
(
    codigo_articulo text COLLATE pg_catalog."default" NOT NULL,
    seccion character varying COLLATE pg_catalog."default",
    nombrearticulo character varying COLLATE pg_catalog."default",
    precio numeric,
    fecha date,
    importado boolean,
    paisdeorigen character varying COLLATE pg_catalog."default",
    foto text COLLATE pg_catalog."default",
    CONSTRAINT productos_pkey PRIMARY KEY (codigo_articulo)
)
```
Ahora hacemos la insercion de los datos

```
INSERT INTO public.productos(
	codigo_articulo, seccion, nombrearticulo, precio, fecha, importado, paisdeorigen)
	VALUES ('AR01','FERRETERÍA','DESTORNILLADOR',       7.63  , '2000-10-22','0','ESPAÑA'),
('AR02','CONFECCIÓN','TRAJE CABALLERO',      284.58 ,'2002-03-11','1','ITALIA'),
('AR03','JUGUETERÍA','COCHE TELEDIRIGIDO',   159.45 ,'2002-05-26','1','MARRUECOS'),
('AR04','DEPORTES','RAQUETA TENIS',          93.47,  '2000-03-20','1','USA'),
('AR06','DEPORTES','MANCUERNAS',             60.00,  '2000-09-13','1','USA'),
('AR07','CONFECCIÓN','SERRUCHO',             30.20,  '2001-03-23','1','FRANCIA'),
('AR08','JUGUETERÍA','CORREPASILLOS',        103.34, '2000-04-11'  ,'1','JAPÓN'),
('AR09','CONFECCIÓN','PANTALÓN SEÑORA',      174.23, '2000-01-10'  ,'1','MARRUECOS'),
('AR10','JUGUETERÍA','CONSOLA VIDEO',        442.54, '2002-09-24'   ,'1','USA'),
('AR11','CERÁMICA','TUBOS',                  168.43, '2000-02-04'   ,'1','CHINA'),
('AR12','FERRETERÍA','LLAVE INGLESA',        24.40,  '2001-05-23'    ,'1','USA'),
('AR13','CONFECCIÓN','CAMISA CABALLERO',     67.13,  '2002-08-11'    ,'0','ESPAÑA'),
('AR14','JUGUETERÍA','TREN ELÉCTRICO',   15.05,      '2001-07-03' ,'1','JAPÓN'),
('AR15','CERÁMICA','PLATO DECORATIVO',       54.09,  '2000-06-07'    ,'1','CHINA'),
('AR16','FERRETERÍA','ALICATES',             6.74,   '2000-04-17'     ,'1','ITALIA'),
('AR17','JUGUETERÍA','MUÑECA ANDADORA',      105.06, '2001-01-04'   ,'0','ESPAÑA'),
('AR18','DEPORTES','PISTOLA OLÍMPICA',       46.73,  '2001-02-02'    ,'1','SUECIA'),
('AR19','CONFECCIÓN','BLUSA SRA.',           101.06, '2000-03-18'   ,'1','CHINA'),
('AR20','CERÁMICA','JUEGO DE TE',            43.27,  '2001-01-15'    ,'1','CHINA'),
('AR21','CERÁMICA','CENICERO',               19.75,  '2001-07-02'    ,'1','JAPÓN'),
('AR22','FERRETERÍA','MARTILLO',             11.40,  '2001-09-04'    ,'0','ESPAÑA'),
('AR23','CONFECCIÓN','CAZADORA PIEL',        522.69, '2001-07-10'   ,'1','ITALIA'),
('AR24','DEPORTES','BALÓN RUGBY',            111.64, '2000-11-11'   ,'1','USA'),
('AR25','DEPORTES','BALÓN BALONCESTO',       75.27,  '2001-06-25'    ,'1','JAPÓN'),
('AR26','JUGUETERÍA','FUERTE DE SOLDADOS',   143.70, '2000-11-25'   ,'1','JAPÓN'),
('AR27','CONFECCIÓN','ABRIGO CABALLERO',     500.00, '2002-04-05'   ,'1','ITALIA'),
('AR28','DEPORTES','BALÓN FÚTBOL',           43.91,  '2002-07-04'    ,'0','ESPAÑA'),
('AR29','CONFECCIÓN','ABRIGO SRA',           360.07, '2001-05-03'   ,'1','MARRUECOS'),
('AR30','FERRETERÍA','DESTORNILLADOR',       9.06,   '2002-02-20'     ,'1','FRANCIA'),
('AR31','JUGUETERÍA','PISTOLA CON SONIDOS',  57.25,  '2001-04-15'    ,'0','ESPAÑA'),
('AR32','DEPORTES','CRONÓMETRO',             439.18, '2002-01-03'   ,'1','USA'),
('AR33','CERÁMICA','MACETA',                 29.04 , '2000-02-23'   ,'0','ESPAÑA'),
('AR34','OFICINA','PIE DE LÁMPARA',          39.76 , '2001-05-27'   ,'1','TURQUÍA'),
('AR35','FERRETERÍA','LIMA GRANDE',          22.07 , '2002-08-10'   ,'0','ESPAÑA'),
('AR36','FERRETERÍA','JUEGO DE BROCAS',      15.10 , '2002-07-04'   ,'1','TAIWÁN'),
('AR37','CONFECCIÓN','CINTURÓN DE PIEL',     4.33,   '2002-05-12'     ,'0','ESPAÑA'),
('AR38','DEPORTES','CAÑA DE PESCA',          270.00, '2000-02-14'   ,'1','USA'),
('AR39','CERÁMICA','JARRA CHINA',            127.77, '2002-09-02'   ,'1','CHINA'),
('AR40','DEPORTES','BOTA ALPINISMO',         144.00, '2002-05-05'   ,'0','ESPAÑA'),
('AR41','DEPORTES','PALAS DE PING PONG',     21.60 , '2002-02-02'   ,'0','ESPAÑA');
```

### Clausulas y operadores

![/assets/15.png](/assets/15.png)

![/assets/16.png](/assets/16.png)

![/assets/17.png](/assets/17.png)

![/assets/18.png](/assets/18.png)

-- Ver articulos y precio de la sección ceramica

`select nombrearticulo, seccion, precio from productos where seccion='CERÁMICA';`

![/assets/19.png](/assets/19.png)

-- Si quiero consultar por ejemplo la sección de ceramica y deportes, lo logico seria que utilizara una expresión finalizando y añadiendo `AND` pero en SQL no funciona de esta forma, se debe añadir `OR` para que salgan las 2 secciones

`select nombrearticulo, seccion, precio from productos where seccion='CERÁMICA' OR seccion='DEPORTES';`

![/assets/20.png](/assets/20.png)

-- Ver articulos que son de la seccion deportes y provienen de usa

En este caso si podemos utilizar el operador `AND` porque se esta consultando 2 columnas distintas

`select nombrearticulo, seccion, paisdeorigen from productos where seccion='DEPORTES' AND paisdeorigen='USA';`

![/assets/21.png](/assets/21.png)

-- Ver articulos que fueron vendidos entre marzo  y abril

Ahora seleccionamos el campo al cual le queremos proporcionar un rango, en este caso es la fecha , la clausula `between` significa **entre**

`select * from productos where fecha between '2000-03-01' AND '2000-04-30';`

![/assets/22.png](/assets/22.png)

Otra forma de utilizarlo seria con los operadores de comparacion mayor o igual que y menor o igual que

`select * from productos where fecha >= '2000-03-01' AND fecha <='2000-04-30';`

## Ejercicios 

- 1. Realizar una consulta que muestre los campos “Empresa” y “Población” de la tabla “Clientes”.

- 2. Realizar una consulta que muestre los artículos d la sección “Cerámica”.

- 3. Realizar una consulta que muestre los productos de la sección “Deportes” cuyo precio esté entre 100 y 200 €. En la consulta solo se mostrarán los campos “Nombre de artículo” y “Precio”.

- 4. Realizar una consulta que muestre los productos cuyo país no sea España.

- 5. Realizar una consulta que muestre los artículos españoles de la sección “Deportes” cuyo precio sea menor a 350 € 

- 6. Realizar una consulta que muestre los productos cuya fecha esté entre 1/05/2001 y 15/12/2001. En la consulta solo se visualizarán los campos “Nombre de artículo”, “Sección” y “Fecha”.

## Solución

- 1. Realizar una consulta que muestre los campos “Empresa” y “Población” de la tabla “Clientes”.

`select empresa, poblacion from clientes;`

![/assets/23.png](/assets/23.png)

- 2. Realizar una consulta que muestre los artículos d la sección “Cerámica”.

`select * from productos;`

`select nombrearticulo, seccion from productos where seccion='CERÁMICA';`

![/assets/24.png](/assets/24.png)

- 3. Realizar una consulta que muestre los productos de la sección “Deportes” cuyo precio esté entre 100 y 200 €. En la consulta solo se mostrarán los campos “Nombre de artículo” y “Precio”.

`select nombrearticulo, precio from productos where precio between 100 and 200 and seccion='DEPORTES';`

![/assets/25.png](/assets/25.png)

- 4. Realizar una consulta que muestre los productos cuyo país no sea España.

`select * from productos where paisdeorigen <> 'ESPAÑA';`

![/assets/26.png](/assets/26.png)

- 5. Realizar una consulta que muestre los artículos españoles de la sección “Deportes” cuyo precio sea menor a 350 € 

```
select codigo_articulo, nombrearticulo, precio, seccion, paisdeorigen 
from productos 
where paisdeorigen='ESPAÑA' and precio < 350 and seccion='DEPORTES';
```

![/assets/27.png](/assets/27.png)


- 6. Realizar una consulta que muestre los productos cuya fecha esté entre 1/05/2001 y 15/12/2001. En la consulta solo se visualizarán los campos “Nombre de artículo”, “Sección” y “Fecha”.

`select nombrearticulo, seccion, fecha from productos where fecha between '2001-05-01' and '2001-12-15';`

![/assets/28.png](/assets/28.png)

### Clausula Order By

Si realizamos una consulta donde conseguimos mostrar los articulos de la seccion deporte y ceramica obtenemos unos datos que son correctos, pero si se fijan la columna codigoarticulo es la que lleva el orden de menor a mayor

![/assets/29.png](/assets/29.png)

Pero si yo no quiero ordenar esta columna si no otra como la seccion, es decir que aparezca primero ceramica y luego deportes ejecuto la sentencia `order by` con el campo que me interesa ordenar, por defecto se va a ordenar de menor a mayor asi sea un campo numerico, de texto o de fecha,

`select * from productos where seccion='DEPORTES' OR seccion='CERÁMICA' order by seccion;`

![/assets/30.png](/assets/30.png)

Si lo quiero ordenar de mayor a menor agrego una sentencia mas la cual seria `desc`, pero en este caso lo vamos a hacer con el campo `nombrearticulo`

`select * from productos where seccion='DEPORTES' OR seccion='CERÁMICA' order by nombrearticulo desc;`

![/assets/31.png](/assets/31.png)

Si quiero ordenar dos campos al tiempo, se deben incluir estos en la sentencia `order by` pero se debe tener en cuenta que la prioridad del orden se la va a dar al campo que coloquemos en primer lugar 

`select * from productos where seccion='DEPORTES' OR seccion='CERÁMICA' order by paisdeorigen, nombrearticulo;`

![/assets/32.png](/assets/32.png)

tambien hay que tener en cuenta que el orden se va a dar por coincidencias como en este ejemplo donde primero, ordena por seccion, luego por pais de origen y por ultimo por precio, pero este orden se debe a las coincidencia que existen entre si

`select * from productos where seccion='DEPORTES' OR seccion='CERÁMICA' order by seccion, paisdeorigen, precio;`

![/assets/33.png](/assets/33.png)

## Consultas de agrupación o totales

Estas consultas lo que hacen es realizar calculos por grupos, es decir se cogen los registros de una tabla, se agrupan en base a un criterio o campo y una vez que estan agrupados con eso se realiza un calculo por ejemplo para saber cuantos articulos se tiene de una seccion, hallar medias y otro tipos de calculos

### Funciones de agregado

![/assets/34.png](/assets/34.png)

Por ejemplo aqui vamos a ver cuanto suman los articulos de cada sección, para esto se necesitan 2 campos, el primero sera un campo de agrupación y el segundo sera el campo del calculo. 

El campo de agrupación sera por sección y el otro campos sera el de precio donde obtengo la suma total de cada sección entonces si quiero hacer la suma de precio por seccion lo primero que debo hacer es anteponer `SUM(precio)` indicar la tabla de busqueda que en este caso es productos y como quiero agrupar por seccion utilizo la sentencia `group by`

`select seccion, sum(precio) from productos group by seccion;`

![/assets/35.png](/assets/35.png)

Si quisiera ordenar el campo del precio, se podria pensar que al final simplemente habria que agregar esta sentencia `order by precio` pero esta consulta va a arrojar un error y en caso que no lo arroje posiblemente no haga nada, es porque en la consulta del select estamos agregando la columna `sum(precio)` asi que si se hace `order by precio`, no la va a encontrar porque no esta declarada, asi que lo que hay que hacer es llamar el `order by` con referencia a la columna existente `order by sum(precio)`.

`select seccion, sum(precio) from productos group by seccion order by sum(precio);`

![/assets/36.png](/assets/36.png)

Otra forma de hacerlo seria a traves de un alias, para declararlo solo agregamos `as` delante de la columna que queremos llamar de otra forma y asi mismo si se va a ordenar se debe utilizar el alias

`select seccion, sum(precio) as suma_de_articulos from productos group by seccion order by suma_de_articulos;`

![/assets/37.png](/assets/37.png)

Ahora vamos a hallar el promedio de 2 secciones por ejemplo de deportes y confeccion, pero como se ve en la tabla de funciones de agregado aqui ya no se utiliza la sentencia `sum`, esta debera ser sustituida por `avg` y nombrar el campo de otra forma, puede ser `promedio_articulos` otra cosa a tener en cuenta es que cuando se hacen agrupaciones la sentencia `where` es reemplazada por `having`, es decir que actuan de la misma forma pero debe ser sustituida

`select seccion, avg(precio) as promedio_articulos from productos group by seccion having seccion='DEPORTES' or seccion='CONFECCIÓN';`

![/assets/38.png](/assets/38.png)

Si se quiere ordenar se utiliza `order by` haciendo referencia a `promedio_articulos`

```
select seccion, avg(precio) as promedio_articulos from productos 
group by seccion having seccion='DEPORTES' or seccion='CONFECCIÓN'
order by promedio_articulos;
```

![/assets/39.png](/assets/39.png)

Ahora si nos vamos a la tabla de clientes tambien podria hacer un conteo de la poblacion que existente para esto utilizamos la sentencia `count`, entonces podriamos hacer un conteo por la referencia del codigo y para que la tabla no quede nombrada como `count(codigocliente)` le colocamos el alias de `num_clientes`

`select poblacion, count(codigocliente) as num_clientes from clientes group by poblacion;`

![/assets/40.png](/assets/40.png)

Por ultimo utilizamos las funciones agregadas `max` y `min` por ejemplo para saber el articulo mas caro o mas barato de alguna de las secciones

`select seccion, max(precio) as precio_maximo from productos group by seccion having seccion = 'CONFECCIÓN'`

![/assets/41.png](/assets/41.png)

Y si lo quiero utilizar para el minimo, cambio `max` por `min` y nombro de otra forma la columna

`select seccion, min(precio) as precio_minimo from productos group by seccion having seccion = 'CONFECCIÓN'`

![/assets/42.png](/assets/42.png)

### Ejercicios


1. Realizar una consulta sobre la tabla “Clientes”  que muestre los campos “Dirección”, “Teléfono” y “Población”. Este último debe aparecer en la consulta con el nombre de “Residencia”. Los registros aparecerán ordenados descendentemente por el campo “Población”.

2. Realizar una consulta que muestre que poblaciones hay en la tabla “Clientes”.

3. Realizar una consulta de agrupación que muestre la media del precio de los artículos de todas las secciones. Mostrar en laconsulta los campos sección y suma por sección.

4. Realizar una consulta de agrupación que muestre la media del precio de todas las secciones menos de juguetería. En la consultadeberán aparecer los campos “Sección” y “Media por sección”.

5. Realizar Una consulta que muestre cuantos artículos hay de la sección “Deportes”.

### Solucion

1. Realizar una consulta sobre la tabla “Clientes”  que muestre los campos “Dirección”, “Teléfono” y “Población”. Este último debe aparecer en la consulta con el nombre de “Residencia”. Los registros aparecerán ordenados descendentemente por el campo “Población”.

`select direccion, telefono, poblacion as residencia from clientes order by residencia desc;`

![/assets/43.png](/assets/43.png)

2. Realizar una consulta que muestre que poblaciones hay en la tabla “Clientes”.

`select poblacion as poblaciones from clientes group by poblaciones order by poblaciones;`

![/assets/44.png](/assets/44.png)

3. Realizar una consulta de agrupación que muestre la suma del precio de los artículos de todas las secciones. Mostrar en laconsulta los campos sección y suma por sección.

`select seccion, sum(precio) as total_seccion from productos group by seccion;`

![/assets/45.png](/assets/45.png)

4. Realizar una consulta de agrupación que muestre la media del precio de todas las secciones menos de juguetería. En la consultadeberán aparecer los campos “Sección” y “Media por sección”.

`select seccion, avg(precio) as media_por_seccion from productos  group by seccion having seccion <> 'JUGUETERÍA';`

![/assets/46.png](/assets/46.png)

5. Realizar Una consulta que muestre cuantos artículos hay de la sección “Deportes”.

`select seccion, count(codigo_articulo) as num_articulos from productos group by seccion having seccion = 'DEPORTES';`

![/assets/47.png](/assets/47.png)

## Consultas de calculo

Las consultas de calculo se realizan sobre registros individuales y no sobre grupos como se veia en el capitulo anterior

![/assets/48.png](/assets/48.png)

- Now(): Devuelve hora y dia actuales en el momento de hacer la consulta

- Datediff(): Devuelve la diferencia que hay entre dos fechas 

- Date_format(): Permite formatear los resultados por ejemplo para quitar decimales

- Concat(): Permite concatenar y se suele utilizar con cadenas de texto

Ahora vamos a añadir un campo que no existe, este sera el campo del iva de cada producto que correspondera al 19%, para esto vamos a obtener las columnas nombrearticulo, seccion, preccio, precio_con_iva de la tabla productos y ejecutamos un calculo para hallarlo que sera `precio * 1.19`

`select nombrearticulo, seccion, precio, precio * 1.19 as precio_con_iva from productos;`

![/assets/49.png](/assets/49.png)

Pero como vemos en la parte de `precio_con_iva` hay muchos decimales y solo podriamos querer 1 o 2 decimales de mas, si esto se quiere quitar se puede utilizar la función **round** la cual el primer parametro es la expresión que en este caso estamos utilizando `precio * 1.19` y el segundo parametro que recibe es el numero de decimales que queremos obtener supongamos que seran 2. La función quedaria asi `round(precio*1.19, 2)`

`select nombrearticulo, seccion, precio, round(precio * 1.19,2) as precio_con_iva from productos;`

![/assets/50.png](/assets/50.png)

Ahora vamos a trabajar con algunas de las funciones de calculo incluidas al principio del capitulo, como lo son `Now()` y `Datediff()`, como estamos usando postgress esta funcion se llama `date_part`, por ejemplo queremos hallar la diferencia de dias entre el dia de hoy y el primer dia que ingreso un articulo, entonces traemos los campos nombrearticulo, seccion, precio, fecha y a continuacion el dia de hoy de la tabla productos

`select seccion, precio, fecha, now() as dia_de_hoy from productos;`

![/assets/51.png](/assets/51.png)

Ahora que tenemos la fecha inicial y la de hoy hacemos el calculo para hallar la diferencia, entonces utilizamos la funcion `date_part()`, esta funcion recibe 3 parametros que seria lo que queremos hallar `'day'`, la fecha de hoy menos la fecha anterior, pero aqui no se puede establecer como un alias por lo que la funcion `date_part()` recibiria a la funcion now() y el campo fecha `date_part('day', now() - fecha)`

`select seccion, precio, fecha, now() as dia_de_hoy, date_part('day', now() - fecha) as diferencia from productos;`

![/assets/52.png](/assets/52.png)

Si queremos formatear el campo del `dia_de_hoy` para que no se incluya por ejemplo la hora y la latitud, podemos usar la funcion `format()` si utilizamos `mysql`, en postgres se utiliza la funcion `to_char`, esta recibe como primer argumento a la funcion `now()` y como segundo argumento lo que queremos establecer que seria año, mes y dia `YYYY-MON-DD`. `to_char(now(), 'YYYY-MON-DD')`

`select seccion, precio, fecha, to_char(now(), 'YYYY-MON-DD') as dia_de_hoy, date_part('day', now() - fecha) as diferencia from productos;`

![/assets/53.png](/assets/53.png)

### Ejercicios

1. Realizar una consulta que visualice los campos NOMBRE ARTÍCULO, SECCIÓN, PRECIO de la tabla PRODUCTOS y un campo nuevo que nombramos con el texto “DESCUENTO_7”. Debe mostrar el resultado de aplicar sobre el campo PRECIO un descuento de un 7 %. El formato del nuevo campo para debe aparecer con 2 lugares decimales.

2. Realizar una consulta visualizando los campos FECHA, SECCIÓN, NOMBRE ARTÍCULO y PRECIO de la tabla PRODUCTOS y un campo nuevo que nombramos con el texto “DTO2 €_EN_CERÁMICA”. Debe mostrar el resultado de aplicar sobre el campo PRECIO la resta de 2 € sólo a los artículos de la sección CERÁMICA. El formato del nuevo campo debe aparecer con 2 lugares decimales. Ordenar el resultado de la consulta por el campo FECHA descendente.

3. Realizar una consulta visualizando los campos NOMBRE ARTÍCULO, SECCIÓN, PRECIO de la tabla PRODUCTOS y un campo nuevo que nombramos con el texto “PRECIO_AUMENTADO_EN_2”. Debe mostrar el PRECIO con un incremento de un 2% del PRECIO. Sólo debemos tener en cuenta los registros de la sección FERRETERÍA. El nuevo campo debe aparecer en Euros y con 2 lugares decimales.

### Solucion

1. Realizar una consulta que visualice los campos NOMBRE ARTÍCULO, SECCIÓN, PRECIO de la tabla PRODUCTOS y un campo nuevo que nombramos con el texto “DESCUENTO_7”. Debe mostrar el resultado de aplicar sobre el campo PRECIO un descuento de un 7 %. El formato del nuevo campo para debe aparecer con 2 lugares decimales.

`select nombrearticulo, seccion, precio, round(precio-(precio*0.07), 2) as descuento_7 from productos;`

![/assets/54.png](/assets/54.png)

2. Realizar una consulta visualizando los campos FECHA, SECCIÓN, NOMBRE ARTÍCULO y PRECIO de la tabla PRODUCTOS y un campo nuevo que nombramos con el texto “DTO2 €_EN_CERÁMICA”. Debe mostrar el resultado de aplicar sobre el campo PRECIO la resta de 2 € sólo a los artículos de la sección CERÁMICA. El formato del nuevo campo debe aparecer con 2 lugares decimales. Ordenar el resultado de la consulta por el campo FECHA descendente.

```
select fecha, seccion, nombrearticulo, precio, round(precio-2, 2) as dto2_€_en_ceramica 
from productos where seccion='CERÁMICA' order by fecha desc
```

![/assets/55.png](/assets/55.png)

3. Realizar una consulta visualizando los campos NOMBRE ARTÍCULO, SECCIÓN, PRECIO de la tabla PRODUCTOS y un campo nuevo que nombramos con el texto “PRECIO_AUMENTADO_EN_2”. Debe mostrar el PRECIO con un incremento de un 2% del PRECIO. Sólo debemos tener en cuenta los registros de la sección FERRETERÍA. El nuevo campo debe aparecer en Euros y con 2 lugares decimales.

```
select nombrearticulo, seccion, precio, round(precio * 1.02, 2) as precio_aumentado_en_2 
from productos where seccion='FERRETERÍA';
```

![/assets/56.png](/assets/56.png)

## Consultas multitabla I

![/assets/57.png](/assets/57.png)

- **Union** permite unir en una unica consulta varias tablas que podamos tener almacenadas en nuestra base de datos 

![/assets/58.png](/assets/58.png)

Para que el operador `union` se pueda ejecutar debe cumplir con unos requisitos:

1. Las tablas deben tener el mismo numero de campos 

2. Los tipos de datos de ambas tablas deben ser compatibles 

3. El nombre de la columna puede ser igual o diferente 

4. Cuando se haga la union, el nombre de las columnas pasara a ser igual al de la tabla 1

![/assets/59.png](/assets/59.png)

Para practicar con la sentencia `union` debemos crear una tabla similar a la de productos, aqui queda la sentencia para crear la nueva tabla

```
CREATE TABLE public.productosnuevos
(
    codigoarticulo text COLLATE pg_catalog."default" NOT NULL,
    seccion character varying COLLATE pg_catalog."default",
    nombrearticulo character varying COLLATE pg_catalog."default",
    precio numeric,
    fecha date,
    importado boolean,
    paisdeorigen character varying COLLATE pg_catalog."default",
    foto text COLLATE pg_catalog."default",
    CONSTRAINT productosnuevos_pkey PRIMARY KEY (codigoarticulo)
)
```

Ahora se insertan los datos

```
INSERT INTO public.productosnuevos(
    codigoarticulo, seccion, nombrearticulo, precio, fecha, importado, paisdeorigen
) VALUES('AR50','ALTA COSTURA','TRAJE CABALLERO',    1.284 ,'2002-03-11', '1','ITALIA'),
('AR51','DEPORTES DE RIESGO','RAQUETA TENIS',1.093 ,'2000-03-20', '1','USA'),
('AR52','DEPORTES DE RIESGO','MANCUERNAS',   1.060 ,'2000-09-13', '1','USA'),
('AR53','ALTA COSTURA','SERRUCHO',           1.030 ,'2001-03-23', '1','FRANCIA'),
('AR54','ALTA COSTURA','PANTALÓN SEÑORA',    1.174 ,'2000-01-10', '1','MARRUECOS'),
('AR55','ALTA COSTURA','CAMISA CABALLERO',   1.067 ,'2002-08-11', '0','ESPAÑA'),
('AR56','DEPORTES DE RIESGO','PISTOLA OLÍMPICA',1.046, '2001-02-02', '1','SUECIA'),
('AR57','ALTA COSTURA','BLUSA SRA.',         1.101, '2000-03-18', '1','CHINA'),
('AR58','ALTA COSTURA','CAZADORA PIEL',      1.522, '2001-07-10', '1','ITALIA'),
('AR59','DEPORTES DE RIESGO','BALÓN RUGBY',  1.111, '2000-11-11', '1','USA'),
('AR60','DEPORTES DE RIESGO','BALÓN BALONCESTO',1.075,'2001-06-25', '1','JAPÓN'),
('AR61','ALTA COSTURA','ABRIGO CABALLERO',   1.500, '2002-04-05', '1','ITALIA'),
('AR62','DEPORTES DE RIESGO','BALÓN FÚTBOL', 1.043, '2002-07-04', '0','ESPAÑA'),
('AR63','ALTA COSTURA','ABRIGO SRA',         1.360, '2001-05-03', '1','MARRUECOS'),
('AR64','DEPORTES DE RIESGO','CRONÓMETRO',   1.439, '2002-01-03', '1','USA'),
('AR65','ALTA COSTURA','CINTURÓN DE PIEL',   1.004, '2002-05-12', '0','ESPAÑA'),
('AR66','DEPORTES DE RIESGO','CAÑA DE PESCA',1.270, '2000-02-14', '1','USA'),
('AR67','DEPORTES DE RIESGO','BOTA ALPINISMO',1.144,'2002-05-05', '0','ESPAÑA'),
('AR68','DEPORTES DE RIESGO','PALAS DE PING PONG', 1.021, '2002-02-02' ,'0','ESPAÑA');
```

para ver el ejemplo con la sentencia `union` a continuacion vamos a unir la seccion de `deportes` y `deportes de riesgo`

```
select * from productos where seccion='DEPORTES' 
union 
select * from productosnuevos where seccion='DEPORTES DE RIESGO';
```

Como podemos observar los valores de las columnas toman al de la tabla uno pero se unen la seccion de `deportes` que pertenece a la tabla uno y la seccion de `deportes de riesgo` que pertenece a la tabla dos

![/assets/60.png](/assets/60.png)

Ahora consultamos articulos en la primer tabla cuyo precio es mayor a 500 y en la segunda tabla consultamos la seccion de alta costura, cabe resaltar que la segunda tabla va a tomar la condicion de la tabla uno y van a salir los articulos de la seccion alta costura mayores a 500

```
select * from productos where precio>500 
union
select * from productosnuevos where seccion ='ALTA COSTURA';
```

![/assets/61.png](/assets/61.png)

Ahora si utilizamos la sentencia `union` y encontramos en ambas tablas 2 registros exactamente iguales solo va a mostrar 1 campo la tabla pero si utilizamos la sentencia `union all` va a mostrar los registros de las 2 tablas para ver el ejemplo vamos a insertar un campo de la tabla en la tabla 2 

```
INSERT INTO public.productosnuevos(
    codigoarticulo, seccion, nombrearticulo, precio, fecha, importado, paisdeorigen
) VALUES('AR12','FERRETERÍA','LLAVE INGLESA', 24.40, '2001-05-23','1','USA');
```

y ahora vamos a realizar la consulta especificamente sobre la seccion `FERRETERIA` utilizando `union`

como podemos ver con esta sentencia pareciera que no hubiera diferencia

```
select * from productos where seccion='FERRETERÍA'
union
select * from productosnuevos where seccion='FERRETERÍA';
```

![/assets/62.png](/assets/62.png)

pero si ahora utilizamos union all va a traer los 2 registros que son iguales 

```
select * from productos where seccion='FERRETERÍA'
union all
select * from productosnuevos where seccion='FERRETERÍA' order by codigo_articulo;
```

![/assets/63.png](/assets/63.png)

## Consultas multitabla II Iner Join 

**INNER JOIN**

Lo que va a hacer es devolver la información que existe en comun en las dos tablas, una de las condiciones es que se deben relacionar entre si 

![/assets/64.png](/assets/64.png)


**LEFT JOIN**

Devuelve los elementos de la tabla 1 y trae elementos de la tabla 1 que no esten relacionadas con la tabla 2 y ademas trae lo que exista en comun con la tabla 2 

![/assets/65.png](/assets/65.png)

**RIGHT JOIN**

Devuelve los elementos de la tabla 2 y tra elemenros de la tabla 2 que no esten relacionadas con la tabla 1 y ademas trae lo que exista en comun con la tabla 1

![/assets/66.png](/assets/66.png)

Ahora vamos a crear una nueva tabla que va a tener relacion con la tabla de clientes

```
CREATE TABLE public.pedidos
(
    numerodepedido bigint NOT NULL,
    codigocliente text COLLATE pg_catalog."default",
    fechadepedido date,
    formadepago character varying COLLATE pg_catalog."default",
    descuento numeric,
    enviado boolean,
    CONSTRAINT pedido_pkey PRIMARY KEY (numerodepedido)
)
```

Despues de ello hacemos la insercion de los datos

INSER INTO public.pedidos (
    numerodepedido, codigocliente, fechadepedido, formadepago, descuento, enviado
) VALUES (1,'CT01','2000-03-11','CONTADO',0.02,'1'),
(3,'CT23','2000-03-18','APLAZADO',0.06,'0'),
(5,'CT25','2000-03-31','CONTADO',0.09,'0'),
(7,'CT12','2000-04-12','CONTADO',0.07,'0'),
(8,'CT01','2000-04-15','TARJETA',0.02,'1'),
(9,'CT21','2000-04-21','CONTADO',0.04,'0'),
(13,'CT13','2000-04-30','APLAZADO',0.03,'0'),
(22,'CT07','2000-05-31','TARJETA',0.05,'1'),
(25,'CT18','2000-06-02','CONTADO',0.06,'0'),
(27,'CT34','2000-06-06','CONTADO',0.04,'0'),
(31,'CT30','2000-06-08','TARJETA',0.05,'1'),
(28,'CT28','2000-06-08','APLAZADO',0.08,'0'),
(47,'CT34','2000-07-31','APLAZADO',0.08,'0'),
(30,'CT02','2000-08-15','CONTADO',0.06,'1'),
(63,'CT28','2000-09-10','CONTADO',0.09,'0'),
(77,'CT01','2000-10-28','CONTADO',0.05,'0'),
(79,'CT34','2000-12-12','CONTADO',0.05,'0'),
(105,'CT30','2001-01-01','APLAZADO',0.09, '0'),
(102,'CT06','2001-01-12','CONTADO',0.07, '1'),
(103,'CT02','2001-01-24','CONTADO',0.04, '0'),
(29,'CT30','2001-04-02','TARJETA',0.06, '0'),
(11,'CT04','2001-05-01','CONTADO',0.08, '1'),
(16,'CT25','2001-05-11','CONTADO',0.12, '0'),
(12,'CT06','2001-05-19','CONTADO',0.09, '1'),
(21,'CT16','2001-05-28','CONTADO',0.03, '0'),
(26,'CT09','2001-06-04','APLAZADO',0.07, '1'),
(32,'CT14','2001-06-20','APLAZADO',0.06, '0'),
(35,'CT26','2001-06-30','CONTADO',0.06, '0'),
(37,'CT24','2001-07-02','TARJETA',0.03, '1'),
(39,'CT20','2001-07-08','TARJETA',0.06, '1'),
(43,'CT09','2001-07-18','CONTADO',0.07, '0'),
(73,'CT01','2001-08-02','CONTADO',0.07, '0'),
(86,'CT09','2001-12-24','APLAZADO',0.03, '0'),
(98,'CT01','2001-12-27','CONTADO',0.08, '1'),
(5050,'CT30','2002-03-27','TARJETA',0, '1'),
(19,'CT10','2002-05-22','CONTADO',0.07, '1'),
(34,'CT26','2002-06-23','TARJETA',0.05, '0'),
(40,'CT04','2002-07-12','CONTADO',0.12, '0'),
(42,'CT34','2002-07-15','APLAZADO',0.07, '1'),
(44,'CT34','2002-07-20','APLAZADO',0.04, '0'),
(45,'CT30','2002-07-22','TARJETA',0.07, '0'),
(46,'CT31','2002-07-25','CONTADO',0.06, '0'),
('5005','CT30','2002-08-10','TARJETA',0, '1'),
(72,'CT01','2002-08-18','CONTADO',0.05, '1'),
(48,'CT18','2002-08-30','CONTADO',0.03, '0'),
(49,'CT28','2002-09-02','CONTADO',0.03, '0'),
(50,'CT09','2002-09-05','APLAZADO',0.08, '0'),
(51,'CT09','2002-09-05','CONTADO',0.05, '1'),
(74,'CT01','2002-09-17','APLAZADO',0.08, '0'),
(75,'CT01','2002-09-30','TARJETA',0.12, '0'),
(76,'CT01','2002-10-19','CONTADO',0.04, '1'),
(85,'CT04','2002-12-23','TARJETA',0.04, '0');

Ahora vamos a añadir una llave foranea, la cual sera la que va a indicar la relacion entre la tabla de clientes y la tabla de pedidos, la relacion sera a traves del campo `codigocliente`

```
ALTER TABLE public.pedidos
    ADD CONSTRAINT pedidos_codigoclientes_fgkey FOREIGN KEY (codigocliente)
    REFERENCES public.clientes (codigocliente)
    ON UPDATE CASCADE
    ON DELETE CASCADE
    NOT VALID;
```
Si no se agrega esta llave foranea no se puede establecer la relacion entre una tabla y otra y por tanto no se podra realizar un `inner join`

Ahora vamos a hacer una consulta donde se traiga a los clientes de Madrid que han hecho pedidos

```
select clientes.codigocliente, poblacion, direccion, numerodepedido, pedidos.codigocliente
from clientes
inner join pedidos
on clientes.codigocliente = pedidos.codigocliente
where poblacion = 'MADRID';
```

Antes de mostrar el resultado primero se va a especificar que es lo que se esta consultando.

En primer lugar cuando se añade `clientes.codigocliente` se esta haciendo referencia al campo de la tabla 1 ya que `codigocliente` existe en ambas tablas,  luego esta `poblacion` y `direccion` que tambien son de la tabla 1, pero `numerodepedido` y `pedidos.codigocliente` son de la tabla 2 se hace un `from` indicando que se viene de la tabla 1 y e `inner join` para indicar con que tabla se quiere hacer la union que en este caso es la tabla 2 luego viene la sentencia `on`, esta, esta indicando que la tabla 1 tiene un campo en relacion con la tabla 2 `clientes.codigo cliente = pedidos.codigocliente` y luego viene la especificidad de la consulta, `where poblacion = 'MADRID'`

como resultado trae todos los clientes que hicieron pedido y que son de madrid

![/assets/67.png](/assets/67.png)

Y si a continuación hago un `LEFT JOIN` va a traer los datos de los clientes que hicieron y no hicieron pedidos, un indicio para saber que la afirmacion es verdadera es porque todos los campos los va a traer en nulo, de esta forma sabemos que clientes no hicieron pedidos

```
select clientes.codigocliente, poblacion, direccion, numerodepedido, pedidos.codigocliente
from clientes
left join pedidos
on clientes.codigocliente = pedidos.codigocliente
where poblacion = 'MADRID';
```

![/assets/68.png](/assets/68.png)
