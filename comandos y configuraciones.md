VLAN 2 - Administracion 
172.1.28.0 -> 172.1.28.127
172.1.28.0/25

Primera IP de prueba: 172.1.28.10
Gateway: 172.1.28.1

255.255.255.128

VLAN 3 - Servicios
172.1.28.128 -> 172.1.28.255
172.1.28.128/25

Primera IP de prueba: 172.1.28.138
Gateway: 172.1.28.129

255.255.255.128

VLAN 4 - Gerencia
172.1.29.0 -> 172.1.29.127
172.1.29.0/25

Primera IP de prueba: 172.1.29.10
Gateway: 172.1.29.1

255.255.255.128

VLAN 5 - Sistemas
172.1.29.128 -> 172.1.29.255
172.1.29.128/25

Primera IP de prueba: 172.1.29.138
Gateway: 172.1.29.129


255.255.255.128


--declarar interfaz del router con el switch
Router(config)# interface FastEthernet0/0
Router(config-if)# no shutdown

--hacer subinterfaz para vlan2
Router(config)# interface FastEthernet0/0.2
Router(config-subif)# encapsulation dot1Q 2
– gateway de la vlan
Router(config-subif)# ip address 172.1.28.1 255.255.255.128
–helper para dhcp
Router(config-subif)# ip helper-address 172.1.28.1

--hacer subinterfaz para vlan3
Router(config)# interface FastEthernet0/0.3
Router(config-subif)# encapsulation dot1Q 3
Router(config-subif)# ip address 172.1.28.129 255.255.255.128
–helper para dhcp
Router(config-subif)# ip helper-address 172.1.28.129


--hacer subinterfaz para vlan4
Router(config)# interface FastEthernet0/0.4
Router(config-subif)# encapsulation dot1Q 4
Router(config-subif)# ip address 172.1.29.1 255.255.255.128
Router(config-subif)# ip helper-address 172.1.29.1


--hacer subinterfaz para vlan5
Router(config)# interface FastEthernet0/0.5
Router(config-subif)# encapsulation dot1Q 5
Router(config-subif)# ip address 172.1.29.129 255.255.255.128
Router(config-subif)# ip helper-address 172.1.29.129

--pool de dhcp
--vlan admin
Router(config)# ip dhcp pool pool-caba-admin
Router(dhcp-config)# network 172.1.28.0 255.255.255.128
Router(dhcp-config)# default-router 172.1.28.1
Router(dhcp-config)# dns-server 10.68.14.68

--vlan servicios
Router(config)# ip dhcp pool pool-caba-svc
Router(dhcp-config)# network 172.1.28.128 255.255.255.128
Router(dhcp-config)# default-router 172.1.28.129
Router(dhcp-config)# dns-server 10.68.14.68

--vlan gerencia
Router(config)# ip dhcp pool pool-caba-gcia
Router(dhcp-config)# network 172.1.29.0 255.255.255.128
Router(dhcp-config)# default-router 172.1.29.1
Router(dhcp-config)# dns-server 10.68.14.68

--vlan sistemas
Router(config)# ip dhcp pool pool-caba-sist
Router(dhcp-config)# network 172.1.29.128 255.255.255.128
Router(dhcp-config)# default-router 172.1.29.129
Router(dhcp-config)# dns-server 10.68.14.68


#redes internas
router caba - sf
caba -> fa 5/0 10.68.14.5 -> 255.255.255.252
sf   -> fa 4/0 10.68.14.6 -> 255.255.255.252

router caba - cba
caba -> fa 4/0 10.68.14.1 -> 255.255.255.252
cba  -> fa 4/0 10.68.14.2 -> 255.255.255.252

router cba - sf
cba -> fa 5/0 10.68.14.9 -> 255.255.255.252
sf -> fa 5/0 10.68.14.10 -> 255.255.255.252


#config sniffer caba

