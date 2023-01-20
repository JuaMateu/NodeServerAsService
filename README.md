# Desafio 6 - Servidor Node como servicio - devops

Clonar el repositorio necesario para realizar el desafio:

 
```
git clone https://github.com/roxsross/challenge-linux-bash 
```


2- Instalar Node.js y npm:

 
```
sudo apt install nodejs npm 
```


Posicionados en el home, descargar de Node 14:

 
```
cd /home 
```


 
```
curl -sL https://deb.nodesource.com/setup_14.x -o node_setup.sh 
```


Instalar Node 14:

 
```
sudo bash node_setup.sh 
```


Instalar gcc, g++ y make

 
```
sudo apt install gcc g++ make 
```


Finalizar el proceso de instalación de la versión 14 de Node:

 
```
sudo apt install -y nodejs 
```


Agregar el usuario nodejs si todavía no lo creaste:

 
```
sudo adduser nodejs 
```


En la carpeta de src/, ejecutar el archivo server.js:


 
```
node server.js 
```


Crear un archivo de configuración para el servicio de Node

 
```
sudo nano /lib/systemd/system/devops@.service 
```

 
```

sudo cat /lib/systemd/system/devops.service

[Unit]
Description=Balanceo para desafio Final
Documentation=https://github.com/roxsross/challenge-linux-bash
After=network.target

[Service]
Enviroment=NODE_PORT=3000
Type=simple
User=nodejs
WorkingDirectory=//home/challenge-linux-bash
ExecStart=/usr/bin/node /home/challenge-linux-bash/server.js
Restart=on-failure

[Install]
WantedBy=multi-user.target
 
```


Nos aseguramos de que la carpeta y archivos del servidor node pertenezcan a nodejs y tengan permisos de ejecucion


 
```

tree -puf challenge-linux-bash

[drwxr-xr-x nodejs  ]  challenge-linux-bash
├── [-rw-rw-r-- nodejs  ]  challenge-linux-bash/package.json
├── [-rw-rw-r-- nodejs  ]  challenge-linux-bash/Readme.md
└── [-rwxr-xr-x nodejs  ]  challenge-linux-bash/server.js
 
```



Habilitamos el servicio que corre le servidor node

 
```
sudo systemctl enable devops.service 
```


Controlamos que se ejecute exitosamente

 
```

systemctl status devops.service

● devops.service - Balanceo para desafio Final
     Loaded: loaded (/lib/systemd/system/devops.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2023-01-20 16:09:03 UTC; 32min ago
       Docs: https://github.com/roxsross/challenge-linux-bash
   Main PID: 663 (node)
      Tasks: 7 (limit: 2236)
     Memory: 40.3M
        CPU: 107ms
     CGroup: /system.slice/devops.service
             └─663 /usr/bin/node /home/challenge-linux-bash/server.js

Jan 20 16:09:03 ubuntuserver2 systemd[1]: Started Balanceo para desafio Final.
Jan 20 16:09:04 ubuntuserver2 node[663]: Servidor corriendo en el puerto 3000
 
```

El servidor ya esta corriendo el puerto 3000


# 2- Generar un script
podemos usar este script para arrancar o denter el servidor.

 
```

# bash script to run nodejs
$ARGS = $1
$PATH = $2
if [ $ARGS = "start" ]
then
    echo "Starting server"
     node $PATH
elif [ $ARGS = "stop" ]
then
    echo "Stopping server"
    killall node
else
    echo "Invalid argument"
fi
 
```


## Scripts de arranque de servidor Node package.json
Otra opcion es hacer un npm init en el proyecto, lo que generará un package.json.

En la seccion de scripts podemos armar los scripts necesarios para correr con el comando
'npm {nombre-script}'

 
```

{
  "name": "challenge-linux-bash",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
 "scripts": {
    "start": "node server.js",
    "test": "nodemon server.js"
    "stop": "killall node"
    "serviceEnable": "systemctl enable devops.service"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/roxsross/challenge-linux-bash.git"  
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/roxsross/challenge-linux-bash/issues"   
  },
  "homepage": "https://github.com/roxsross/challenge-linux-bash#readme"
}
 
```
