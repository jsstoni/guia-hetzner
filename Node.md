# Instalar Node.js y configurar la aplicación

Después de haber configurado Nginx, puedes agregar una sección para instalar Node.js en el servidor y ejecutar tu aplicación:

#### Instalar Node.js

Conéctate al servidor si no lo has hecho:
```bash
ssh root@PUBLIC_IP
```

Instala Node.js utilizando el repositorio oficial:

* instala nvm (node version manager)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
```
* Descarga eh instala node.js
```bash
nvm install 20
```
* verifica que la versión correcta de Node.js esté en el entorno
```bash
node -v
```
  debería imprimir `v20.18.0`
* verifica que la versión correcta de npm esté en el entorno
```bash
npm -v
```
  debería imprimir `10.8.2`

## Subir y configurar tu aplicación
#### No en todos los servidores vienen con git instalado por defecto

puedes instalar Git con el siguiente comando:
```bash
sudo apt update
sudo apt install git
```

Después de la instalación, puedes verificar que Git está correctamente instalado ejecutando:
```bash
git --version
```

Sube tu aplicación al servidor. Puedes hacerlo usando Git o copiando los archivos directamente:
#### Opción 1: Usando Git:
```bash
git clone https://github.com/tu-usuario/tu-repositorio.git
cd tu-repositorio
```
#### Opción 2: Usando SCP desde tu máquina local:
```bash
scp -r /ruta/local/a/tu/app root@PUBLIC_IP:/ruta/en/servidor
```

Instala las dependencias de tu aplicación:
```bash
npm install
```

Prueba tu aplicación ejecutándola: `node server.js`

Si todo funciona correctamente, puedes continuar configurando PM2 (o cualquier otra alternativa) para que la aplicación siga corriendo en segundo plano.

## Configurar PM2 para mantener la aplicación en ejecución

Como hablamos antes de PM2, podrías incluir una sección para instalarlo y configurarlo para que la aplicación se mantenga ejecutándose en segundo plano, incluso después de cerrar la sesión SSH.

Instalar PM2
```bash
npm install pm2 -g
```

Ejecuta tu aplicación con PM2
```bash
pm2 start server.js
```

Puedes configurar PM2 para que inicie automáticamente con el servidor:
```bash
pm2 startup
```

Guarda la lista de procesos de PM2 para que se reinicien automáticamente después de un reinicio del servidor:
```bash
pm2 save
```
Pronto: [Despliegue continuo]()