monitor session 1 source interface fastEthernet 0/1 both
monitor session 1 source interface fastEthernet 1/1 both
monitor session 1 source interface fastEthernet 2/1 both
monitor session 1 source interface fastEthernet 3/1 both
monitor session 1 source interface fastEthernet 4/1 both
monitor session 1 source interface fastEthernet 5/1 both
monitor session 1 source interface ethernet 7/1 both
monitor session 1 source interface ethernet 8/1 both
monitor session 1 source interface ethernet 9/1 both
monitor session 1 destination interface Gig7/1


FAMA.COM.AR 
127.1.29.129->200.45.110.132
LOGISTICA.FAMA.COM.AR
10.68.14.92->200.45.110.133
MANTENIMIENTO.FAMA.COM.AR
172.1.29.254->200.45.110.134


TIENEN QUE TENER UN MAPEO NAT IP ESTATICA
LO MISMO LOS DOS DNS
LO MISMO LOS DOS DNS DE SANTA FE

200.45.110.128/25

ip nat inside source static 172.1.29.149 200.45.110.132 --FAMA.COM.AR
ip nat inside source static 10.68.14.92 200.45.110.133 -- LOGISTICA.FAMA.COM.AR
ip nat inside source static 172.1.29.254 200.45.110.134 -- MANTENIMIENTO.FAMA.COM.AR
ip nat inside source static 172.1.29.152 200.45.110.135 -- DNS GLOBAL 1 FAMA
ip nat inside source static 10.68.14.127 200.45.110.136 -- DNS GLOBAL 1 LOGISTICA



0 hasta 255 es el pool disponible
0 hasta 255 vamos a usar como pool de NAT dinámico
no tenemos espacio para el estático


<--borrar-->
no ip nat inside source static 10.68.14.92 200.45.110.133
no ip nat inside source static 172.1.29.254 200.45.110.134 
no ip nat inside source static 172.1.29.149 200.45.110.132 
no ip nat inside source static 172.1.29.152 200.45.110.135 
no ip nat inside source static 10.68.14.240 200.45.110.136 


NUEVO RANGO NAT:
ip nat pool POOL-NAT-FAMA 200.45.110.193 200.45.110.254 netmask 255.255.255.128

<--RECREAR-->
ip nat inside source static 172.1.29.149 200.45.110.132 --FAMA.COM.AR
ip nat inside source static 10.68.14.92 200.45.110.133 -- LOGISTICA.FAMA.COM.AR
ip nat inside source static 172.1.29.254 200.45.110.134  -- MANTENIMIENTO.FAMA.COM.AR
ip nat inside source static 172.1.29.152 200.45.110.135  -- DNS GLOBAL 1 FAMA
ip nat inside source static 10.68.14.125 200.45.110.136  -- DNS GLOBAL 1 LOGISTICA
ip nat inside source static 172.1.29.153 200.45.110.137  -- DNS GLOBAL 2 FAMA
ip nat inside source static 10.68.14.126 200.45.110.138  -- DNS GLOBAL 2 LOGISTICA

SEGMENTOS Y DHCP
SEGMENTOS	SEDE	RANGO	MASCARA	DESDE	HASTA	HOST UTILES
SANTA FE	10.68.14.64/26	255.255.255.192	10.68.14.64	10.68.14.127	62
CORDOBA	10.68.14.128/27	255.255.255.224	10.68.14.128	10.68.14.159	30
ISP	205.32.130.0/30	255.255.255.252	205.32.130.0	205.32.130.3	2
CABA	172.1.29.0/23	255.255.254.0	172.1.29.0	172.1.30.255	510
NAT	200.45.110.128/25	255.255.255.128	200.45.110.128	200.45.110.255	126
						
TRANSPORTE	CABA CORDOBA	10.68.14.0/30	255.255.255.252	10.68.14.0	10.68.14.3	
CABA STFE	10.68.14.4/30	255.255.255.252	10.68.14.4	10.68.14.7	
CORDOBA STFE	10.68.14.8/30	255.255.255.252	10.68.14.8	10.68.14.11




VLAN 2 - Administracion 
172.1.28.0 -> 172.1.28.127
172.1.28.0/25

Primera IP de prueba: 172.1.28.10
Gateway: 172.1.28.1

