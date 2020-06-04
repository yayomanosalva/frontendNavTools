# SPA ANGULAR

==================== ---	Install new project & structure	--- ====================

- ng new spa

- route => yes

- style => scss

  ==================== ---			components				--- ====================

- ng g c components/shared/navbar -is - -skipTests

- ng g c components/home -is –skipTests

- ng g c components/about -is –skipTests

- ng g c components/heroes -is –skipTests

  ==================== ---		Install bootstrap				--- ====================

- npm install jquery -–save

- npm install @popperjs/core

- npm install bootstrap

- npm install bootswatch

  ==================== ---		File:  Angular.json			--- ====================

```json
"styles": ["src/styles.css","node_modules/bootstrap/dist/css/bootstrap.min.css"],
"scripts": ["node_modules/jquery/dist/jquery.min.js",
         "node_modules/@popperjs/core/dist/umd/popper.min.js",
         "node_modules/bootstrap/dist/js/bootstrap.min.js"]
```

## RUTAS 

==================== ---	File:  app.routing.modules.ts		--- ====================

```typescript
const routes: Routes = [
 { path: 'home', component: HomeComponent },
 { path: 'precios', component: PreciosComponent },
 { path: 'compartida', component: CompartidaComponent },
 { path: 'protegida', component: ProtegidaComponent },
 { path: '****', pathMatch: 'full', redirectTo: 'home' },
];
```

==================== ---	File:  navbar.component.html		--- ====================

```html
<ul class="navbar-nav mr-auto">
    <li class="nav-item" routerLinkActive="active">
        <a class="nav-link" routerLink='/home'>Home <span class="sr-only">(current)</span></a>
    </li>
    <li class="nav-item" routerLinkActive="active">
        <a class="nav-link" routerLink='/precios'>precios</a>
    </li>
    <li class="nav-item" routerLinkActive="active">
        <a class="nav-link" routerLink='/protegida'>protegida</a>
    </li>
</ul>
```



```
ng g c components/fileUpload --`module=app.module`
```



#### ==================== ---						service								--- ====================

ng g s services/auth  --skipTests

/////////    ng g s services/producto --module=app.module

==================== ---					guard						--- ====================

ng g guard services/auth  --skipTests

> CanActivate

```typescript
{ path: 'compartida', component: CompartidaComponent, canActivate: [AuthGuard]},
```

#### ==================== ---					interfaces						--- ====================

ng g i interfaces/img interface
ng g i interfaces/producto interface
