# SPA ANGULAR

==================== --- Install new project & structure --- ====================

```bash
ng new spa 
```

- route => yes

- style => scss

  ==================== --- components --- ====================

  ```bash
  ng g c components/shared/navbar --skipTests=true
  ng g c components/home –-skipTests=true
  ng g c components/about --skipTests=true
  ng g c components/heroes --skipTests=true
  ```

  ==================== --- generate model class --- ====================

  ```bash
  ng generate class hero --type=model
  ```

  ==================== --- Install bootstrap --- ====================

  ```bash
  npm install jquery -–save
  npm install @popperjs/core
  npm install bootstrap
  npm install bootswatch
  ```

  ==================== --- File: Angular.json --- ====================

```html
"styles": ["src/styles.css","node_modules/bootstrap/dist/css/bootstrap.min.css"],
"scripts": ["node_modules/jquery/dist/jquery.min.js",
         "node_modules/@popperjs/core/dist/umd/popper.min.js",
         "node_modules/bootstrap/dist/js/bootstrap.min.js"]
```

## RUTAS

```bash
ng new {Project-name} --routing=true
```

==================== --- File: app.routing.modules.ts --- ====================

```typescript
const routes: Routes = [
 { path: 'home', component: HomeComponent },
 { path: 'precios', component: PreciosComponent },
 { path: 'compartida', component: CompartidaComponent },
 { path: 'protegida', component: ProtegidaComponent },
 { path: '**', pathMatch: 'full', redirectTo: 'home' },
];
```

#### ==================== --- File: index.html

```html
<router-oulet></router-oulet>
```

#### ==================== --- File: app.module.ts

```typescript
import { FormsModule } from "@angular/forms";

imports: [BrowserModule, AppRoutingModule, FormsModule],
```

#### ==================== --- File: navbar.component.html

```html
<ul class="navbar-nav mr-auto">
    <li class="nav-item" routerLinkActive="active">
        <a class="nav-link" routerLink='/home'>Home <span class="sr-only">(current)</span></a>
    </li>
    <li class="nav-item" routerLinkActive="active">
        <a class="nav-link" routerLink='/precios'>precios</a>
    </li>
    <li class="nav-item" routerLinkActive="active">
        <a class="nav-link" routerLink='/protegida'>protegida</a>
    </li>
</ul>
ng g c components/fileUpload --`module=app.module`
```

#### ==================== --- service --- ====================

```bash
ng g s services/auth --skipTests
```

///////// ng g s services/producto --module=app.module

#### ==================== --- guard --- ====================

```bash
ng g guard guards/auth --skipTest
```

> CanActivate

```
{ path: 'compartida', component: CompartidaComponent, canActivate: [AuthGuard]},
```

#### ==================== --- interfaces --- ====================

```bash
ng g i interfaces/img interface ng g i interfaces/producto interface
```



