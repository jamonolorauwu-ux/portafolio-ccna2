# Proyecto de Redes e Interconexión VLANS

###### **ASIGNATURA: Manejo de tecnologías de conmutación y enrutamiento** 
###### **ALUMNO:** Jorge Manuel Hernández Ambrosio
###### **GRUPO:** 5101
###### **INSTITUCIÓN:** Plantel Conalep Oaxaca 039

## ***DIAGRAMA Y TOPOLOGÍA***
<img width="860" height="950" alt="image" src="https://github.com/user-attachments/assets/29d3e410-6946-4a5c-94bf-553541eece96" />

## ***TABLAS DE DIRECCIONAMIENTO***
<br>

| DISPOSITIVO | PUERTOS | CONECTADOS A | PUERTOS |
| ----------- | ------- | ------------ | ------- |
| R1-Core | `g0/0/0` | SW-Core | `fa0/10` |
| SW-Lab1 | `g0/1` | SW-Core | `g0/1` |
| SW-Lab2 | `g0/2` | SW-Core | `g0/2` |
| PC14 GESTIÓN | `fa0/0` | SW-Core | `fa0/9` |
| PC ADMIN | `fa0/0`  | SW-Lab1 - 2 | `fa0/1 - 3` |
| PC ALUMNOS | `fa0/0` | SW-Lab1 - 2 | `fa0/4 - 6` |
| PC DIRECCIÓN |  `fa0/0` | SW-Lab1 - 2 | `fa0/7` |

<br>

## ***CONFIGURACIÓN DE LOS DISPOSITIVOS***

### **ROUTER (R1-Core)**
````
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1-Core-JMHA
R1-Core-JMHA(config)#enable secret CHOCOCHOCO
R1-Core-JMHA(config)#service password-encryption
R1-Core-JMHA(config)#banner motd #ACCESO
````
<br>
<br>

### **SWITCH (SW-Core)**
#### **PC 14 GESTIÓN**
<br>
<br>

### **SWITCH (SW-Lab1)**
##### VLANs & PUERTOS

````
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
#### **PC 0 ADMIN**
#### **PC 1 ADMIN**
#### **PC 2 ADMIN**
<br>

#### **PC 3 ALUMNOS**
#### **PC 4 ALUMNOS**
#### **PC 5 ALUMNOS**
<br>

#### **PC 6 DIRECCIÓN**
<br>
<br>

### **SWITCH (R1-Lab2)**
##### VLANs & PUERTOS
````
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

#### **PC 7 ADMIN**
#### **PC 8 ADMIN**
#### **PC 9 ADMIN**
<br>

#### **PC 10 ALUMNOS**
#### **PC 11 ALUMNOS**
#### **PC 12 ALUMNOS**
<br>

#### **PC 13 DIRECCIÓN**




