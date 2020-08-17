<img src="https://portal.ingenieria.usac.edu.gt/images/2019/logo/logo-fiusac.png"/>



**NOMBRE**: FRANCISCO HUMBERTO LEZANA RAMOS  
**CARNET**: 201503777  
**CURSO**: REDES DE COMPUTADORAS 1

# MANUAL DE CONFIGURACIÓN

## HERRAMIENTAS A UTILIZAR 

- GNS3
- Software de virtualización (VMWare o Virtual Box) instalados y configurado para uso con GNS3.

## TOPOLOGIA DE RED DEL PROYECTO 

La siguiente topología cuenta con 4 host de los cuales 3 son VPCS y 1 es una máquina virtual con un sistema tiny-linux para ahorrar recursos, podemos observar que los host se conectan a 2 switches distintos y estos se conectan entre sí por medio de un router el cuál será centro principal de comunicación.
<img src="/src/topologia.PNG"/>


## CONFIGURACIÓN DE LA TOPOLOGÍA DE RED EN GNS3

### DIRECCIONES IP DE LOS HOST

Para esta práctica se van a utilizar las siguientes direcciones IP, la X y Y representan el último y penúltimo número del carnét del estudiante. El carnet del usuario es 201503777 , se utilizarán X:7 y Y:8 para evitar errores al momento de conectar los host.  

<img src="/src/ips.PNG"/> 

Las interfaces del router poseerán las siguientes ips:  

<img src="/src/iprouter.PNG"/>   


### CONFIGURACIÓN DE INTERFACES FAST ETHERNET DEL ROUTER C3725

Una vez con la topología realizada en GNS3, y con el router iniciado abrimos la terminal para empezar a configurarlo, veremos la siguiente ventana:  
<img src="/src/r1.PNG" alt="drawing" width="600"/> 

Para entrar a la configuración del router scribimos el siguiente comando:
#### conf t  

<img src="/src/r2.PNG" alt="drawing" width="600"/> 

Una vez adentro para configurar la interfaz FastEthernet0/0 escribimos: 
#### int f0/0  

<img src="/src/r3.PNG" alt="drawing" width="600"/> 

Ahora asignamos una dirección ip a la interfaz y la máscara de red con el siguiente comando:
#### ip address 192.168.17.254 255.255.255.0  

<img src="/src/r4.PNG" alt="drawing" width="600"/> 
  
Una vez asignada al ip para esta interfaz activamos la activamos con el comando:
#### no shut  

<img src="/src/r5.PNG" alt="drawing" width="600"/> 

Salimos de la configuración de interfaz con el comando:
#### exit  

<img src="/src/r6.PNG" alt="drawing" width="600"/> 

Configuramos la otra interfaz que es la FastEthernet0/1 con los mismos comandos que utilizamos en la interfaz anterior, solamente aplicando cambios en el nombre de la interfaz y la dirección IP de esta.  
Para entrar a la configuración del router scribimos el siguiente comando:
#### conf t  

<img src="/src/r2.PNG" alt="drawing" width="600"/> 

Una vez adentro para configurar la interfaz FastEthernet0/1 escribimos: 
#### int f0/1  

<img src="/src/r7.PNG" alt="drawing" width="600"/> 

Ahora asignamos una dirección ip a la interfaz y la máscara de red con el siguiente comando:
#### ip address 192.168.18.254 255.255.255.0  

<img src="/src/r8.PNG" alt="drawing" width="600"/> 
  
Una vez asignada al ip para esta interfaz activamos la activamos con el comando:
#### no shut  

<img src="/src/r9.PNG" alt="drawing" width="600"/> 

Salimos de la configuración de interfaz con el comando:
#### exit  

<img src="/src/r10.PNG" alt="drawing" width="600"/> 

Salimos de la configuración del router con el comando exit y escribimos el siguiente comando para ver las direcciones asignadas
#### sh ip int brief  

<img src="/src/r11.PNG" alt="drawing" width="600"/> 

Por último escribimos el siguiente comando para guardar los cambios permanentemente
#### wr  

<img src="/src/r12.PNG" alt="drawing" width="600"/> 


### CONFIGURACIÓN DE HOST PC2
Una vez configuradas las direcciones de las interfaces del router, procedemos a encender nuestros host, en este caso la que tiene por nombre PC2, ingresando a la consola tendríamos la siguiente ventana:  
<img src="/src/pc1.PNG" alt="drawing" width="600"/> 

A continuación asignamos la IP y definimos el gateway correspondiente a esta máquina con el siguiente comando:
#### ip 192.168.17.15 192.168.17.254  

<img src="/src/pc2.PNG" alt="drawing" width="600"/> 

