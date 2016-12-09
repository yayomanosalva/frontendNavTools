# Express.js
Express.js está basado en Connect, que es un framework extensible de manejo de servidores HTTP, el cual provee plugins de alto rendimiento conocidos como middleware.

Middleware es un software que asiste a una aplicación para interactuar o comunicarse con otras aplicaciones, software, redes, hardware y/o sistemas operativos.

### Instalar Express.js

Vamos a instalar expres.js de manera global en nuestro sistema:
```sh
sudo npm install -g express
```
![N|Solid](https://geekytheory.com/wp-content/uploads/2013/08/Terminal_040.png)

### La primera aplicación

Algo curioso, es que podremos crear una aplicación rápidamente con express.js y ejecutarla al momento. Esta aplicación, como era de esperar, es extremadamente básica. Cuando creemos el proyecto, tendremos que instalar las dependencias necesarias para poder ejecutarlo. Haremos esto de la siguiente manera:

```sh
express node_app
```
A continuación, entraremos en el directorio de la aplicación que acabamos de crear e instalamos las dependencias:

```sh
cd node_app && npm install
```
![N|Solid](https://geekytheory.com/wp-content/uploads/2013/08/Terminal_041.png)

comando:
```sh
node app.js
```
![N|Solid](https://geekytheory.com/wp-content/uploads/2013/08/Selection_042-600x266.png)

### Aplicación ejemplo:

Primero, importaremos el módulo express.js. Tras esto, crearemos una variable 'app' y, definiremos que cuando reciba la ruta '/', mande un mensaje. Por otra parte, cuando reciba la ruta '/prueba', mandará otro mensaje distinto. Ejecutaremos node.js en el puerto 8080, como solemos hacer en estos tutoriales.

`
var express = require("express"); var app = express(); app.get('/', function(req, res) { res.send('Geeky Theory probando express.js'); }); app.get('/prueba', function(req, res) { res.send('Geeky Theory probando express.js en /prueba'); }
`

![N|Solid](https://geekytheory.com/wp-content/uploads/2013/08/Selection_043-600x230.png)
