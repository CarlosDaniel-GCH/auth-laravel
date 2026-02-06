# 🚀 Laravel Auth API (Sanctum)

Este es un backend robusto construido con Laravel para gestionar la autenticación de usuarios mediante tokens (API Rest). Utiliza Laravel Sanctum para emitir tokens de acceso seguros que pueden ser consumidos por cualquier cliente (Vue, React, Postman, etc.).

## 🛠️ Tecnologías utilizadas

- Framework: Laravel 10/11
- Autenticación: Laravel Sanctum
- Base de datos: MySQL / PostgreSQL
- Herramienta de pruebas: Postman

## 🏁 Instalación y Configuración

Sigue estos pasos para levantar el proyecto localmente:


### 1. Clonar el repositorio:

```bash
git clone https://github.com/CarlosDaniel-GCH/auth-laravel.git
cd auth-laravel
```

### 2. Instalar dependencias:

```bash
composer install
```

### 3. Configurar el entorno:

- Copia el archivo de ejemplo: cp .env.example .env
- Configura tus credenciales de base de datos en el archivo .env.

### 4. Generar clave de aplicación y migrar:

```bash
php artisan key:generate
php artisan migrate
```

### 5. Iniciar el servidor:

```bash
php artisan serve
```

## 📡 Endpoints de la API

Todas las peticiones deben incluir el Header: Accept: application/json.

| Método | Ruta | Descripción | Protección |
| :--- | :--- | :--- | :--- |
| **POST** | `/api/register` | Registra un nuevo usuario y retorna el Bearer Token. | 🔓 Pública |
| **POST** | `/api/login` | Autentica credenciales y retorna el Bearer Token. | 🔓 Pública |
| **GET** | `/api/user` | Retorna los datos del usuario dueño del token. | 🔐 `auth:sanctum` |

## 🔐 Guía de Uso con Postman

### 1. Registro / Login

Envía un POST con email y password. Recibirás una respuesta como esta:

```json
{
    "access_token": "1|yQr3QDJ...",
    "token_type": "Bearer"
}
```

### 2. Acceso a Rutas Protegidas

Para las rutas que requieren autenticación, debes usar el token obtenido:

- Pestaña Authorization: Selecciona Bearer Token.
- Token: Pega el valor de access_token.

## 📂 Estructura del Proyecto (Lógica de Auth)

- app/Models/User.php: Usa el trait HasApiTokens para gestionar los tokens.
- app/Http/Controllers/RegisterController.php: Contiene la lógica de creación y validación de usuarios.
- app/Http/Middleware/MiAutenticacion.php: Middleware personalizado para filtros de seguridad adicionales.