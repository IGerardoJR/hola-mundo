## Proceso de instalacion

Durante el proceso de instalacion no podras usar el mouse para desplazarte, por lo cual se trata de un instalador de texto. Por lo que el unico medio por el cual podras deslizarte atraves de los campos es mediante el teclado.

En las primeras 3 pantallas puedes dejar los valores por defecto y darle a "Hecho"

En el almacenamiento asegurate de que este seleccionada la unidad vas a usar y sobretodo ten en cuenta que usara todo el almacenamiento.

# particiones
Punto clave, por defecto Ubuntu te creara un sistema de particionado. Pero ese sistema por lo regular suele dejar mucho espacio sin usar, por lo que vete a la parte de abajo en donde dice "reset" o "Reestablecer/Reiniciar"
![particiones](https://github.com/IGerardoJR/hola-mundo/blob/main/dale%20a%20reset.png)
y en donde dice free space dale enter y te debera aparecer un mini submenu. Le das en donde dice add new gpt partition y te debera aparecer algo como lo siguiente.

### boot
Le asignas un 1 de almacenamiento y en donde dice punto de montaje buscas uno donde diga /boot
![particiones-boot](https://github.com/IGerardoJR/hola-mundo/blob/main/boot.png)

### Resto del almacenamiento
Vuelves a realizar el mismo procedimiento (darle enter a free space) > add gpt partition y el espacio restante se lo das al punto de montaje que diga "/"
![particiones-boot](https://github.com/IGerardoJR/hola-mundo/blob/main/restante%20raiz.png)


### username y nombre servidor
Asignale los valores que quieras, solo anota bien los datos.
![particiones-boot](https://github.com/IGerardoJR/hola-mundo/blob/main/username%20y%20servidor.png)


### ssh
Importante, con la barra de espacio dale en donde dice Instalar Servidor OpenSSH
una vez la hayas marcado dale a "Hecho"
![particiones-boot](https://github.com/IGerardoJR/hola-mundo/blob/main/instalar_ssh.png)


### featured server snaps
Te puedes brincar esa parte.
![particiones-boot](https://github.com/IGerardoJR/hola-mundo/blob/main/por-el-momento-no-instalar-nada.png)


### Proceso de instalacion
Despues de todas las pantallas debera empezar el proceso de instalacion y una vez culmine se habilitara en la parte inferior la opcion "Reiniciar ahora"
![particiones-boot](https://github.com/IGerardoJR/hola-mundo/blob/main/instalacion_completada.png)


## Comandos inciales
### Obtener las actualizaciones mas recientes del SO

```sh
sudo apt-get update && sudo apt-get upgrade
```

### Instalar las herramientas esenciales de ssh

```shell
sudo apt-get install openssh-server
sudo apt-get install ssh
```

### Instalar el siguiente paquete: El cual nos ayudara mas que nada a obtener la ip del servidor

```shell
sudo apt-get install net-tools
```

### Configurando SSH

Verifica si el proceso de ssh esta activo, con

```sh
sudo systemctl status ssh
```

Si sale active todo bien, pero en caso contrario levanta el servicio con

```sh
sudo systemctl enable ssh
sudo systemctl start ssh
```

Vuelves a verificar el estado con:

```sh
sudo systemctl status ssh
```

y ya deberia salir en "activo". En caso de que siga saliendo inactivo reinicias la maquina con :

```shell
reboot
```

#### Puertos

El puerto por defecto es el 22, si deseas cambiarlo dirijete al archivo de configuracion

```shell
sudo nano /etc/ssh/sshd_config
```

Si desides modificar el archivo busca una variable llamada Port, muy seguramente vendra comentada por defecto de esta forma.

```
# Port 22
```

quitale el # y modifica el valor numerico a un puerto que creas con el que no habra conflictos, puedes usar por ejemplo: 3333, 2222,etc.

##### Abriendo los puertos

Una vez hayas definido los puertos es hora de abrir los puertos con los siguientes comandos.
en donde puerto lo reemplazas por el que hayas decidido asignar o en caso de no haber modificado nada lo dejas en 22.

```shell
sudo ufw allow ssh
sudo ufw allow <puerto>/tcp
```

### Obteniendo Ip del servidor.

Por ultimo antes de probar ssh, obten la direccion ip del servidor. Esto lo puedes hacer con el siguiente comando.

```sh
ip a
```

buscas una parte donde diga inet y es ahi en donde veras la ip a la cual deberas hacer la solicitud cuando uses ssh. Esta ip puede ser 192.168.XX.XX, etc.

### Probando la conexion.

Abre una terminal windows y escribes lo siguiente

```shell
ssh <usuario>@<direccion-ip-del-servidor>
```

En caso de tener un puerto distinto al 22, la estructura del comando seria la siguiente:

```sh
ssh <usuario>@<direccion-ip-del-servidor> -p <puerto>
```

### Instalando escritorio grafico.

Si quieres la interfaz grafica vas a necesitar instalar el servidor grafico.

```shell
sudo apt-get install xorg mate
```

En donde xorg es el servidor grafico y mate el tipo de escritorio que se usa.De antemano te digo que puede tardar un poco este proceso.

Una vez se haya completado esta tarea, solo quedara inicializar el proceso con

```shell
startx
```

Si todo salio bien te debera deberas ya poder interfaz grafica. El comando startx lo tendras que usar cada vez que vayas a inicializar en modo GUI.
