# Trabajo práctico integrador - Redes de Computadoras - Primer semestre 2025
### Grupo 9 - Integrantes:
- Leandro Correa
- Ezequiel Ibarra
- Facundo Gozio


# Introducción y Marco Teórico

La implementación del trabajo requirió aplicar conceptos de la totalidad de la materia. Desde DNS a NAT, prácticamente todas las herramientas que aprendimos fueron utilizadas. Tanto la inspección de paquetes con el modo de simulación en Packet Tracer, como los distintos comandos por consola, ya sea `ping`, `tracert` o incluso `telnet` fueron algunos de tantos recursos utilizados. 
A su vez, ciertas decisiones al inicio tuvieron que ser revisadas, como por ejemplo, alocar la totalidad del rango NAT al pool dinámico. Esto hizo el trabajo algo complejo, ya que a cada modificación, debía seguir un testeo de conectividad en todas las sedes.
Trataremos de cubrir de manera sencilla todas las configuraciones, sin detallar los distintos problemas, sino tratando de enfocarnos en el estado final de la solución.

# Diseño de capa física

## Conectividad entre Sedes
- Enlaces entre sedes: Gigabit Ethernet punto-a-punto por fibra óptica entre routers (CABA, Córdoba y Santa Fe)
- Enlaces de transporte configurados:
  - CABA-CÓRDOBA: FastEthernet 4/0 en ambos routers
  - CABA-SANTA FE: FastEthernet 5/0 en CABA, FastEthernet 4/0 en Santa Fe
  - CÓRDOBA-SANTA FE: FastEthernet 5/0 en ambos routers

## Conectividad con Internet
Enlace con ISP: Conexión serial punto a punto desde CABA en el segmento dado `205.32.130.0/30`

## Cableado Estructurado
- Cableado Vertical: Fibra óptica entre pisos en CABA para aislación galvánica
- Cableado Horizontal: UTP para conexiones dentro de cada piso

# Diseño capa de enlace

## VLANs en CABA
- **VLAN 2** - Administración: Encapsulación 802.1Q en subinterfaz Fa0/0.2
  - Facturación y Liquidaciones
  - Departamento de Contabilidad
  - Atención al Público
  - Departamento de RRHH
  - Departamento de Compras

- **VLAN 3** - Servicios: Encapsulación 802.1Q en subinterfaz Fa0/0.3
  - Departamento de Prensa
  - Departamento de Diseño
  - Departamento de Ingeniería
  - Departamento de Mantenimiento

- **VLAN 4** - Gerencia: Encapsulación 802.1Q en subinterfaz Fa0/0.4
  - Directorio
  - Gerentes
  - Departamento de Marketing
  - Sala de Reuniones
  - SUM

- **VLAN 5** - Sistemas: Encapsulación 802.1Q en subinterfaz Fa0/0.5
  - Departamento de Sistemas
  - Centro de Datos

## Monitoreo de Red
Implementación de SPAN (Switch Port Analyzer):
- Interfaces monitoreadas: Fa0/1, 1/1, 2/1, 3/1, 4/1, 5/1, Eth7/1, 8/1, 9/1
- Puerto destino: Gig7/1 (sniffer)

**Nota**: tuvimos que aplicar esto para tratar de no modificar, al final del trabajo, la entrada del router CABA al switch principal de la sede. En lugar de esto, agrgamos un puert Gigabit al switch y redirigimos el tráfico hacia el Sniffer.

## Distribución de Switches
- Piso 10: Dos switches (uno dedicado al centro de datos)
- Demás pisos: Un switch por piso con soporte para todas las VLANs

Todas las interfaces entre pisos van con trunking. 

# Diseño capa de red

## Esquema de direccionamiento:

| Segmento | Sede | Rango | Máscara | Desde | Hasta | Hosts útiles |
|----------|------|-------|---------|-------|-------|--------------|
| Interno | SANTA FE | 10.68.14.64/26 | 255.255.255.192 | 10.68.14.64 | 10.68.14.127 | 62 |
| Interno | CÓRDOBA | 10.68.14.128/27 | 255.255.255.224 | 10.68.14.128 | 10.68.14.159 | 30 |
| WAN | ISP | 205.32.130.0/30 | 255.255.255.252 | 205.32.130.0 | 205.32.130.3 | 2 |
| Interno | CABA | 172.1.29.0/23 | 255.255.254.0 | 172.1.29.0 | 172.1.30.255 | 510 |
| Público | NAT | 200.45.110.128/25 | 255.255.255.128 | 200.45.110.128 | 200.45.110.255 | 126 |

