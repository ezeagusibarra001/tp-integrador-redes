
Proyecto Inicial FAMA SRL





Materia: 
Redes de Computadoras 



Docentes: 
César Luis Zaccagnini 
Leonardo Jose Balbiani 
Sergio Daniel Loyola 



Integrantes: 
Ezequiel Ibarra 
Facundo Gozio 
Leandro Correa







Introducción
Objetivo del proyecto
El objetivo principal de este proyecto es diseñar, implementar y simular una red de datos eficiente y segura para la empresa FAMA SRL. Esta empresa posee 3 sedes, la principal ubicada en Buenos Aires (CABA), una en Córdoba y otra en Santa Fe. Este proyecto integra aspectos como la configuración de servicios, la seguridad de la información y la conectividad de los dispositivos. Esta red debe ser capaz de soportar la comunicación interna y externa, garantizar la disponibilidad de los servicios y permitir una gestión eficiente de los recursos. 

 
Contexto de la Empresa
FAMA SRL es una empresa la cual tiene 3 sedes: Ciudad Autónoma de Buenos Aires (sede principal), Córdoba y Santa Fe. En este proyecto nos comenzamos concentrándonos en la sede de Santa Fe, la cual posee un edificio de dos pisos, en donde el primer piso se encuentra Producción, Logística y Transporte y el Departamento Comercial y en el segundo piso se encuentra el Departamento de Administración y el Cuarte de Servicios. Más avanzados con el proyecto continuamos configurando el servidor de CABA que tiene 10 pisos de los cuales nosotros vamos a utilizar, el número 1º, 2º, 7º y 10º. En el piso 10 se ubica el centro de datos que tiene capacidad para alojar 200 servidores, también se encuentra las oficinas del departamento de sistemas, la oficina del directorio el departamento de prensa, departamento de ingeniería, mantenimiento y contabilidad. Luego en el piso 7 se ubican el departamento de marketing, facturación y liquidación y RRHH. En el 2 piso diseño y compras y en el primer piso la sala de reuniones, el SUM y atención al público. Por ultimo hicimos la sede de Córdoba la cual posee 4 pisos y solo nos concentramos en el 2. En este piso encontramos producción, departamento comercial, de administración, logística y transporte, cuarto de servidores y conectividad.

Importancia del Proyecto

La implementación de una red robusta y eficiente es crucial para FAMA SRL, debido a las siguientes razones: 
1. Mejora de la Comunicación: Una red bien diseñada facilita la comunicación interna entre departamentos y la comunicación externa con otras sedes y clientes. 
2. Eficiencia Operativa: La automatización de servicios como DNS, DHCP, y el acceso a aplicaciones web y de correo electrónico mejora la productividad y eficiencia de los empleados. 
3. Seguridad de la Información: La red debe asegurar la protección de los datos a través de protocolos seguros y la correcta configuración de firewalls y políticas de acceso. 
4. Escalabilidad y Flexibilidad: Una infraestructura de red bien planificada permite a la empresa crecer y adaptarse a nuevas tecnologías y demandas sin comprometer la calidad del servicio.
Marco teórico 
Modelo OSI
 
El Modelo de Interconexión de Sistemas Abiertos (OSI) es un marco conceptual que estandariza las funciones de un sistema de telecomunicaciones o de computación sin tener en cuenta su estructura interna y tecnología. El modelo OSI se divide en siete capas: 
1. Capa Física: Se encarga de la transmisión y recepción de datos en forma de bits a través de medios físicos como cables de cobre, fibra óptica y señales inalámbricas. 
2. Capa de Enlace de Datos: Proporciona la transferencia de datos entre dos dispositivos conectados directamente, detectando y corrigiendo errores que puedan ocurrir en la capa física. 
3. Capa de Red: Gestiona el direccionamiento y enrutamiento de datos entre diferentes redes. El protocolo más conocido en esta capa es el IP. 
4. Capa de Transporte: Asegura la transferencia confiable de datos entre sistemas finales. Los principales protocolos en esta capa son TCP y UDP. 
5. Capa de Sesión: Establece, gestiona y finaliza conexiones entre aplicaciones. 
Permite la sincronización y la recuperación de diálogos entre dispositivos. 
6. Capa de Presentación: Traduce datos entre el formato que usa la red y el formato que usan las aplicaciones. Incluye la compresión de datos y la criptografía. 
7. Capa de Aplicación: Proporciona servicios de red a las aplicaciones del usuario. 
Ejemplos incluyen HTTP para la web, SMTP para el correo electrónico y FTP para la transferencia de archivos.

