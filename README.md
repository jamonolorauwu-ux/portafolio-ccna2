# Proyecto de Redes e Interconexión VLANS

###### **ASIGNATURA: Manejo de tecnologías de conmutación y enrutamiento** 
###### **ALUMNO:** Jorge Manuel Hernández Ambrosio
###### **GRUPO:** 5101
###### **INSTITUCIÓN:** Plantel Conalep Oaxaca 039

## ***DIAGRAMA Y TOPOLOGÍA***
<img width="860" height="950" alt="image" src="https://github.com/user-attachments/assets/29d3e410-6946-4a5c-94bf-553541eece96" />

## ***TABLAS DE DIRECCIONAMIENTO***

### PUERTOS

| DISPOSITIVO | PUERTOS | CONECTADOS A | PUERTOS |
| ----------- | ------- | ------------ | ------- |
| R1-Core | `g0/0/0` | SW-Core | `fa0/10` |
| SW-Lab1 | `g0/1` | SW-Core | `g0/1` |
| SW-Lab2 | `g0/2` | SW-Core | `g0/2` |
| PC14 GESTIÓN | `fa0/0` | SW-Core | `fa0/9` |
| PC ADMIN | `fa0/0`  | SW-Lab1 - 2 | `fa0/1 - 3` |
| PC ALUMNOS | `fa0/0` | SW-Lab1 - 2 | `fa0/4 - 6` |
| PC DIRECCIÓN |  `fa0/0` | SW-Lab1 - 2   | `fa0/7` |

### SW-Lab1

| PCs | IP | IP | MÁSCARA |
| --- | -- | -- | ------- |
| PC 0 ADMIN | | | |
| PC 1 ADMIN | | | |
| PC 2 ADMIN | | | |
| PC 3 ADMINISTRACION | | | |
| PC 4 ADMINISTRACION | | | |
| PC 5 ADMINISTRACION | | | |
| PC 6 DIRECCION | | | |

### SW-Lab2

| PCs | IP | IP | MÁSCARA |
| --- | -- | -- | ------- |
| PC 7 ADMIN | | | |
| PC 8 ADMIN | | | |
| PC 9 ADMIN | | | |
| PC 10 ALUMNOS | | | |
| PC 11 ALUMNOS | | | |
| PC 12 ALUMNOS | | | |
| PC 13 DIRECCION | | | |

### SW-Core

| PCs | IP | IP | MÁSCARA |
| --- | -- | -- | ------- |
| PC 14 GESTION | | | |



<br>

## ***CONFIGURACIÓN DE LOS DISPOSITIVOS***

### **ROUTER (R1-Core)**
````bash
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1-Core-JMHA
R1-Core-JMHA(config)#enable secret CHOCOCHOCO
R1-Core-JMHA(config)#service password-encryption
R1-Core-JMHA(config)#banner motd #ACCESO REESTRINGIDO#
R1-Core-JMHA(config)#line console 0
R1-Core-JMHA(config-line)#password CHOCOCHOCO
R1-Core-JMHA(config-line)#login
R1-Core-JMHA(config-line)#exit
````
````bash
ACCESO REESTRINGIDO

User Access Verification

Password: 

R1-Core-JMHA>enable
Password: 
R1-Core-JMHA#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1-Core-JMHA(config)#interface gi0/0/0
R1-Core-JMHA(config-if)#no ip address
R1-Core-JMHA(config-if)#no shutdown
R1-Core-JMHA(config-if)#exit
R1-Core-JMHA(config)#interface gi0/0/0.10
R1-Core-JMHA(config-subif)#
%LINK-3-UPDOWN: Interface GigabitEthernet0/0/0.10, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0.10, changed state to up

R1-Core-JMHA(config-subif)#encapsulation dot1Q 10
R1-Core-JMHA(config-subif)#ip address 192.168.10.254 255.255.255.0
R1-Core-JMHA(config-subif)#exit
R1-Core-JMHA(config)#interface gi0/0/0.20
R1-Core-JMHA(config-subif)#
%LINK-3-UPDOWN: Interface GigabitEthernet0/0/0.20, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0.20, changed state to up

R1-Core-JMHA(config-subif)#encapsulation dot1Q 20
R1-Core-JMHA(config-subif)#ip address 192.168.20.254 255.255.255.0
R1-Core-JMHA(config-subif)#exit
R1-Core-JMHA(config)#interface gi0/0/0.30
R1-Core-JMHA(config-subif)#
%LINK-3-UPDOWN: Interface GigabitEthernet0/0/0.30, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0.30, changed state to up

