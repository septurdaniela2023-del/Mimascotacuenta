<?php
// 1. Definimos los módulos del sistema "Mi Mascota Cuenta"
$menu_sistema = [
    'Inicio' => [
        'enlace' => 'dashboard.php',
        'icono'  => 'fas fa-home'
    ],
    'Registro de Mascotas' => [
        'enlace' => 'mascotas.php',
        'icono'  => 'fas fa-id-card' // Ideal para el concepto de "cuenta/registro"
    ],
    'Control de Vacunas' => [
        'enlace' => 'vacunas.php',
        'icono'  => 'fas fa-syringe'
    ],
    'Agenda de Citas' => [
        'enlace' => 'citas.php',
        'icono'  => 'fas fa-calendar-alt'
    ],
    'Reportes / Estadísticas' => [
        'enlace' => 'reportes.php',
        'icono'  => 'fas fa-chart-pie'
    ]
];

// 2. Detectar la página actual para activar el estilo visual
$pagina_actual = basename($_SERVER['PHP_SELF']); 
?>

<!-- Estructura del Menú Lateral (Sidebar) -->
<div class="sidebar">
    <div class="sidebar-brand">
        <h2><span>Mi Mascota</span> Cuenta 🐾</h2>
    </div>
    
    <ul class="sidebar-menu">
        <?php foreach ($menu_sistema as $nombre => $datos): ?>
            <?php 
                // Si la página abierta coincide con el enlace, se activa
                $clase_activa = ($pagina_actual == $datos['enlace']) ? 'active' : ''; 
            ?>
            <li class="<?php echo $clase_activa; ?>">
                <a href="<?php echo $datos['enlace']; ?>">
                    <i class="<?php echo $datos['icono']; ?>"></i>
                    <span><?php echo $nombre; ?></span>
                </a>
            </li>
        <?php endforeach; ?>
    </ul>
    
    <div class="sidebar-footer">
        <p>© 2026 Gestión Comunitaria</p>
    </div>
</div>
