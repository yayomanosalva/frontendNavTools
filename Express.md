## PASOS PARA PROYECTO EXPRESS
## Jair Manosalva
### Getting started
# step for project express

# express js

1. npm install -g express
```bash
instala de forma gloal
```
1. npm install -g express-generator

  ```bash
  genera la estructura del proyecto
  ```
1. express --ejs name-project

  ```bash
  tareas
  ```
1. npm install
1. npm install --save mongoose
```bash
libreria que modela los objetos
```
1. mkdir models
1. npm install --save-dev pm2
```bash
Crear un archivo como pm2.json en la raiz del projecto
{
    "apps": [{
        "name" : "CLIENT",
        "script" : "./src/app.js",
        "port": "3333",
        "watch": "./src",
        "ignore_watch": ["./src/stylus", "./src/public"],
        "watch_options": {
            "usePolling": true
        },
        "error_file": "./logs/app-error.log",
        "out_file": "./logs/app-out.log",
        "env": {
            "NODE_ENV": "development"
        }
    }]
}
```
1. mkdir src
```bash
Insertar en src -->
public
routes
views
app.js
```
1. modidicar app.js
```bash
Agragamos antes de module.exports = app;
  if (!module.parent) {
      app.listen(3333);
  }

```
1. pm2 start pm2.json
```bash
arranca el servidor
```
## Resumen
```bash
$> npm install -g express
$> npm install -g express-generator
$> express --ejs name-project
$> npm install
$> npm install --save mongoose
$> mkdir models
$> pm2 start pm2.json
```
