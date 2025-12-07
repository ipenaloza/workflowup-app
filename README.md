# WorkflowUp

Proyecto Django para gestión de flujos de trabajo.

## Requisitos

- Python 3.13.9 o superior
- MariaDB/MySQL
- pip (gestor de paquetes de Python)

## Instalación

### 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
cd workflowup2
```

### 2. Crear y activar entorno virtual

```bash
python3 -m venv py-env
source py-env/bin/activate  # En Windows: py-env\Scripts\activate
```

### 3. Instalar dependencias

```bash
pip install django==5.2.8
pip install mysqlclient  # Para conexión con MariaDB/MySQL
```

### 4. Configurar la base de datos

Crea una base de datos MariaDB/MySQL con las siguientes credenciales (o modifica `workflowup/workflowup/settings.py` según tu configuración):

```sql
CREATE DATABASE workflowup2;
CREATE USER 'admindb'@'localhost' IDENTIFIED BY 'admindb';
GRANT ALL PRIVILEGES ON workflowup2.* TO 'admindb'@'localhost';
FLUSH PRIVILEGES;
```

### 5. Ejecutar migraciones

```bash
cd workflowup
python manage.py migrate
```

### 6. Crear superusuario (opcional)

```bash
python manage.py createsuperuser
```

## Ejecutar el servidor

```bash
cd workflowup
python manage.py runserver
```

El servidor estará disponible en `http://127.0.0.1:8000/`

## Estructura del proyecto

```
workflowup2/
├── py-env/              # Entorno virtual
├── workflowup/          # Proyecto Django
│   ├── manage.py        # Utilidad de gestión de Django
│   ├── db.sqlite3       # Base de datos SQLite (no usada actualmente)
│   └── workflowup/      # Configuración del proyecto
│       ├── settings.py  # Configuración principal
│       ├── urls.py      # URLs del proyecto
│       ├── wsgi.py      # Configuración WSGI
│       └── asgi.py      # Configuración ASGI
├── .gitignore
└── README.md
```

## Configuración

### Base de datos

El proyecto está configurado para usar MariaDB/MySQL. La configuración se encuentra en `workflowup/workflowup/settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'workflowup2',
        'USER': 'admindb',
        'PASSWORD': 'admindb',
        'HOST': '127.0.0.1',
        'PORT': '3306'
    }
}
```

### Variables de entorno

Para producción, se recomienda usar variables de entorno para datos sensibles como:
- `SECRET_KEY`
- Credenciales de base de datos
- `DEBUG = False`

## Comandos útiles

```bash
# Crear migraciones
python manage.py makemigrations

# Aplicar migraciones
python manage.py migrate

# Crear superusuario
python manage.py createsuperuser

# Ejecutar servidor de desarrollo
python manage.py runserver

# Ejecutar shell de Django
python manage.py shell

# Recopilar archivos estáticos
python manage.py collectstatic
```

## Tecnologías

- Django 5.2.8
- Python 3.13.9
- MariaDB/MySQL

## Notas de desarrollo

- El proyecto usa Django 5.2.8, asegúrate de revisar la [documentación oficial](https://docs.djangoproject.com/en/5.2/)
- La base de datos está configurada para MariaDB/MySQL
- El modo DEBUG está activado para desarrollo, desactívalo en producción

## Licencia

[Especifica la licencia de tu proyecto]

## Contribuir

[Especifica las guías para contribuir al proyecto]
