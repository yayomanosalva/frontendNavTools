# Login Angular Firebase

### Install new project

- ng new login-angular9-firebase
- route => yes
- style => scss

### Install dependency

- npm install bootstrap jquery @popperjs/core
- npm install bootswatch

### File Angular.json

```
"styles": ["src/styles.css","node_modules/bootstrap/dist/css/bootstrap.min.css"],
"scripts": ["node_modules/jquery/dist/jquery.min.js",
         "node_modules/@popperjs/core/dist/umd/popper.min.js",
         "node_modules/bootstrap/dist/js/bootstrap.min.js"]
```

## create components

###### Create components del navbar - home page - login - register

generate modulo & component home

```
ng g m home -m=app --route home
ng g c shared/navbar
```

generate authenticate de users

```
ng g m auth/login -m=app --route login
```

generate register

```
ng g m auth/register -m=app --route register
ng add @angular/fire
npm i firebase
```

