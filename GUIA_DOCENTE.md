# Agenda Simple V2 — Guía docente

## 1. Estructura

- `config`: configuración Django, URLs y puntos de entrada WSGI/ASGI.
- `apps/models`: modelos de clientes y citas.
- `apps/views.py`: login protegido, operaciones CRUD, búsquedas y validación.
- `apps/templates/control`: interfaz de inicio, clientes, citas y login.
- `apps/static/control`: estilos y confirmación de eliminación.
- `apps/migrations`: creación de las tablas de la aplicación.

## 2. Modelo de datos

`Cliente` corresponde a `clientes`: nombre, apellido, correo, DNI, teléfono y fechas automáticas. `Cita` corresponde a `citas`: asunto, fecha, hora, dirección, referencia, notas, estado y fechas automáticas. Una cita pertenece a un cliente; un cliente puede tener varias citas. En SQL la clave foránea se llama `client_id`, aunque en Django se accede como `cita.cliente`.

Los estados admitidos son Pendiente, Confirmada, Completada y Cancelada. El DNI se valida como ocho dígitos. Los teléfonos, referencias y notas son opcionales. Se evita borrar clientes que aún tengan citas.

## 3. Instalación en Windows

Se requiere Python 3.10 o posterior. Desde la carpeta del proyecto ejecuta:

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe manage.py check
.\.venv\Scripts\python.exe manage.py migrate
.\.venv\Scripts\python.exe manage.py createsuperuser
.\.venv\Scripts\python.exe manage.py runserver
```

Abre `http://127.0.0.1:8000/` e inicia sesión con el superusuario creado. Si recibes un error de Python no encontrado al usar `.venv`, elimina esa carpeta virtual antigua, créala de nuevo y repite la instalación.

## 4. Base de datos

SQLite está habilitada por defecto y no requiere instalación adicional. Las migraciones crean `db.sqlite3` automáticamente. Para usar MariaDB/MySQL, instala `mysqlclient`, crea la base `agenda_simple_v2_db` con codificación `utf8mb4` y configura las variables de entorno `DB_ENGINE=mysql`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST` y `DB_PORT`. En PowerShell:

```powershell
$env:DB_ENGINE = "mysql"
$env:DB_NAME = "agenda_simple_v2_db"
$env:DB_USER = "root"
$env:DB_PASSWORD = "tu_clave"
$env:DB_HOST = "127.0.0.1"
$env:DB_PORT = "3306"
```

La versión de Django aceptada está fijada en `requirements.txt` para mantener compatibilidad con Python 3.10 y posterior.

## 5. Flujo CRUD para practicar

1. Crear un cliente y revisar cómo se guarda en `clientes`.
2. Agendar una cita para ese cliente y observar la relación `client_id`.
3. Editar y buscar clientes y citas.
4. Intentar eliminar el cliente que tiene citas: el sistema muestra un aviso y conserva los datos.
5. Eliminar la cita y luego eliminar el cliente.

Los formularios usan POST y protección CSRF. Las vistas validan los datos antes de guardar y redirigen con mensajes de resultado.