255.255.255.128

VLAN 3 - Servicios
172.1.28.128 -> 172.1.28.255
172.1.28.128/25

Primera IP de prueba: 172.1.28.138
Gateway: 172.1.28.129

255.255.255.128

VLAN 4 - Gerencia
172.1.29.0 -> 172.1.29.127
172.1.29.0/25

Primera IP de prueba: 172.1.29.10
Gateway: 172.1.29.1

255.255.255.128

VLAN 5 - Sistemas
172.1.29.128 -> 172.1.29.255
172.1.29.128/25

Primera IP de prueba: 172.1.29.138
Gateway: 172.1.29.129


255.255.255.128


--declarar interfaz del router con el switch
Router(config)# interface FastEthernet0/0
Router(config-if)# no shutdown

--hacer subinterfaz para vlan2
Router(config)# interface FastEthernet0/0.2
Router(config-subif)# encapsulation dot1Q 2
Router(config-subif)# ip address 172.1.28.1 255.255.255.128
Router(config-subif)# ip helper-address 172.1.28.1

--hacer subinterfaz para vlan3
Router(config)# interface FastEthernet0/0.3
Router(config-subif)# encapsulation dot1Q 3
Router(config-subif)# ip address 172.1.28.129 255.255.255.128
Router(config-subif)# ip helper-address 172.1.28.129


--hacer subinterfaz para vlan4
Router(config)# interface FastEthernet0/0.4
Router(config-subif)# encapsulation dot1Q 4
Router(config-subif)# ip address 172.1.29.1 255.255.255.128
Router(config-subif)# ip helper-address 172.1.29.1


--hacer subinterfaz para vlan5
Router(config)# interface FastEthernet0/0.5
Router(config-subif)# encapsulation dot1Q 5
Router(config-subif)# ip address 172.1.29.129 255.255.255.128
Router(config-subif)# ip helper-address 172.1.29.129

--pool de dhcp
--vlan admin
Router(config)# ip dhcp pool pool-caba-admin
Router(dhcp-config)# network 172.1.28.0 255.255.255.128
Router(dhcp-config)# default-router 172.1.28.1
Router(dhcp-config)# dns-server 10.68.14.68

--vlan servicios
Router(config)# ip dhcp pool pool-caba-svc
Router(dhcp-config)# network 172.1.28.128 255.255.255.128
Router(dhcp-config)# default-router 172.1.28.129
Router(dhcp-config)# dns-server 10.68.14.68

--vlan gerencia
Router(config)# ip dhcp pool pool-caba-gcia
Router(dhcp-config)# network 172.1.29.0 255.255.255.128
Router(dhcp-config)# default-router 172.1.29.1
Router(dhcp-config)# dns-server 10.68.14.68

--vlan sistemas
Router(config)# ip dhcp pool pool-caba-sist
Router(dhcp-config)# network 172.1.29.0 255.255.255.128
Router(dhcp-config)# default-router 172.1.29.129
Router(dhcp-config)# dns-server 10.68.14.68


SEGMENTOS	SEDE	RANGO	MASCARA	DESDE	HASTA	HOST UTILES
	SANTA FE	10.68.14.64/26	255.255.255.192	10.68.14.64	10.68.14.127	62
	CORDOBA	10.68.14.128/27	255.255.255.224	10.68.14.128	10.68.14.159	30
	ISP	205.32.130.0/30	255.255.255.252	205.32.130.0	205.32.130.3	2
	CABA	172.1.29.0/23	255.255.254.0	172.1.29.0	172.1.30.255	510
	NAT	200.45.110.128/25	255.255.255.128	200.45.110.128	200.45.110.255	126
						
TRANSPORTE	CABA CORDOBA	10.68.14.0/30	255.255.255.252	10.68.14.0	10.68.14.3	
	CABA STFE	10.68.14.4/30	255.255.255.252	10.68.14.4	10.68.14.7	
	CORDOBA STFE	10.68.14.8/30	255.255.255.252	10.68.14.8	10.68.14.11	