## Enlaces de transporte:

| Enlace | Rango | Máscara | IP Router 1 | IP Router 2 |
|--------|-------|---------|-------------|-------------|
| CABA-CÓRDOBA | 10.68.14.0/30 | 255.255.255.252 | 10.68.14.1 | 10.68.14.2 |
| CABA-SANTA FE | 10.68.14.4/30 | 255.255.255.252 | 10.68.14.5 | 10.68.14.6 |
| CÓRDOBA-SANTA FE | 10.68.14.8/30 | 255.255.255.252 | 10.68.14.9 | 10.68.14.10 |

## Configuración NAT
- Pool dinámico: POOL-NAT-FAMA (200.45.110.193 - 200.45.110.254)
- NAT estático: Configurado para servidores públicos

ALERTA, FALTA: Tablas de ruteo estático completas y políticas de firewall.

# Descripción de servicio DHCP

## Pools DHCP en CABA:

| Pool | Red | Gateway | DNS Server |
|------|-----|---------|------------|
| pool-caba-admin | 172.1.28.0/25 | 172.1.28.1 | 10.68.14.68 |
| pool-caba-svc | 172.1.28.128/25 | 172.1.28.129 | 10.68.14.68 |
| pool-caba-gcia | 172.1.29.0/25 | 172.1.29.1 | 10.68.14.68 |
| pool-caba-sist | 172.1.29.128/25 | 172.1.29.129 | 10.68.14.68 |

La configuración de DHCP para Córdoba fue agregada al router, mientras que el de Santa Fe no fue modificado (se usó el de la entrega anterior).

# Descripción de servicios de capa de aplicación

## Servidores y Servicios

| FQDN | FUNCIONES | IP/MÁSCARA | VLAN | SEDE | PISO/ÁREA | IP PÚBLICA NAT |
|------|-----------|------------|------|------|-----------|----------------|
| fama.com.ar | Servidor Web Principal | 172.1.29.149/25 | 5 | CABA | Piso 10/Sistemas | 200.45.110.132 |
| logistica.fama.com.ar | Servidor Web Logística | 10.68.14.92/26 | - | Santa Fe | Piso 2 | 200.45.110.133 |
| mantenimiento.fama.com.ar | Servidor Web Mantenimiento | 172.1.29.254/25 | 5 | CABA | Piso 10 | 200.45.110.134 |
| compras.fama.com.ar | Intranet de compras | 172.1.29.253/25 | 5 | CABA | Piso 10 | NO TIENE |
| dnsglobal1.fama.com.ar | (EXTERNO) DNS Primario FAMA | 172.1.29.152/25 | 5 | CABA | Piso 10 | 200.45.110.135 |
| dnsglobal1.logistica.fama.com.ar | (EXTERNO) DNS Primario Logística | 10.68.14.125/26 | - | Santa Fe | Piso 2 | 200.45.110.136 |
| dnsglobal2.fama.com.ar | (EXTERNO) DNS Secundario FAMA | 172.1.29.153/25 | 5 | CABA | Piso 10 | 200.45.110.137 |
| dnsglobal2.logistica.fama.com.ar | (EXTERNO) DNS Secundario Logística | 10.68.14.126/26 | - | Santa Fe | Piso 2 | 200.45.110.138 |
| dns1.fama.com.ar | DNS Primario FAMA | 172.1.29.150/25 | 5 | CABA | Piso 10 | |
| dns2.fama.com.ar | DNS Secundario FAMA | 172.1.29.151/25 | 5 | CABA | Piso 10 | |
| dns1.logistica.fama.com.ar | DNS Primario Logística FAMA | 10.68.14.90/26 | - | Santa Fe | Piso 2 | |
| dns2.logistica.fama.com.ar | DNS Secundario Logística FAMA | 10.68.14.90/26 | - | Santa Fe | Piso 2 | |
| smtp.fama.com.ar | Servidor SMTP Fama | 172.1.29.252 | 5 | CABA | Piso 10 | |

## Pruebas con Google
Se agregó, tal como se sugiere en el trabajo, un servidor para prueba de acceso a internet a `www.google.com.ar`.