R1-Core-JMHA(config-subif)#encapsulation dot1Q 30
R1-Core-JMHA(config-subif)#ip address 192.168.30.254 255.255.255.0
R1-Core-JMHA(config-subif)#exit
R1-Core-JMHA(config)#interface gi0/0/0.99
R1-Core-JMHA(config-subif)#
%LINK-3-UPDOWN: Interface GigabitEthernet0/0/0.99, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0.99, changed state to up

R1-Core-JMHA(config-subif)#encapsulation dot1Q 99
R1-Core-JMHA(config-subif)#ip address 192.168.99.254 255.255.255.0
R1-Core-JMHA(config-subif)#exit
R1-Core-JMHA(config)#interface gi0/0/0.111
R1-Core-JMHA(config-subif)#
%LINK-3-UPDOWN: Interface GigabitEthernet0/0/0.111, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0.111, changed state to up

R1-Core-JMHA(config-subif)#encapsulation dot1Q 111 native
R1-Core-JMHA(config-subif)#no ip address
R1-Core-JMHA(config-subif)#exit
R1-Core-JMHA(config)#end
R1-Core-JMHA#
%SYS-5-CONFIG_I: Configured from console by console
````
<br>

### **SWITCH (SW-Core)**
````bash
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW-Core-JMHA
SW-Core-JMHA(config)#enable secret CHOCO
SW-Core-JMHA(config)#service password-encryption
SW-Core-JMHA(config)#banner motd #ACCESO REESTRINGIDO#
SW-Core-JMHA(config)#line console 0
SW-Core-JMHA(config-line)#password CHOCO
SW-Core-JMHA(config-line)#login
SW-Core-JMHA(config-line)#end
SW-Core-JMHA#
%SYS-5-CONFIG_I: Configured from console by console

SW-Core-JMHA#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Core-JMHA(config)#vlan 10
SW-Core-JMHA(config-vlan)#name ADMIN
SW-Core-JMHA(config-vlan)#exit
SW-Core-JMHA(config)#vlan 20
SW-Core-JMHA(config-vlan)#name ALUMNOS
SW-Core-JMHA(config-vlan)#exit
SW-Core-JMHA(config)#vlan 30
SW-Core-JMHA(config-vlan)#name DIRECCION
SW-Core-JMHA(config-vlan)#exut
                            ^
% Invalid input detected at '^' marker.
	
SW-Core-JMHA(config-vlan)#exit
SW-Core-JMHA(config)#vlan 99
SW-Core-JMHA(config-vlan)#name GESTION
SW-Core-JMHA(config-vlan)#exit
SW-Core-JMHA(config)#vlan 111
SW-Core-JMHA(config-vlan)#name native
SW-Core-JMHA(config-vlan)#exit
SW-Core-JMHA(config)#vlan 999
SW-Core-JMHA(config-vlan)#name blackhole
SW-Core-JMHA(config-vlan)#exit
SW-Core-JMHA(config)#end
SW-Core-JMHA#
%SYS-5-CONFIG_I: Configured from console by console

SW-Core-JMHA#
````
<br>


### **SWITCH (SW-Lab1)**
##### VLANs & PUERTOS

````bash
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 10
Switch(config-vlan)#name ADMIN
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name ALUMNOS
Switch(config-vlan)#exit
Switch(config)#vlan 30
Switch(config-vlan)#name DIRECCION
Switch(config-vlan)#end
Switch#
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#interface range fa0/1 - 3
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10
Switch(config-if-range)#exit
Switch(config)#interface range fa0/4 - 6
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20
Switch(config-if-range)#exit
Switch(config)#interface fa0/7
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 30
Switch(config-if)#end
````
<br>

### **SWITCH (R1-Lab2)**
##### VLANs & PUERTOS
````bash
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 10
Switch(config-vlan)#name ADMIN
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name ALUMNOS
Switch(config-vlan)#exit
Switch(config)#vlan 30
Switch(config-vlan)#name DIRECCION
Switch(config-vlan)#end
Switch#
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#interface range fa0/1 - 3
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10
Switch(config-if-range)#exit
Switch(config)#interface range fa0/4 - 6
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20
Switch(config-if-range)#exit
Switch(config)#interface fa0/7
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 30
Switch(config-if)#end
````
<br>





