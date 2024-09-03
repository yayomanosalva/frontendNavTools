# **`ngModel`**
En Angular, `ngModel` es una directiva que se utiliza para crear una unión bidireccional entre los datos del componente y los elementos del formulario en la vista. Esto significa que los cambios en el formulario se reflejan automáticamente en el modelo del componente y viceversa. Es una parte clave del sistema de formularios de Angular y facilita la creación de formularios interactivos.

### **Explicación de `ngModel`**

- **Binding Bidireccional**: `ngModel` permite la vinculación bidireccional de datos entre el componente y la vista. Cualquier cambio en el input del usuario se refleja inmediatamente en el modelo del componente, y cualquier cambio en el modelo también se refleja en la vista.
- **Uso en Formularios**: `ngModel` es especialmente útil en formularios para capturar y validar datos de entrada del usuario.
- **Requisitos**: Para usar `ngModel`, necesitas importar el módulo `FormsModule` en tu módulo de Angular.

### **Ejemplo de Uso de `ngModel`**

Vamos a ver un ejemplo básico para entender cómo funciona `ngModel`.

1. **Paso 1: Importa `FormsModule`**

   Asegúrate de importar `FormsModule` en el módulo donde utilizarás `ngModel`. Por ejemplo, en `app.module.ts`:

   ```typescript
   import { NgModule } from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { FormsModule } from '@angular/forms'; // Importa FormsModule

   import { AppComponent } from './app.component';

   @NgModule({
     declarations: [
       AppComponent
     ],
     imports: [
       BrowserModule,
       FormsModule // Añade FormsModule a los imports
     ],
     providers: [],
     bootstrap: [AppComponent]
   })
   export class AppModule { }
   ```

2. **Paso 2: Usa `ngModel` en el Componente**

   A continuación, utiliza `ngModel` en el template del componente para realizar el binding bidireccional. Por ejemplo, en `app.component.ts` y `app.component.html`:

   **app.component.ts**:
   ```typescript
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-root',
     templateUrl: './app.component.html',
     styleUrls: ['./app.component.css']
   })
   export class AppComponent {
     // Define una propiedad que será vinculada
     userName: string = '';
   }
   ```

   **app.component.html**:
   ```html
   <div>
     <label for="name">Name:</label>
     <input id="name" [(ngModel)]="userName" placeholder="Enter your name">
   </div>
   <div>
     <p>Hello, {{ userName }}!</p>
   </div>
   ```

### **Explicación del Ejemplo**

- **Binding Bidireccional**: En el ejemplo, `[(ngModel)]="userName"` en el campo de entrada vincula el valor del campo con la propiedad `userName` del componente. Esto significa que cualquier cambio en el campo de entrada actualizará automáticamente la propiedad `userName` y cualquier cambio en `userName` se reflejará en el campo de entrada.
- **Visualización en Tiempo Real**: El párrafo `<p>Hello, {{ userName }}!</p>` muestra un saludo que se actualiza en tiempo real a medida que el usuario escribe en el campo de entrada.

### **Conclusión**

`ngModel` simplifica la gestión de formularios al proporcionar una forma sencilla de vincular datos entre el modelo y la vista. Facilita la captura y visualización de datos del usuario, así como la validación y manipulación de formularios en Angular.

<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# **`EventEmitter Eventos`**


En Angular, los eventos personalizados (custom events) son una manera de comunicar un componente hijo con su componente padre. Son útiles cuando un componente hijo necesita informar al componente padre sobre ciertas acciones o cambios, que no se pueden gestionar directamente a través de la vinculación de datos.

### **Explicación de Eventos Personalizados**

- **Emisión de Eventos**: Los eventos personalizados se emiten desde el componente hijo utilizando el `@Output` y un objeto `EventEmitter`.
- **Manejo de Eventos**: El componente padre escucha estos eventos y responde a ellos de acuerdo a la lógica definida.
- **Comunicación de Componentes**: Facilitan la comunicación entre componentes sin necesidad de pasar datos a través de múltiples niveles de la jerarquía de componentes.

### **Ejemplo de Eventos Personalizados**

Vamos a crear un ejemplo simple en el que un componente hijo emite un evento cuando se hace clic en un botón, y el componente padre maneja ese evento.