Protocolo de Red

Los protocolos son conjuntos de reglas que dictan cómo se comunican los dispositivos en una red. Este proyecto utiliza varios protocolos esenciales:

DHCP: Asigna dinámicamente direcciones IP a los dispositivos, facilitando la gestión y configuración de la red. 
DNS: Traduce nombres de dominio legibles por humanos a direcciones IP. La sede de Santa Fe gestionará su propio DNS para el dominio y subdominios.
HTTP y HTTPS: Protocolos para la transferencia de datos en la web. HTTPS incluye cifrado para seguridad adicional.
SMTP: Protocolo utilizado para el envío de correos electrónicos. 
WPA2-PSK: Protocolo de seguridad para redes inalámbricas que utiliza cifrado AES para proteger la comunicación.






Servicios de Red

La implementación de servicios de red es fundamental para asegurar la operatividad y accesibilidad de los recursos. Los servicios implementados incluyen: 
● Servicios Web: 
○ Servidor Web Principal: Aloja el sitio corporativo de FAMA SRL. con información general y enlaces a servicios. 
○ Servidor Web de Logística: Dedicado al Departamento de Logística, con contenido específico y acceso a la información sobre la distribución y el transporte de la maquinaria. 
○ Servidores Web Seguros (HTTPS): Proporcionan acceso seguro a la intranet administrativa y al sistema de del Departamento de 
Logística. 
● Servicio de Correo Electrónico: Facilita la comunicación interna y externa a través de direcciones de correo. 
● Red Inalámbrica (Wireless): Puntos de acceso configurados para ofrecer conectividad Wi-Fi segura a dispositivos móviles.

Diseño de Capa Física 
En todos los edificios las vinculaciones entre se hicieron por enlaces Gigabit Ethernet punto a punto de fibra óptica. La conectividad se realizó con un enlace dedicado punto a punto serial desde el edificio de CABA hasta el Router del ISP. Para la realización de todo este trabajo se utilizaron distintos dispositivos físicos tales como Switches, Switches de capa 2, Routers, distintos tipos de servidores, distintos cables de red y también muchas PCs. Para la configuración IP el proveedor proporciona un segmento de red público de 205.32.130.0/30 y el segmento 200.45.110.128/25 para implementar todos los servicios que interactúan con Internet.






Diseño de Capa de Enlace
Las Vlans se encuentran en CABA y son las siguientes:
Vlan 		Departamento 	Rango IP
02		Administración 	completar
03		Gerencia 		completar
04		Servicios		completar
05		Sistema 		completar
El objetivo de poner Vlans en este servidor es el  de separar logísticamente los grupos de trabajo (sin sumar costos de infraestructura), reducir el Broadcast innecesario de la red, mejorar la seguridad separando los departamentos con información importante y facilitar la administración y escalabilidad de la red.

  Diseño de Red







· Introducción. Marco teórico. 
· Diseño de capa física (cableado estructurado, conectividad, etc.). 
· Diseño capa de enlace (Asignación de VLANs, 802.1q, etc.). 
· Diseño capa de red (despliegue IP, ruteo, NAT etc.).

· Descripción de servicio DHCP. 
· Descripción de servicios de capa de aplicación implementados. 
· Una tabla que contenga los siguientes datos sobre los equipos configurados con IP estática: FQDN | FUNCIONES | IP/MASCARA | [VLAN] | SEDE | PISO/AREA | [IP PUBLICA NAT] · Una tabla que contenga los siguientes datos sobre los equipos configurados con IP dinámica: 
Pool DHCP | [VLAN] | SEDE | [IP PUBLICA NAT] 
· Conclusiones, implementaciones pendientes, dificultades encontradas, etc.
