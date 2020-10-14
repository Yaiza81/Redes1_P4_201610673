# Practica 4 

Se le solicita configurar y administrar los dispositivos de una infraestructura de red para una compañía la cual está empezando a crecer y quieren ampliar su red, un arquitecto
de redes les proporciona el diseño de la topología que será utilizada como
infraestructura de red para dicha compañía, pero deberán de configurarla para proveer
comunicación de acuerdo con las necesidades que se indican.

La compañía cuenta con 2 departamentos: Contabilidad y Ventas. Se debe proveer
comunicación entre los usuarios del mismo departamento, por ejemplo, los usuarios del
departamento de ventas no se podrán comunicar con ningún otro departamento
solamente con host de su mismo departamento.

## Definición de las redes

| VLAN | Dirección de red | Primera Dirección Asignable | Última dirección asignable | Dirección de Broadcast |
| -- | -- | -- | -- | -- |
| 10 | 192.168.13.0/24 | 192.168.13.1 | 192.168.13.254 | 192.168.13.255 |
| 20 | 192.168.23.0/24  | 192.168.23.1 | 192.168.23.254 | 192.168.23.255 |

## Configuración de la topología de red en GNS3.

#### ==============  Configurar los modos de acceso y/o troncal ==================================

###### ESW1

###### ESW2

###### ESW3

###### Switch 1 
- Posicionarse sobre el sw
- Clic derecho y seleccionar configuración 
- Configurar los puertos conectados como en la siguiente imagen 

  ![image](Imagenes/sw1.PNG)

###### Switch 2 
- Posicionarse sobre el sw
- Clic derecho y seleccionar configuración 
- Configurar los puertos conectados como en la siguiente imagen 

   ![image](Imagenes/sw2.PNG)


#### ================  Configuración de VTP   ===================================================

###### ESW1
- conf t
- vtp domain redes1_201610673
- vtp password redes1_201610673
- vtp mode server
- sh vtp status 

    ![image](Imagenes/vtp_1.PNG)

###### ESW2
- conf t
- vtp domain redes1_201610673
- vtp password redes1_201610673
- vtp mode client
- sh vtp status 

    ![image](Imagenes/vtp_2.PNG)

###### ESW3
- conf t
- vtp domain redes1_201610673
- vtp password redes1_201610673
- vtp mode client
- sh vtp status 

    ![image](Imagenes/vtp_3.PNG)
    
#### ==============  Crear VLAN 10, 20   =========================================================

- conf t
- vlan 10
- name VENTAS
- vlan 20
- name CONTABILIDAD
- end

Para comprobar las vlans
- sh vlan-sw

![image](Imagenes/vlans.PNG)

#### ============= Configurar las Subinterfaces del router  ======================================= 

- conf t  
- interface fastethernet 0/0
- no shutdown
- interface fastEthernet 0/0.10
- encapsulation dot1Q 10
- ip address 192.168.13.254 255.255.255.0

- interface fastEthernet 0/0.20
- encapsulation dot1Q 20
- ip address 192.168.23.254 255.255.255.0
- end

Para comprobar 
- sh ip interface brief 

 ![image](Imagenes/router.PNG)