1. **Paso 1: Crear el Componente Hijo**

   **child.component.ts**:
   ```typescript
   import { Component, EventEmitter, Output } from '@angular/core';

   @Component({
     selector: 'app-child',
     templateUrl: './child.component.html',
     styleUrls: ['./child.component.css']
   })
   export class ChildComponent {
     // Define el EventEmitter
     @Output() notify: EventEmitter<string> = new EventEmitter<string>();

     // Método para emitir el evento
     sendNotification() {
       this.notify.emit('Hello from child!');
     }
   }
   ```

   **child.component.html**:
   ```html
   <button (click)="sendNotification()">Send Notification</button>
   ```

   En este componente hijo, `@Output` se utiliza para definir un `EventEmitter` llamado `notify`. El método `sendNotification` emite un evento con un mensaje cuando el botón es clicado.

2. **Paso 2: Crear el Componente Padre**

   **parent.component.ts**:
   ```typescript
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-parent',
     templateUrl: './parent.component.html',
     styleUrls: ['./parent.component.css']
   })
   export class ParentComponent {
     // Método para manejar el evento emitido por el componente hijo
     handleNotification(message: string) {
       console.log(message);
     }
   }
   ```

   **parent.component.html**:
   ```html
   <app-child (notify)="handleNotification($event)"></app-child>
   ```

   En el componente padre, el método `handleNotification` recibe el mensaje del evento emitido por el componente hijo. En el template, el componente hijo (`app-child`) es utilizado con el evento `notify` enlazado al método `handleNotification`.

### **Explicación del Ejemplo**

- **Emisión del Evento**: En el componente hijo (`ChildComponent`), el evento se emite cuando se hace clic en el botón. La llamada a `this.notify.emit('Hello from child!')` envía el mensaje al componente padre.
- **Manejo del Evento**: En el componente padre (`ParentComponent`), el evento se escucha con `(notify)="handleNotification($event)"`. Cuando el evento es recibido, se ejecuta el método `handleNotification`, que en este caso simplemente imprime el mensaje en la consola.

### **Conclusión**

Los eventos personalizados son una herramienta poderosa para la comunicación entre componentes en Angular. Permiten una interacción flexible y mantienen una separación clara de responsabilidades entre los componentes. Este enfoque es especialmente útil en aplicaciones más grandes donde los componentes tienen que trabajar juntos de manera coordinada.

<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# **`Reactive forms`**

Los formularios reactivos en Angular ofrecen una manera más robusta y programática de manejar formularios en comparación con los formularios basados en plantillas (template-driven forms). Se basan en el uso de objetos `FormGroup` y `FormControl`, permitiendo una mayor flexibilidad y control sobre el formulario.

### **Explicación de Formularios Reactivos**

- **Control y Validación Programática**: Los formularios reactivos permiten la configuración dinámica y validación programática del formulario en el componente TypeScript.
- **Estructura**: Utilizan instancias de `FormGroup` para agrupar controles (`FormControl`) y `FormArray` para manejar colecciones de controles.
- **Sincronización**: Los cambios en el modelo de datos se reflejan en la vista y viceversa, con validaciones y lógica de presentación manejadas en el código del componente.

### **Ejemplo de Formularios Reactivos**

Vamos a crear un formulario reactivo básico con Angular para mostrar cómo se configuran y manejan los formularios reactivos.

1. **Paso 1: Importar `ReactiveFormsModule`**

   Asegúrate de importar `ReactiveFormsModule` en el módulo de tu aplicación:

   **app.module.ts**:
   ```typescript
   import { NgModule } from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { ReactiveFormsModule } from '@angular/forms'; // Importa ReactiveFormsModule

   import { AppComponent } from './app.component';
   import { MyFormComponent } from './my-form/my-form.component'; // Suponiendo que tienes un componente para el formulario

   @NgModule({
     declarations: [
       AppComponent,
       MyFormComponent
     ],
     imports: [
       BrowserModule,
       ReactiveFormsModule // Añade ReactiveFormsModule a los imports
     ],
     providers: [],
     bootstrap: [AppComponent]
   })
   export class AppModule { }
   ```

