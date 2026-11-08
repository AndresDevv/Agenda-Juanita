# Agenda Simple V2

Sistema web para administrar clientes y sus citas. Está hecho con Django y funciona por defecto con SQLite, por lo que no requiere instalar ni configurar un servidor de base de datos. También permite usar MariaDB/MySQL.

## Requisitos

- Python 3.10 o posterior.
- Windows PowerShell, CMD, macOS o Linux.

## Instalación y ejecución en Windows

Desde esta carpeta, ejecuta:

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe manage.py migrate
.\.venv\Scripts\python.exe manage.py createsuperuser
.\.venv\Scripts\python.exe manage.py runserver
```

Abre <http://127.0.0.1:8000/> e inicia sesión con el usuario creado. La base se guarda en `db.sqlite3`. Si `.venv` ya existía y dejó de funcionar, bórrala y vuelve a ejecutar los dos primeros comandos.

## MariaDB/MySQL (opcional)

Instala `mysqlclient` en el entorno virtual y crea `agenda_simple_v2_db` con codificación `utf8mb4`. Configura estas variables antes de iniciar Django:

```powershell
$env:DB_ENGINE = "mysql"
$env:DB_NAME = "agenda_simple_v2_db"
$env:DB_USER = "root"
$env:DB_PASSWORD = "tu_clave"
$env:DB_HOST = "127.0.0.1"
$env:DB_PORT = "3306"
```

Luego ejecuta `manage.py migrate` y los demás comandos normalmente. `DJANGO_SECRET_KEY`, `DJANGO_DEBUG` y `DJANGO_ALLOWED_HOSTS` también se pueden configurar mediante variables de entorno para despliegues.

## Funciones

- Inicio de sesión y cierre de sesión.
- Registro, búsqueda, edición y eliminación de clientes.
- Registro, búsqueda, edición y eliminación de citas.
- Restricción para evitar eliminar clientes que tengan citas asociadas.
- Panel con totales de clientes y citas.

Para más información didáctica revisa [GUIA_DOCENTE.md](GUIA_DOCENTE.md).