Para mostrar las configuraciones que hemos realizado podemos ejecutar el siguiente comando:
#### show ip  

<img src="/src/pc3.PNG" alt="drawing" width="600"/> 

Por último utilizamos el siguiente comando para guardar las configuraciones realizadas
#### save

<img src="/src/pc4.PNG" alt="drawing" width="600"/> 

Realizamos la misma configuracion en los otros host para asignar la ip y el gateway correspondientes.  

### CONFIGURACIÓN DE HOST PC3
Asignamos la IP y definimos el gateway correspondiente a esta máquina con el siguiente comando:
#### ip 192.168.18.15 192.168.18.254  

<img src="/src/pc5.PNG" alt="drawing" width="600"/> 

Guardamos las configuraciones realizadas con el siguiente comando:
#### save

<img src="/src/pc6.PNG" alt="drawing" width="600"/> 

### CONFIGURACIÓN DE HOST PC4
Asignamos la IP y definimos el gateway correspondiente a esta máquina con el siguiente comando:
#### ip 192.168.18.30 192.168.18.254  

<img src="/src/pc7.PNG" alt="drawing" width="600"/> 

Guardamos las configuraciones realizadas con el siguiente comando:
#### save

<img src="/src/pc8.PNG" alt="drawing" width="600"/> 

### CONFIGURACIÓN DE HOST LINUX-1
Procedemos a encender nuestra máquina virtual y para esta práctica se utilizó TinyCore Linux, veremos una ventana en donde seleccionaremos la opción llamada **Boot TinyCore** para iniciar el sistema operativo 

<img src="/src/linux1.PNG" alt="drawing" width="600"/> 

<img src="/src/linux2.PNG" alt="drawing" width="600"/> 


Una vez ubicados en el escritorio, nos dirigimos a la parte inferior de esta y buscamos la opcion que se llama **Panel de Control** la cual nos permitirá acceder a las configuraciones de la máquina:

<img src="/src/linux3.PNG" alt="drawing" width="600"/> 

Estando en el menú que nos apareció seleccionamos la opción de **Network**, para gestionar las configuraciones de red

<img src="/src/linux4.PNG" alt="drawing" width="600"/> 

En el apartado de **IP Address** escribiremos la dirección IP asignada a esta máquina la cuál es: **192.168.17.30** , el sistema identificará el Gateway automáticamente, selecccionamos la opción de **Apply** y luego **Exit** para finalizar con la configuración

<img src="/src/linux5.PNG" alt="drawing" width="600"/> 

## PRUEBAS DE CONFIGURACION 

Para comprobar el correcto funcionamiento de la topología realizada y verificar que las direcciones ip se hayan asignado correctamente realizaremos pruebas de comunicación entre los host configurados, para ello utilizaremos el comando **ping**

### PRUEBAS DE CONEXIÓN PC2

En la consola debemos escribir los siguientes comandos:  
- COMUNICACIÓN CON EL HOST LINUX-1:  **ping 192.168.17.30**
- COMUNICACIÓN CON EL HOST PC3:      **ping 192.168.18.15**
- COMUNICACIÓN CON EL HOST PC4:      **ping 192.168.18.30**

<img src="/src/test1.PNG" alt="drawing" width="600"/>

### PRUEBAS DE CONEXIÓN PC3

En la consola debemos escribir los siguientes comandos:  
- COMUNICACIÓN CON EL HOST LINUX-1:  **ping 192.168.17.30**
- COMUNICACIÓN CON EL HOST PC2:      **ping 192.168.17.15**
- COMUNICACIÓN CON EL HOST PC4:      **ping 192.168.18.30**

<img src="/src/test2.PNG" alt="drawing" width="600"/> 

### PRUEBAS DE CONEXIÓN PC4

En la consola debemos escribir los siguientes comandos:  
- COMUNICACIÓN CON EL HOST LINUX-1:  **ping 192.168.17.30**
- COMUNICACIÓN CON EL HOST PC2:      **ping 192.168.17.15**
- COMUNICACIÓN CON EL HOST PC3:      **ping 192.168.18.15**

<img src="/src/test3.PNG" alt="drawing" width="600"/> 

### PRUEBAS DE CONEXIÓN LINUX-1

En la consola de la máquina virtual debemos escribir los siguientes comandos:  
- COMUNICACIÓN CON EL HOST PC2:      **ping 192.168.17.15**
- COMUNICACIÓN CON EL HOST PC3:      **ping 192.168.18.15**
- COMUNICACIÓN CON EL HOST PC4:      **ping 192.168.18.30**

<img src="/src/test4.PNG" alt="drawing" width="600"/> 

  
    
## GLOSARIO 