2. **Paso 2: Configurar el Componente con el Formulario Reactivo**

   **my-form.component.ts**:
   ```typescript
   import { Component } from '@angular/core';
   import { FormBuilder, FormGroup, Validators } from '@angular/forms';

   @Component({
     selector: 'app-my-form',
     templateUrl: './my-form.component.html',
     styleUrls: ['./my-form.component.css']
   })
   export class MyFormComponent {
     // Define el FormGroup
     myForm: FormGroup;

     constructor(private fb: FormBuilder) {
       // Inicializa el formulario con validadores
       this.myForm = this.fb.group({
         name: ['', Validators.required],
         email: ['', [Validators.required, Validators.email]],
         age: ['', Validators.pattern('^[0-9]+$')]
       });
     }

     // Método para manejar el envío del formulario
     onSubmit() {
       if (this.myForm.valid) {
         console.log(this.myForm.value);
       } else {
         console.log('Formulario inválido');
       }
     }
   }
   ```

   **my-form.component.html**:
   ```html
   <form [formGroup]="myForm" (ngSubmit)="onSubmit()">
     <div>
       <label for="name">Name:</label>
       <input id="name" formControlName="name">
       <div *ngIf="myForm.get('name').invalid && myForm.get('name').touched">
         Name is required
       </div>
     </div>
     
     <div>
       <label for="email">Email:</label>
       <input id="email" formControlName="email">
       <div *ngIf="myForm.get('email').invalid && myForm.get('email').touched">
         <div *ngIf="myForm.get('email').errors?.required">Email is required</div>
         <div *ngIf="myForm.get('email').errors?.email">Invalid email format</div>
       </div>
     </div>
     
     <div>
       <label for="age">Age:</label>
       <input id="age" formControlName="age">
       <div *ngIf="myForm.get('age').invalid && myForm.get('age').touched">
         <div *ngIf="myForm.get('age').errors?.pattern">Age must be a number</div>
       </div>
     </div>
     
     <button type="submit">Submit</button>
   </form>
   ```

### **Explicación del Ejemplo**

- **Definición del Formulario**: En el componente TypeScript (`MyFormComponent`), se crea un formulario reactivo utilizando `FormBuilder`. Se definen controles (`name`, `email`, `age`) con sus respectivos validadores.
- **Template del Formulario**: En el HTML (`my-form.component.html`), el formulario se vincula al objeto `FormGroup` usando `[formGroup]`, y cada campo se vincula a un control con `formControlName`.
- **Validaciones**: Se muestran mensajes de error si los campos son inválidos y han sido tocados.
- **Manejo de Envíos**: El método `onSubmit` se ejecuta cuando el formulario se envía, validando y mostrando los valores si el formulario es válido.

### **Conclusión**

Los formularios reactivos en Angular proporcionan un enfoque más flexible y programático para manejar formularios, facilitando la gestión de validaciones y lógica compleja. Son ideales para aplicaciones que requieren formularios dinámicos y complejos.

<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# **Componentes y Directivas**

- **Componentes**: Son la base de cualquier aplicación Angular. Cada componente tiene una clase que maneja los datos y la lógica, y una plantilla que define la vista. Los componentes se definen con el decorador `@Component`.
- **Directivas**: Son clases que pueden modificar el comportamiento o el aspecto de elementos en el DOM. Hay tres tipos principales:
  - **Directivas estructurales**: Cambian la estructura del DOM (`*ngIf`, `*ngFor`).
  - **Directivas de atributo**: Cambian el aspecto o comportamiento de un elemento (`ngClass`, `ngStyle`).
  - **Componentes**: Técnicamente, los componentes son directivas con una plantilla asociada.

### Decoradores Importantes

- **@ViewChild**: Permite acceder a un elemento hijo del DOM o a una directiva desde el componente padre. Se usa para manipular elementos después de que se hayan renderizado.

  ```typescript
  @ViewChild('containerTitle') contenedorRef!: ElementRef;
  ngAfterViewInit() {
    console.log(this.element.nativeElement);
  }
  ```

  ```html
  <div #containerTitle>
    <p>title works!</p>
  </div>
  ```

- **@Input**: Permite que un componente hijo reciba datos desde su componente padre.

  ```typescript
  @Input() data: string;
  ```

<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
# **Ciclos de Vida de los Componentes**

Angular proporciona varios hooks que permiten ejecutar código en diferentes momentos del ciclo de vida de un componente:

- **ngOnChanges**: Se llama cuando una propiedad enlazada a datos cambia.

  ```typescript
  ngOnChanges(changes: SimpleChanges) {
    console.log(changes);
  }
  ```