![img](https://i.stack.imgur.com/WczZ8.png)



# 	================== Login ==================

```bash
ng new ng-login --routing
```

## creamos las paginas de las rutas

```bash
ng g c pages/home
ng g c pages/login
ng g c pages/registro
```

## crear modelo para el manejo de usuarios

#### > create class usuario

```bash
ng g class  models/usuario --type=model
```

#### > usuario.model.ts

```typescript
export class Usuario {
    email:string;
    password:string;
    nombre:string;
}
```

## Conectar el formulario de registro con una instancia del modelo de usuario

se agrega [(ngModel)]="usuario.email" al input

```html
<form (ngSubmit)="onSubmit()" class="login100-form validate-form flex-sb flex-w">
<input class="input100" type="text" name="email" [(ngModel)]="usuario.email"                    placeholder="Email">
```

en el component.ts se instancia el modelo y se crea el metodo onSubmit que recibe la data de la vista

```typescript
export class RegistroComponent implements OnInit {
  usuario: UsuarioModel;	//propiedad tipo modelo 
  constructor() { }
  ngOnInit(): void {
    this.usuario = new UsuarioModel(); //instancia el modelo de la clase models/usuario.model.ts
    this.usuario.email = "yayomanosalva@gmail.com";
  }
    //metodo que recibe la data de el input
  onSubmit(){
    console.log("Enviando mensaje");
    console.log(this.usuario);
  }
}
```

## Validar informacion antes de enviar a un servidor

se valida el formulario los campor requeridos y una directiva email de angular

```html
<input class="input100" type="text" name="email" [(ngModel)]="usuario.email"
                           required email placeholder="Email">
```

se envia como parametro un identificador que hace referencia al formulario es de tipo ngForm(template)

```html
<form (ngSubmit)="onSubmit(f)" #f="ngForm" class="login100-form validate-form flex-sb flex-w">
```

## Mostrar Errores por pantalla

antes del input en un span va un ngIf validando al ngForm del identificador

```html
<span *ngIf="f.submitted && f.controls['password'].errors"
                 class="text-danger animated fadeIn">La contraseña debe de ser más de 6 letras</span>
```

## Servicios REST

importamos la biblioteca HttpClientModule en app.module.ts

#### ==================== --- File: app.module.ts

```tsx
import { HttpClientModule } from '@angular/common/http';

imports: [BrowserModule, AppRoutingModule, FormsModule, HttpClientModule],
```

creamos un servicio para manejo de la autenticación

```
ng g s services/auth
```

#### ==================== --- File: auth.services.ts

```tsx
import { UsuarioModel } from './../models/usuario.model';
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

import { observable, Observable, throwError } from 'rxjs';

@Injectable({
  providedIn: 'root'
})

  // crear nuevos usuarios
  // https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=[API_KEY]

  // Login
  // https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=[API_KEY]

export class AuthService {

  private urlApi = 'https://identitytoolkit.googleapis.com/v1';
  private apiKey = 'AIzaSyARA4_5dAaStoY3kBubjlUpnVhtD2Imf1U';

  constructor(private http: HttpClient) { }

  logout() { }

  login(usuario: UsuarioModel): Observable<any>{
    const authData = {
      ...usuario,
      returnSecureToken: true
    };

    return this.http.post(
      `${this.urlApi}/accounts:signInWithPassword?key=${this.apiKey}`, authData
    );
  }

  nuevoUsuario( usuario: UsuarioModel ): Observable<any>{
    // const authData = {
    //   email:usuario.email,
    //   password:usuario.password,
    //   returnSecureToken:usuario.returnSecureToken,
    // }

    const authData = {
      ...usuario, returnSecureToken: true
    };

    return this.http.post(
       `${ this.urlApi }/accounts:signUp?key=${ this.apiKey }`, authData
     );
  }
}
```

#### ==================== --- File: registro.component.ts

```tsx
import { Component, OnInit } from '@angular/core';
import { NgForm } from '@angular/forms';
import { Observable } from 'rxjs';
import { UsuarioModel } from 'src/app/models/usuario.model';
import { AuthService } from 'src/app/services/auth.service';

@Component({
  selector: 'app-registro',
  templateUrl: './registro.component.html',
  styleUrls: ['./registro.component.css']
})
export class RegistroComponent implements OnInit {

  usuario: UsuarioModel;

  constructor(private auth: AuthService) { }

  ngOnInit(): void {
    this.usuario = new UsuarioModel();
   }

  onSubmit( form: NgForm ): Observable<any>{
    if ( form.invalid ) { return; }

    // console.log('Enviando mensaje');
    // console.log(this.usuario);
    // console.log(form);

    this.auth.nuevoUsuario(this.usuario)
    .subscribe( resp => {
      console.log('resp register --> ', resp );
    }, (err) => console.log('err --> ', err.error.error.message));
  }
}
```

#### ==================== --- File: login.component.ts

```tsx
import { Component, OnInit } from '@angular/core';
import { NgForm } from '@angular/forms';
import { Observable } from 'rxjs';
import { UsuarioModel } from 'src/app/models/usuario.model';
import { AuthService } from 'src/app/services/auth.service';

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.css']
})
export class LoginComponent implements OnInit {

  usuario: UsuarioModel = new UsuarioModel();

  constructor(private auth: AuthService) { }

  ngOnInit(): void {
  }

  login( form: NgForm ): Observable<any>{
    if (form.invalid) { return; }
    // console.log('Imprimir si el formulario es valido');
    // console.log(this.usuario);
    // console.log(form);

    this.auth.login(this.usuario)
    .subscribe((resp) => {
      console.log('resp login ==>', resp);
    }, (err) => console.log('err --> ', err.error.error.message));
  }
}
```
