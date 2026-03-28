# 🔐 OAuth3 API – Autenticación con Django + Docker + MySQL

API de autenticación desarrollada con Django REST Framework que incluye registro de usuarios, autenticación y base para MFA (Multi-Factor Authentication).
El proyecto está completamente dockerizado usando MySQL como base de datos.

---

## 🚀 Tecnologías

* Python 3.10
* Django 5
* Django REST Framework
* MySQL 8
* Docker & Docker Compose

---

## 📁 Estructura del proyecto

```
oauth3/
│
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
├── manage.py
├── README.md
│
├── oauth3_project/       # Configuración principal Django
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
└── OAuth3/               # App principal (auth + MFA)
    ├── models.py         # Modelo de usuario personalizado
    ├── views.py          # Endpoints API
    ├── serializers.py    # Validación de datos
    ├── urls.py           # Rutas de la app
    ├── admin.py          # Configuración admin
    ├── services/         # Lógica de negocio desacoplada
    │   ├── email_service.py
    │   └── mfa_service.py
    └── migrations/
```

---

## ⚙️ Configuración del entorno

Crear archivo `.env` en la raíz:

```
MYSQL_DATABASE=oauth3_db
MYSQL_USER=oauth3_user
MYSQL_PASSWORD=oauth3_pass
MYSQL_ROOT_PASSWORD=rootpass
```

---

## 🐳 Levantar el proyecto con Docker

### 1. Construir y levantar contenedores

```
docker compose up --build
```

---

### 2. Servicios incluidos

* **API Django** → http://localhost:8000
* **MySQL** → puerto `3307` (host)

---

### 3. Base de datos MySQL

* Host (desde Docker): `mysql`
* Host (desde tu PC): `localhost`
* Puerto: `3307`

---

## 🛠 Comandos útiles

### Crear superusuario

```
docker exec -it oauth3-api-container python manage.py createsuperuser
```

---

### Aplicar migraciones

```
docker exec -it oauth3-api-container python manage.py migrate
```

---

### Acceder a MySQL desde el contenedor

```
docker exec -it oauth3-mysql mysql -u root -p
```

---

## 🔐 Panel de administración

```
http://localhost:8000/admin/
```

Desde aquí puedes:

* Crear usuarios
* Gestionar MFA
* Ver datos en la base de datos

---

## 📡 Endpoints principales

### Registro de usuario

```
POST /api/auth/register/
```

#### Body (JSON):

```
{
  "email": "user@test.com",
  "password": "12345678",
  "nombres": "Nombre",
  "apellidos": "Apellido"
}
```

---

### Respuesta esperada

```
201 Created
```

---

## ⚠️ Notas importantes

* El endpoint `/api/auth/register/` **no acepta GET**
* Debe usarse POST (Postman, curl, etc.)
* Docker maneja la red interna, por eso se usa `mysql` como host

---

## 🧠 Arquitectura

El proyecto separa responsabilidades:

* **models.py** → estructura de datos
* **serializers.py** → validación
* **views.py** → lógica HTTP
* **services/** → lógica de negocio reutilizable

Esto permite escalar fácilmente (ej: agregar JWT, OAuth, MFA completo).

---

## 🚀 Próximas mejoras

* Autenticación con JWT
* Refresh tokens
* MFA completo (TOTP / email)
* OAuth providers (Google, GitHub)

---

## 👨‍💻 Autor

Proyecto desarrollado como práctica avanzada de backend con Django + Docker.

```
```
