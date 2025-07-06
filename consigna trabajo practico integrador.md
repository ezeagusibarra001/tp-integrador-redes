Redes de computadoras 
Proyecto integrador 
Objetivo 
La realización de un proyecto en el cual se integren todos los temas que incumben a la materia. Este trabajo será defendido y explicado individualmente en la instancia correspondiente a la evaluación de fin de curso o en la instancia de integración. 
Presentación del trabajo 
Este trabajo será entregado con un informe del desarrollo del mismo en el cual se detallen las tecnologías utilizadas y se justifiquen las elecciones de diseño seleccionadas. 
Deberá contener los siguientes apartados: 
· Introducción. Marco teórico. 
· Diseño de capa física (cableado estructurado, conectividad, etc.). 
· Diseño capa de enlace (Asignación de VLANs, 802.1q, etc.). 
· Diseño capa de red (despliegue IP, ruteo, NAT etc.). 
· Descripción de servicio DHCP. 
· Descripción de servicios de capa de aplicación implementados. 
· Una tabla que contenga los siguientes datos sobre los equipos configurados con IP estática: FQDN | FUNCIONES | IP/MASCARA | [VLAN] | SEDE | PISO/AREA | [IP PUBLICA NAT] · Una tabla que contenga los siguientes datos sobre los equipos configurados con IP dinámica: 
Pool DHCP | [VLAN] | SEDE | [IP PUBLICA NAT] 
· Conclusiones, implementaciones pendientes, dificultades encontradas, etc. 
El trabajo consta de la entrega del informe y de la emulación de la red planteada en esquema reducido pero que contenga todas las redes y servicios a implementar utilizando el programa de emulación de redes recomendado por los docentes. La confección y entrega del trabajo será grupal. 
La entrega grupal se realizará en el campus virtual mediante un archivo comprimido zip (N° grupo apellidos.zip; ejemplo: 03-pacino-pitt-dicaprio.zip) que contenga el informe en formato pdf + el archivo del emulador pkt. 
Se valorará el cumplimiento de los objetivos, la calidad del informe, la preparación y la buena presentación. 
Se evaluará de forma individual y también grupal, de tal forma que la colaboración y el trabajo en equipo serán importantes en la evaluación final de la presentación. 
Detalle del trabajo a realizar 
Se deberá desarrollar el proyecto de una red de datos para una Petrolera “FAMA SRL” que cuenta con la siguiente condición geográfica y edilicia. 
FAMA SRL 
FAMA SRL posee 3 sedes, la principal situada en la Ciudad Autónoma de Buenos Aires (CABA), otra en Córdoba y la última en Santa Fe. 
A. CABA: El edificio de la Ciudad Autónoma de Buenos Aires posee las siguientes características: es un edificio de 10 pisos, de los cuales FAMA posee y hace uso de los pisos 1º , 2º, 7º y 10º.
En el último de los pisos es donde se aloja el Centro de Datos que posee 10 racks para instalar equipos con capacidad para alojar hasta 200 servidores. En este mismo piso se encuentran las oficinas del Departamento de Sistemas (con 30 puestos de trabajo), la oficina del Directorio (10 puestos de trabajo), Departamento de Prensa (15 puestos de trabajo), Departamento de Ingeniería (5 puestos de trabajo), Departamento de Mantenimiento (15 puestos de trabajo), Departamento de Contabilidad (10 puestos de trabajo). 
En el 7º piso se encuentran, Gerentes (6 puestos de trabajo), Departamento de Marketing (5 puestos de trabajo), Facturación y Liquidaciones (12 puestos de trabajo) y Departamento de RRHH (4 puestos de trabajo). 
En el 2º piso se encuentran, el Departamento de Diseño (10 puestos de trabajo) y el Departamento de Compras (10 puestos de trabajo). 
En el 1º piso se encuentra la Sala de Reuniones (8 puestos de trabajo), el SUM (60 puestos de trabajo) y Atención al Público (20 puestos de Trabajo). 
En esta sede, las redes se encuentran segmentadas en redes virtuales (VLANs) de acuerdo a los siguientes grupos de pertenencia: 
1. Administración: Facturación y Liquidaciones, Departamento de Contabilidad, Atención al Público, Departamento de RRHH y Departamento de Compras 
2. Servicios: Departamento de Prensa, Departamento de Diseño, Departamento de Ingeniería y Departamento de Mantenimiento. 
3. Gerencia: Directorio, Gerentes, Departamento de Marketing, Sala de Reuniones y SUM. 4. Departamento de Sistemas y Centro de Datos: Tienen su VLAN propia. 
Se desea que el vínculo vertical de datos de este edificio se encuentre galvánicamente aislado, de modo de desvincular eléctricamente los mismos y aislar cualquier problema eléctrico que haya en un sector del resto de la red. Este aislamiento se logrará mediante la implementación de enlaces de fibra óptica. 
B. Santa Fe: El edificio de Santa Fe es de propiedad íntegra de FAMA SRL y tiene 2 pisos. 
En el 1º piso se encuentran Producción (20 puestos de trabajo), Logística y Transporte (5 puestos de Trabajo) y Departamento Comercial (3 puestos de trabajo) 
En el 2º piso se encuentran Departamento de Administración (4 puestos de trabajo) y Cuarto de Servidores y Conectividad (alojando 6 servidores). 
En esta sede se utilizará un único segmento de red. 
C. Córdoba: El edificio de Córdoba tiene 4 pisos, de los cuales FAMA SRL posee y hace uso sólo del 2º piso. 
En ese piso encontramos Producción (10 puestos), Departamento Comercial (3 puestos), Departamento de Administración (2 puestos), Logística y Transporte (5 puestos) y Cuarto de Servidores y Conectividad (alojando 4 servidores). 
En esta sede se utilizará un único segmento de red. 
Conectividad 
Todos los edificios deberán ser vinculados entre sí por enlaces Gigabit Ethernet punto-a-punto por fibra óptica entre routers.
La conectividad de FAMA SRL. con Internet se realizará a través de un enlace dedicado punto a punto serial desde el edificio de CABA hasta el router del ISP. Para su configuración IP el proveedor proporciona el segmento de red 205.32.130.0/30.
Además el proveedor ha asignado el segmento público 200.45.110.128/25, con el cual la empresa tendrá que implementar todos los servicios de la red que interactúan con Internet. El proceso de NAT/PAT se efectuará en la sede de CABA. 
Las subredes internas deberán ser obtenidas para la sede de CABA a partir del siguiente bloque 172.1.29.0/23 y para el resto de las sedes incluyendo los enlaces punto a punto entre sedes a partir del bloque 10.68.14.0/24. Deberá respetarse el segmento ya asignado a Santa Fe. 
Servicios y equipamiento 
El nombre de dominio de FAMA SRL será fama.com.ar, administrado por el Departamento de Sistemas en el DNS primario de FAMA (LO MOVIMOS A CAB). 
Además se delegará la administración del subdominio logistica.fama.com.ar al Departamento de Logística y Transporte de Santa Fe que administrará su propio servidor DNS primario y lo tendrá alojado en su propia sala de datos. 
Los servidores DNS primarios y secundarios deberán ser completamente configurados en el emulador (registros SOA, A, NS, varios registros CNAME, etc.).
Todos los dispositivos (PCs, laptops, smartphones, etc.), excepto aquellos equipos que provean servicios o por algún motivo requieran IP estática, obtendrán sus configuraciones de red utilizando el protocolo DHCP. 
FAMA contará con los siguientes servicios. Salvo indicación en contrario, los servidores respectivos serán alojados en la sede CABA: 
I. Dos servidores Web y dos servidores Web con protocolo seguro (HTTPS). · 
El servidor Web principal contendrá como mínimo un logo (imagen), información general sobre FAMA SRL, un enlace al listado de servicios brindados utilizando listas y tablas al estilo del problema 1 de la práctica World Wide Web y un enlace al servidor del Departamento de “Logística y Transporte” de Santa Fe  
El segundo servidor Web estará instalado en la Sede Santa Fe y brindará información sobre el departamento de “Logística y Transporte” y contendrá como mínimo un logo, información general y un enlace a un listado de empresas de transporte. (QUEDA IGUAL)
El primer servidor Web seguro será dedicado al Departamento de “Mantenimiento” y contendrá como mínimo la pantalla de acceso al sistema de Gestión de Mantenimiento. (CABA)
El segundo servidor Web seguro contendrá la Intranet1 del sistema de compras. Este 
servidor Web deberá ser accedido solamente por los clientes de la VLAN Administración de CABA; para esto se deberá configurar adecuadamente el firewall local del servidor. 
Sólo se deberán diseñar las páginas de inicio de los servidores. Se deberán desarrollar páginas HTML acordes con la función de cada uno de los servidores. 
II. Servicio de correo electrónico. 
Todas las direcciones de correo electrónico serán de la forma usuario@fama.com.ar. 
En el emulador se deberá configurar el servidor de correo con al menos 3 usuarios pertenecientes a distintas redes virtuales y sedes con sus respectivos clientes. 
III. Todos los edificios contarán en cada uno de sus pisos con puntos de acceso wireless con los que se ofrecerán servicio a laptops, tablets, smartphones, etc. Su identificación en la red (SSID) será “Wifi-FAMA”. 
IV. Cada piso tendrá al menos una impresora de red accesible y utilizable por todos los usuarios de ese piso. Algunas de ellas wireless y otras conectadas por cable. Todas las oficinas contarán con al menos un teléfono IP conectado a la red y a una PC.
1 Una intranet es una red informática que utiliza la tecnología del protocolo de Internet para compartir información, sistemas operativos o servicios de computación dentro de una organización. Suele ser interna, en vez de pública como internet, por lo que solo los miembros de esa organización tienen acceso a ella. 
Se deberá tener en cuenta la distribución de los distintos servicios en los equipos físicos prestando atención a la distribución de la carga, la seguridad y fiabilidad de la red. 
Ruteo IP 
Todos los equipos deberán utilizar rutas estáticas. 
En caso de querer utilizar protocolos de ruteo dinámico (RIP, OSPF, etc.) a modo de desafío personal, se deberá entregar una segunda versión del trabajo con esta implementación. 
Seguridad y administración de la red 
I. Como regla general de seguridad informática los servidores deberán tener operativos únicamente los servicios necesarios para realizar su función. 
II. Con el fin de analizar el tráfico de la red se desplegarán sniffers que se situarán para examinar el tráfico entre las sedes de Santa Fe y Córdoba con la Ciudad Autónoma de Buenos Aires (CABA). 
III. El acceso a puntos de acceso wireless será asegurado con WPA2-PSK usando AES. 
Se pide que desarrolle el proyecto implementando los servicios requeridos. Desarrolle en capa física según normas de cableado estructurado (indique los diferentes tipos de cableado horizontal, vertical, armarios de distribución y tipo de cableado en cada caso). Para la capa de enlace de datos indique qué tipo de equipamiento será necesario y desarrolle el despliegue de VLANs utilizado para satisfacer la segmentación requerida. Para la capa de red realice los subneteos que satisfagan el requerimiento, indicando el ruteo requerido. Para capa de aplicación implemente los servicios requeridos indicando los servicios de capa de transporte utilizados. Describa los servicios auxiliares necesarios para que la red sea operativa indicando las configuraciones básicas de los mismos. 
En la emulación recree las redes requeridas e implemente todos los servicios utilizados. 
Para ilustrar el acceso a Internet, configure un servidor Web con IP pública simulando estar en Internet (www.google.com.ar con IP 216.58.202.99 /25). Para esto habilite en el router donde se conectan los servidores DNS externos (root, ar, etc.) un puerto para la red de Google (similar al Laboratorio DNS – Delegación de dominios). 
Notas para el emulador: 
a. No se encuentra implementada en el emulador la funcionalidad de configuración de servidores DNS primarios y secundarios. En consecuencia las configuraciones de los secundarios deberán ser replicadas de forma manual en los servidores. 
b. No es necesario configurar los teléfonos IP en el emulador. 
c. Se deberá utilizar la versión del emulador publicada en el campus virtual.
