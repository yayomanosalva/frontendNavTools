## PHP 


# Insertar datos en MySQL mediante PHP

### conexion.php

```php
<?php
$host = "localhost";
$user = "root";
$pw = "clave123";
$bd = "prueba";
?>
```

### insertar.php
```php
  <?php
  include("conexion.php");
  
  if(isset($_POST['nombre']) && !empty($_POST['nombre']) &&
     isset($_POST['pw']) && !empty($_POST['pw']))
  {
    //  sirve para conectar con el servidor
    $con = mysql_connect($host,$user,$pw) or die ("Problema al conectar el host");
    
    //  sirve para seleccionar base de datos 
    mysql_select_db($bd,$con) or die ("Problema con la bd");
    
    //  sirve para realizar consulta 
    mysql_query("INSERT INTO personas (nombre, pw) VALUES ('$_POST[nombre]','$_POST[pw]')",$con);
    
    echo "datos insertados correctamente";
  }else{
    echo "problemas al insertar datos";
  }
  ?>
  ```

### form.php
```php
  <form name="formulario" method="post" action="insertar.php">
  	<p>Datos Generales</p>
  	<p>Nombre de Empleado:
  	<input type="text" name="nombre" id="textfield" />
  	</p>
  	<p>Nombre de Empleado:
    <input type="password" name="pw" id="textfield" />
    </p>
  	<li>
  		<input type="submit" name="enviar" value="Guardar">
  	</li>
	</form>
```

# Seleccionar Registros de Base de Datos en PHP

# Eliminar Registros de Base de Datos en PHP


##### Jair Manosalva
