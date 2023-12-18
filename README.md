# Proyecto de redes 2 y 3
### Autores:  Carlos Sandoval y Valentina Yañez

## Introducción
En el siguiente documento se detalla como replicar la experiencia de proyecto 2 y 3. La idea principal del siguiente proyecto es demostrar habilidades como administrador de sistemas, para lo cual levantaremos servicios con Docker y Kubernetes. Haremos un levantamiento con Docker compose, otro con Kubernetes e iremos experimentando que sucede cuando estos son atacados.

## Instalación
En primera instancia instalaremos un wordpress en un servidor nginx con certificado SSL y una base de datos mariadb.
Para esto utilizaremos el archivo docker-compose ubicado en la carpeta /docker/ de nuestro repositorio, este documento tiene derechos reservados al usuario de github jmlcas, su repositorio se encuentra en la bibliografía __es importante tener en cuenta que debes modificar el archivo docker-compose.yml para definir tu dominio__.

Considerando que este proyecto esta pensado en un entorno de Google Cloud para los pasos que se detallarán a continuación, necesitaremos una maquina virtual con Ubuntu, permitiendo trafico HTTP y HTTPS
#### Pasos:
1) Primero actualizamos e instalamos paquetes necesarios para la instalación con docker-compose, en la consola poner los siguientes comandos:
```
# Para la obtención de paquetes de Docker
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose unzip -y
```

2) Si todo va bien podemos continuar, ahora obtendremos nuestro archivo desde la maquina virtual con el siguiente comando:
```
cd /home/
sudo wget https://github.com/Caarloh/sysadmin2y3/archive/main.zip
```
3. Con lo anterior tendriamos un zip llamado main.zip en nuestro directorio home, lo descomprimiremos y ejecutaremos:
```
sudo unzip main.zip
sudo mv /sysadmin2y3-main/docker/ /home/
cd docker
```

3. a. Este es el momento que podrías editar el archivo docker-compose con tu dominio y las variables de entorno en .env
```
# Para editar docker-compose
sudo nano docker-compose.yml
# Para editar variables de entorno
sudo nano .env
```
  
4. Ahora levantamos nuestro servicio con:
```
sudo docker-compose up -d
```
5. Tenemos arriba nuestro servicio con certificado SSL, visita abuelo.pintocruces.cl ^^

  ## Biblografía
***
Lista de recursos de este proyecto:
* [docker installation](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
* [docker-compose.yml](https://github.com/jmlcas/Docker-WordPress-SSL/tree/main)