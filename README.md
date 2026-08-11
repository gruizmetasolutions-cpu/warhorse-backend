# ⚙️ Warhorse Logistics Group — Official API Backend

Servicio API REST y servidor backend desarrollado en **CodeIgniter 4 (PHP 8.x)** para la gestión y enrutamiento inteligente de oportunidades comerciales y cotizaciones de **Warhorse Logistics Group**.

## 🌟 Características Principales

- **Endpoint de Contacto Inteligente (`POST /api/contact`)**:
  - Procesa requerimientos de clientes según la modalidad seleccionada (`ftl`, `ltl`, `special`, `managed`).
  - Redirecciona lógicamente las notificaciones a los departamentos correspondientes (`Quotes@WarhorseBrokerage.com`, `SafetyandCompliance@warhorsebrokerage.com`, etc.).
- **Persistencia SQL**: Estructura de BD en MySQL (`warhorse_db`) preparada para registro de prospectos.
- **CORS Configurado**: Integración fluida con el cliente React frontend.

## 🛠️ Tech Stack

- **Lenguaje**: PHP 8.x
- **Framework**: CodeIgniter 4 (CI4)
- **Base de Datos**: MySQL 8.x / MariaDB (Compatible con entorno Laragon `.test`)
- **Gestor de Dependencias**: Composer

## 🚀 Inicio Rápido

### Prerrequisitos
- PHP >= 8.1 con extensiones `intl`, `mbstring`, `mysqli`, `curl`, `json` habilitadas.
- MySQL / MariaDB (o Laragon).
- Composer 2.x

### Instalación

```bash
# 1. Clonar repositorio
git clone https://github.com/gruizmetasolutions-cpu/warhorse-backend.git
cd warhorse-backend

# 2. Instalar dependencias con Composer
composer install

# 3. Configurar entorno
cp .env.example .env

# 4. Crear la Base de Datos en MySQL
# mysql -u root -e "CREATE DATABASE IF NOT EXISTS warhorse_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"

# 5. Iniciar el servidor local de CodeIgniter
php spark serve
```

El servidor estará escuchando en `http://localhost:8080`.

## 📡 Endpoints de la API

### 1. Registrar Cotización / Contacto
- **Método**: `POST`
- **Ruta**: `/api/contact`
- **Headers**: `Content-Type: application/json`
- **Body**:
```json
{
  "name": "Juan Pérez",
  "email": "juan@empresa.com",
  "service": "ftl",
  "message": "Requiero cotización FTL de Cd. Juárez a El Paso para 3 cargas semanales."
}
```
- **Respuesta de Éxito (200 OK)**:
```json
{
  "status": "success",
  "message": "Contact request received and routed to specialized department.",
  "department": "Quotes@WarhorseBrokerage.com"
}
```

## 📂 Estructura del Proyecto

```text
backend/
├── app/
│   ├── Config/
│   │   ├── Database.php        # Configuración de base de datos
│   │   └── Routes.php          # Definición de rutas API (/api/contact)
│   ├── Controllers/
│   │   ├── BaseController.php
│   │   └── ContactController.php # Controlador de enrutamiento inteligente
│   ├── Models/
│   └── Views/
├── public/
│   └── index.php               # Punto de entrada HTTP
├── writable/                   # Archivos temporales, logs y cache (Ignorados por git)
├── .env.example                # Plantilla sanitizada de entorno
├── composer.json
└── spark                       # CLI de CodeIgniter 4
```

## 🔒 Seguridad y Buenas Prácticas

- Ninguna contraseña de base de datos real ni secreto de producción se encuentra en el repositorio.
- Las variables reales deben configurarse de forma local mediante el archivo `.env` (el cual está protegido en `.gitignore`).

---

© 2026 **Warhorse Logistics Group**. Todos los derechos reservados.