- **ngAfterViewInit**: Se llama después de que la vista del componente y sus vistas hijas se hayan inicializado.

  ```typescript
  ngAfterViewInit() {
    console.log('Vista inicializada');
    console.log('contenedorRef >>> ', this.contenedorRef)
  }
  ```

- **ngOnInit**: Se ejecuta después de la inicialización del componente y es ideal para inicializar propiedades.

  ```typescript
     ngOnInit(): void {
    console.log("<< Hello from ngOnInit >>")
  }
  ```
- **ngDoCheck**: Permite la detección personalizada de cambios.

  ```typescript

  ```

- **ngAfterContentInit**: Se ejecuta después de que el contenido del componente se haya inicializado.

  ```typescript

  ```

- **ngAfterContentChecked**:  Se ejecuta después de que el contenido del componente se haya revisado.

  ```typescript

  ```

- **ngAfterViewChecked**:  Se ejecuta después de que la vista del componente y sus vistas hijas se hayan revisado.

  ```typescript

  ```

- **ngOnDestroy**: Se llama justo antes de que Angular destruya el componente. Útil para limpiar suscripciones y liberar recursos.

  ```typescript
  ngOnDestroy() {
    console.log('Componente destruido');
  }
  ```
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# **interceptor**

los interceptores son una herramienta poderosa que se utilizan para interceptar y manipular las solicitudes HTTP y las respuestas antes de que lleguen a su destino o antes de que sean procesadas por el código que las maneja. Esto te permite, por ejemplo, añadir encabezados a las solicitudes, manejar errores globalmente o realizar transformaciones en los datos.

### ¿Qué es un interceptor?

Un interceptor es una clase que implementa la interfaz `HttpInterceptor` proporcionada por Angular. Esta interfaz define un método `intercept` que debes implementar. El método `intercept` toma dos argumentos:

1. **`HttpRequest`**: Representa la solicitud HTTP que está siendo realizada.
2. **`HttpHandler`**: Utilizado para enviar la solicitud HTTP y obtener una respuesta.

### Ejemplo básico de un interceptor

Vamos a crear un interceptor que añada un encabezado de autorización a todas las solicitudes salientes. Aquí están los pasos:

1. **Crear el interceptor**:

   Primero, crea un nuevo archivo para el interceptor, por ejemplo `auth.interceptor.ts`.

   ```typescript
   import { Injectable } from '@angular/core';
   import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
   import { Observable } from 'rxjs';

   @Injectable()
   export class AuthInterceptor implements HttpInterceptor {
     intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
       // Clonar la solicitud para añadir el nuevo encabezado
       const authReq = req.clone({
         setHeaders: {
           Authorization: `Bearer your-auth-token-here`
         }
       });

       // Pasar la solicitud clonada al siguiente manejador
       return next.handle(authReq);
     }
   }
   ```

   En este ejemplo, estamos clonando la solicitud original (`req`) y añadiendo un encabezado `Authorization`. Luego, pasamos la solicitud clonada al siguiente manejador (`next.handle(authReq)`).

2. **Registrar el interceptor**:

   Después, debes registrar el interceptor en el módulo de tu aplicación (`app.module.ts`).

   ```typescript
   import { NgModule } from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
   import { AppComponent } from './app.component';
   import { AuthInterceptor } from './auth.interceptor'; // Asegúrate de importar el interceptor

   @NgModule({
     declarations: [
       AppComponent
     ],
     imports: [
       BrowserModule,
       HttpClientModule
     ],
     providers: [
       {
         provide: HTTP_INTERCEPTORS,
         useClass: AuthInterceptor,
         multi: true
       }
     ],
     bootstrap: [AppComponent]
   })
   export class AppModule { }
   ```

   En este paso, estamos diciendo a Angular que el `AuthInterceptor` debe ser utilizado para interceptar las solicitudes HTTP. La opción `multi: true` indica que puede haber múltiples interceptores y que Angular debe acumularlos en lugar de reemplazarlos.

### Conclusión

Los interceptores son útiles para gestionar tareas comunes relacionadas con las solicitudes y respuestas HTTP, como agregar tokens de autenticación, manejar errores globalmente, o modificar las respuestas. Este patrón ayuda a mantener el código más limpio y modular, centralizando la lógica común relacionada con las solicitudes HTTP.
