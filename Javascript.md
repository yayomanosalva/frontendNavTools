1. **filter()**: Crea un nuevo array con todos los elementos que pasen la prueba implementada por la función proporcionada.
    ```javascript
    const numeros = [1, 2, 3, 4, 5];
    const pares = numeros.filter(num => num % 2 === 0);
    console.log(pares); // [2, 4]
    ```

2. **Plantillas literales**: Permiten incrustar expresiones en cadenas de texto. Se crean usando comillas invertidas (` `).
    ```javascript
    const nombre = 'Juan';
    const saludo = `Hola, ${nombre}!`;
    console.log(saludo); // "Hola, Juan!"
    ```

3. **findIndex()**: Devuelve el índice del primer elemento de un array que cumpla con la función proporcionada. Si no se encuentra, devuelve -1.
    ```javascript
    const frutas = ['manzana', 'banana', 'cereza'];
    const indice = frutas.findIndex(fruta => fruta === 'banana');
    console.log(indice); // 1
    ```

4. **sort()**: Ordena los elementos de un array en su lugar y devuelve el array.
    ```javascript
    const letras = ['d', 'b', 'a', 'c'];
    letras.sort();
    console.log(letras); // ['a', 'b', 'c', 'd']
    ```

5. **Objetos**: Estructuras de datos que almacenan datos en forma de pares clave-valor.
    ```javascript
    const persona = {
        nombre: 'Ana',
        edad: 25,
        ciudad: 'Barranquilla'
    };
    console.log(persona.nombre); // "Ana"
    ```

6. **push()**: Añade uno o más elementos al final de un array y devuelve la nueva longitud del array.
    ```javascript
    const array = [1, 2, 3];
    array.push(4);
    console.log(array); // [1, 2, 3, 4]
    ```

7. **pop()**: Elimina el último elemento de un array y lo devuelve.
    ```javascript
    const array = [1, 2, 3];
    const ultimo = array.pop();
    console.log(array); // [1, 2]
    console.log(ultimo); // 3
    ```

8. **shift()**: Elimina el primer elemento de un array y lo devuelve.
    ```javascript
    const array = [1, 2, 3];
    const primero = array.shift();
    console.log(array); // [2, 3]
    console.log(primero); // 1
    ```

9. **unshift()**: Añade uno o más elementos al inicio de un array y devuelve la nueva longitud del array.
    ```javascript
    const array = [1, 2, 3];
    array.unshift(0);
    console.log(array); // [0, 1, 2, 3]
    ```

10. **trim()**: Elimina los espacios en blanco de ambos extremos de una cadena.
    ```javascript
    const cadena = '  Hola Mundo  ';
    console.log(cadena.trim()); // 'Hola Mundo'
    ```

11. **indexOf()**: Devuelve el primer índice en el que se puede encontrar un elemento dado en el array, o -1 si el elemento no se encuentra.
    ```javascript
    const array = [1, 2, 3, 4];
    console.log(array.indexOf(3)); // 2
    ```

12. **slice()**: Devuelve una copia superficial de una porción de un array dentro de un nuevo array.
    ```javascript
    const array = [1, 2, 3, 4];
    const nuevoArray = array.slice(1, 3);
    console.log(nuevoArray); // [2, 3]
    ```

13. **replace()**: Devuelve una nueva cadena con algunas o todas las coincidencias de un patrón, siendo cada una de estas coincidencias reemplazada por un reemplazo.
    ```javascript
    const cadena = 'Hola Mundo';
    const nuevaCadena = cadena.replace('Mundo', 'JavaScript');
    console.log(nuevaCadena); // 'Hola JavaScript'
    ```

14. **splice()**: Cambia el contenido de un array eliminando elementos existentes y/o agregando nuevos elementos.
    ```javascript
    const array = [1, 2, 3, 4];
    array.splice(2, 1, 'a', 'b');
    console.log(array); // [1, 2, 'a', 'b', 4]
    ```

15. **find()**: Devuelve el primer elemento de un array que cumpla con la función de prueba proporcionada.
    ```javascript
    const array = [1, 2, 3, 4];
    const encontrado = array.find(elemento => elemento > 2);
    console.log(encontrado); // 3
    ```

16. **split()**: Divide un objeto de tipo String en un array de cadenas mediante la separación de la cadena en subcadenas.
    ```javascript
    const cadena = 'Hola Mundo';
    const array = cadena.split(' ');
    console.log(array); // ['Hola', 'Mundo']
    ```

17. **charAt()**: Devuelve el carácter en el índice especificado.
    ```javascript
    const cadena = 'Hola Mundo';
    console.log(cadena.charAt(0)); // 'H'
    ```

18. **substring()**: Devuelve un subconjunto de un objeto String.
    ```javascript
    const cadena = 'Hola Mundo';
    console.log(cadena.substring(1, 4)); // 'ola'
    ```

19. **length**: Devuelve la longitud de un array o cadena.
    ```javascript
    const array = [1, 2, 3, 4];
    console.log(array.length); // 4
    const cadena = 'Hola Mundo';
    console.log(cadena.length); // 10
    ```

20. **fetch** y **axios**: Métodos para hacer peticiones HTTP.
    ```javascript
    // fetch
    fetch('https://api.example.com/data')
        .then(response => response.json())
        .then(data => console.log(data))
        .catch(error => console.error('Error:', error));

    // axios
    axios.get('https://api.example.com/data')
        .then(response => console.log(response.data))
        .catch(error => console.error('Error:', error));
    ```

21. **async/await**: Sintaxis para trabajar con promesas de manera más cómoda.
    ```javascript
    async function fetchData() {
        try {
            const response = await fetch('https://api.example.com/data');
            const data = await response.json();
            console.log(data);
        } catch (error) {
            console.error('Error:', error);
        }
    }
    ```

22. **Conceptos básicos de Express.js con MySQL**:
    ```javascript
    const express = require('express');
    const mysql = require('mysql');
    const app = express();

    const db = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '',
        database: 'mydatabase'
    });

    db.connect((err) => {
        if (err) throw err;
        console.log('Connected to database');
    });

    app.get('/users', (req, res) => {
        let sql = 'SELECT * FROM users';
        db.query(sql, (err, result) => {
            if (err) throw err;
            res.json(result);
        });
    });

    app.listen(3000, () => {
        console.log('Server started on port 3000');
    });
    ```
