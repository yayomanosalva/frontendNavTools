#Reduce

```typescript
export interface Task {
	nombre:string,
	prioridad:string;
}

const tareas = [
			{ nombre: 'Cargar Móvil', prioridad: 'A' },
			{ nombre: 'Comprar el pan', prioridad: 'B' },
			{ nombre: 'Enviar email', prioridad: 'A' },
			{ nombre: 'Pintar la sala', prioridad: 'C' },
			{ nombre: 'Limpiar el abanico', prioridad: 'B' },
			{ nombre: 'Lavar la ropa', prioridad: 'A' },
			{ nombre: 'ordenar la sala', prioridad: 'C' },
		];
		const final = tareas.reduce((obj, task: Task) => {
			console.log({ task });
			if (!obj[task.prioridad]) {
				obj[task.prioridad] = [];
			}

			obj[task.prioridad].push(task.nombre);
			return obj;

		}, {});

		console.log("object -->> ", {final});
```
