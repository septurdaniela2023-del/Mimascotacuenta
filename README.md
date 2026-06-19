<?php
// ==========================================
// 1. CONEXIÓN A LA BASE DE DATOS (Bloque PHP)
// ==========================================
$host = 'localhost';
$dbname = 'centro_mascotas';
$username = 'root'; // Usuario por defecto en XAMPP
$password = '';     // Contraseña por defecto en XAMPP vacía

try {
    // Creamos la conexión PDO
    $conexion = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8", $username, $password);
    // Configurar para que lance excepciones en caso de error
    $conexion->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    // 2. CONSULTA PARA OBTENER LOS 5 REGISTROS
    $query = "SELECT nombre, especie, raza, edad, comunidad FROM mascotas LIMIT 5";
    $stmt = $conexion->prepare($query);
    $stmt->execute();
    
    // Guardamos los resultados en una variable
    $mascotas = $stmt->fetchAll(PDO::FETCH_ASSOC);

} catch (PDOException $e) {
    // Si hay un error, detenemos el proceso y lo mostramos
    die("Error de conexión o consulta: " . $e->getMessage());
}
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro de Mascotas</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7f6;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            text-align: center;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        th {
            background-color: #4CAF50;
            color: white;
        }
        tr:hover {
            background-color: #f5f5f5;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Listado de Mascotas Registradas</h1>
    
    <table>
        <thead>
            <tr>
                <th>Nombre</th>
                <th>Especie</th>
                <th>Raza</th>
                <th>Edad (Años)</th>
                <th>Comunidad</th>
            </tr>
        </thead>
        <tbody>
            <?php
            // ==========================================
            // 3. MOSTRAR LOS DATOS DINÁMICAMENTE (Bloque PHP)
            // ==========================================
            // Verificamos si la consulta trajo registros
            if (count($mascotas) > 0) {
                // Recorremos cada mascota con un ciclo foreach
                foreach ($mascotas as $mascota) {
                    echo "tr";
                    // htmlspecialchars evita problemas con caracteres especiales o inyecciones de código
                    echo "<td>" . htmlspecialchars($mascota['nombre']) . "</td>";
                    echo "<td>" . htmlspecialchars($mascota['especie']) . "</td>";
                    echo "<td>" . htmlspecialchars($mascota['raza']) . "</td>";
                    echo "<td>" . htmlspecialchars($mascota['edad']) . "</td>";
                    echo "<td>" . htmlspecialchars($mascota['comunidad']) . "</td>";
                    echo "/tr";
                }
            } else {
                echo "<tr><td colspan='5' style='text-align:center;'>No hay mascotas registradas.</td></tr>";
            }
            ?>
        </tbody>
    </table>
</div>

</body>
</html>
