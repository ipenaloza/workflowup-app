# Manual de Instalación - WorkflowUp

## Tabla de Contenidos
1. [Requisitos del Sistema](#requisitos-del-sistema)
2. [Instalación de Prerequisitos](#instalación-de-prerequisitos)
3. [Configuración del Proyecto](#configuración-del-proyecto)
4. [Configuración de la Base de Datos](#configuración-de-la-base-de-datos)
5. [Inicialización de la Aplicación](#inicialización-de-la-aplicación)
6. [Verificación de la Instalación](#verificación-de-la-instalación)
7. [Solución de Problemas](#solución-de-problemas)
8. [Configuración para Producción](#configuración-para-producción)

---

## Requisitos del Sistema

### Requisitos Mínimos de Hardware
- **Procesador:** Dual-core 2.0 GHz o superior
- **Memoria RAM:** 4 GB mínimo (8 GB recomendado)
- **Espacio en Disco:** 500 MB libres mínimo
- **Conexión a Internet:** Requerida para descarga de dependencias

### Requisitos de Software
- **Sistema Operativo:**
  - macOS 10.15 o superior
  - Linux (Ubuntu 20.04+, CentOS 8+, Debian 10+)
  - Windows 10/11 (con WSL2 recomendado)
- **Python:** Versión 3.13 o superior
- **MySQL:** Versión 8.0 o superior
- **Navegador Web:** Chrome, Firefox, Safari o Edge (versiones actuales)

---

## Instalación de Prerequisitos

### 1. Instalación de Python 3.13

#### En macOS
```bash
# Usando Homebrew
brew install python@3.13

# Verificar instalación
python3.13 --version
```

#### En Ubuntu/Debian
```bash
# Actualizar repositorios
sudo apt update

# Instalar Python 3.13
sudo apt install python3.13 python3.13-venv python3.13-dev

# Verificar instalación
python3.13 --version
```

#### En Windows
1. Descargar Python 3.13 desde https://www.python.org/downloads/
2. Ejecutar el instalador
3. **IMPORTANTE:** Marcar la opción "Add Python to PATH"
4. Completar la instalación
5. Verificar en PowerShell:
```powershell
python --version
```

### 2. Instalación de MySQL 8.0

#### En macOS
```bash
# Usando Homebrew
brew install mysql@8.0

# Iniciar el servicio MySQL
brew services start mysql@8.0

# Configurar seguridad (opcional pero recomendado)
mysql_secure_installation
```

#### En Ubuntu/Debian
```bash
# Actualizar repositorios
sudo apt update

# Instalar MySQL Server
sudo apt install mysql-server

# Iniciar el servicio
sudo systemctl start mysql
sudo systemctl enable mysql

# Configurar seguridad
sudo mysql_secure_installation
```

#### En Windows
1. Descargar MySQL 8.0 desde https://dev.mysql.com/downloads/installer/
2. Ejecutar el instalador
3. Seleccionar "Developer Default"
4. Seguir el asistente de instalación
5. Configurar password para usuario root

### 3. Instalación de pip y virtualenv

```bash
# Actualizar pip
python3.13 -m pip install --upgrade pip

# Instalar virtualenv (opcional, Python 3.13 incluye venv)
python3.13 -m pip install virtualenv
```

---

## Configuración del Proyecto

### 1. Obtener el Código Fuente

```bash
# Navegar al directorio donde desea instalar
cd /ruta/deseada/

# Si tiene el proyecto en un repositorio Git
git clone <URL_DEL_REPOSITORIO> workflowup2

# O copiar la carpeta del proyecto
cp -r /ruta/origen/workflowup2 /ruta/destino/
```

### 2. Crear y Activar el Entorno Virtual

```bash
# Navegar al directorio del proyecto
cd workflowup2

# Crear entorno virtual con Python 3.13
python3.13 -m venv py-env

# Activar el entorno virtual

## En macOS/Linux:
source py-env/bin/activate

## En Windows (PowerShell):
py-env\Scripts\Activate.ps1

## En Windows (CMD):
py-env\Scripts\activate.bat

# Verificar que el entorno está activo
# Debería ver (py-env) al inicio de la línea de comandos
which python  # En macOS/Linux
where python  # En Windows
```

### 3. Instalar Dependencias de Python

```bash
# Con el entorno virtual activado, instalar dependencias
pip install -r requirements.txt

# Verificar instalación
pip list
```

**Dependencias que se instalarán:**
- Django 5.2.8
- mysqlclient 2.2.7
- asgiref 3.11.0
- sqlparse 0.5.3

---

## Configuración de la Base de Datos

### 1. Acceder a MySQL

```bash
# Conectarse a MySQL como root
mysql -u root -p
# Ingresar la contraseña de root cuando se solicite
```

### 2. Crear la Base de Datos y Usuario

```sql
-- Crear la base de datos
CREATE DATABASE workflowup2 CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Crear el usuario (si no existe)
CREATE USER 'admindb'@'localhost' IDENTIFIED BY 'admindb';

-- Otorgar privilegios
GRANT ALL PRIVILEGES ON workflowup2.* TO 'admindb'@'localhost';

-- Aplicar cambios
FLUSH PRIVILEGES;

-- Verificar
SHOW DATABASES;
SELECT User, Host FROM mysql.user WHERE User = 'admindb';

-- Salir de MySQL
EXIT;
```

### 3. Verificar Conexión

```bash
# Probar conexión con las credenciales configuradas
mysql -u admindb -padmindb workflowup2

# Si se conecta correctamente, salir
EXIT;
```

### 4. Configurar Parámetros de Django (Opcional)

Si necesita cambiar las credenciales de la base de datos:

```bash
# Editar el archivo de configuración
nano workflowup/workflowup/settings.py
```

Buscar la sección `DATABASES` y modificar según sea necesario:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'workflowup2',          # Nombre de la base de datos
        'USER': 'admindb',               # Usuario de MySQL
        'PASSWORD': 'admindb',           # Contraseña del usuario
        'HOST': '127.0.0.1',             # Host (localhost)
        'PORT': '3306',                  # Puerto de MySQL
    }
}
```

---

## Inicialización de la Aplicación

### 1. Aplicar Migraciones de Base de Datos

```bash
# Navegar al directorio que contiene manage.py
cd workflowup

# Crear las migraciones (si es necesario)
python manage.py makemigrations

# Aplicar las migraciones a la base de datos
python manage.py migrate

# Deberá ver mensajes indicando que las tablas se crearon correctamente
```

### 2. Cargar Datos Iniciales (Usuarios de Prueba)

```bash
# Volver al directorio raíz del proyecto
cd ..

# Ejecutar el script de creación de usuarios
python setup_users.py

# Deberá ver mensajes confirmando la creación de 5 usuarios
```

**Usuarios creados por defecto:**
- **admin** / admin123 (Administrador)
- **jproyecto** / test123 (Jefe de Proyecto)
- **scm_user** / test123 (SCM)
- **release_mgr** / test123 (Release Manager)
- **qa_tester** / test123 (QA)

### 3. Crear un Superusuario (Opcional)

```bash
cd workflowup
python manage.py createsuperuser

# Seguir las instrucciones:
# - Username: [su elección]
# - Email: [su email]
# - Password: [su contraseña]
# - Password (again): [confirmar contraseña]
```

### 4. Recopilar Archivos Estáticos (Para Producción)

```bash
# Solo necesario en producción
python manage.py collectstatic
```

---

## Verificación de la Instalación

### 1. Iniciar el Servidor de Desarrollo

```bash
# Desde el directorio workflowup/
python manage.py runserver

# O especificar puerto diferente
python manage.py runserver 8080

# Deberá ver:
# Starting development server at http://127.0.0.1:8000/
# Quit the server with CONTROL-C.
```

### 2. Acceder a la Aplicación

Abrir un navegador web y navegar a:
```
http://127.0.0.1:8000/
```

Deberá ver la **página de inicio de sesión** de WorkflowUp.

### 3. Probar el Inicio de Sesión

**Prueba 1: Usuario Administrador**
```
Usuario: admin
Contraseña: admin123
```
- Deberá redirigir al dashboard
- Verificar que aparece "Administración de Usuarios" en el menú

**Prueba 2: Usuario Regular**
```
Usuario: qa_tester
Contraseña: test123
```
- Deberá redirigir al dashboard
- Verificar que NO aparece "Administración de Usuarios"

### 4. Acceder al Panel de Administración de Django

```
http://127.0.0.1:8000/admin/
```
- Usar las credenciales del superusuario creado
- Verificar acceso al panel administrativo

### 5. Ejecutar Pruebas del Sistema

```bash
# Ejecutar todas las pruebas
python manage.py test

# Verificar la configuración
python manage.py check

# Deberá mostrar: System check identified no issues (0 silenced).
```

---

## Solución de Problemas

### Error: "Can't connect to MySQL server"

**Causa:** El servidor MySQL no está ejecutándose o las credenciales son incorrectas.

**Solución:**
```bash
# Verificar estado del servicio MySQL
## macOS:
brew services list | grep mysql

## Linux:
sudo systemctl status mysql

# Iniciar MySQL si está detenido
## macOS:
brew services start mysql@8.0

## Linux:
sudo systemctl start mysql

# Verificar credenciales en settings.py
```

### Error: "ModuleNotFoundError: No module named 'mysqlclient'"

**Causa:** La dependencia mysqlclient no está instalada correctamente.

**Solución:**
```bash
# En macOS, puede necesitar:
brew install mysql-client
export PATH="/usr/local/opt/mysql-client/bin:$PATH"

# En Linux, puede necesitar:
sudo apt-get install python3-dev default-libmysqlclient-dev build-essential

# Reinstalar mysqlclient
pip install mysqlclient
```

### Error: "Port 8000 already in use"

**Causa:** Otro proceso está usando el puerto 8000.

**Solución:**
```bash
# Usar un puerto diferente
python manage.py runserver 8080

# O encontrar y detener el proceso
## macOS/Linux:
lsof -i :8000
kill -9 [PID]

## Windows:
netstat -ano | findstr :8000
taskkill /PID [PID] /F
```

### Error: "Template does not exist"

**Causa:** Configuración incorrecta de plantillas.

**Solución:**
```bash
# Verificar que TEMPLATES esté configurado en settings.py
# Verificar que los archivos de plantilla existen en workflowup/templates/
ls -la workflowup/templates/
```

### Error de Migraciones

**Causa:** Base de datos desincronizada o corrupta.

**Solución:**
```bash
# Resetear la base de datos (CUIDADO: Borra todos los datos)
python reset_db.py

# Aplicar migraciones nuevamente
cd workflowup
python manage.py migrate

# Recrear usuarios de prueba
cd ..
python setup_users.py
```

### Error: "Permission denied" al acceder a /usuarios/

**Causa:** Usuario sin rol de Administrador intentando acceder.

**Solución:**
- Esta es una funcionalidad esperada
- Solo usuarios con rol "Administrador" pueden acceder
- Iniciar sesión con usuario **admin/admin123**

---

## Configuración para Producción

### 1. Configuración de Seguridad

Editar `workflowup/workflowup/settings.py`:

```python
# Cambiar DEBUG a False
DEBUG = False

# Configurar hosts permitidos
ALLOWED_HOSTS = ['sudominio.com', 'www.sudominio.com', 'IP_DEL_SERVIDOR']

# Generar nueva SECRET_KEY (no usar la de desarrollo)
# Puede generar una usando:
# python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'
SECRET_KEY = 'NUEVA_CLAVE_SECRETA_AQUI'

# Configurar HTTPS
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True
```

### 2. Configuración de Base de Datos de Producción

```python
# Usar variables de entorno para credenciales
import os

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': os.environ.get('DB_NAME', 'workflowup2'),
        'USER': os.environ.get('DB_USER', 'admindb'),
        'PASSWORD': os.environ.get('DB_PASSWORD'),
        'HOST': os.environ.get('DB_HOST', '127.0.0.1'),
        'PORT': os.environ.get('DB_PORT', '3306'),
        'OPTIONS': {
            'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
            'charset': 'utf8mb4',
        },
    }
}
```

### 3. Configuración de Email

```python
# Configurar servidor SMTP real
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'  # O su servidor SMTP
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = os.environ.get('EMAIL_USER')
EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_PASSWORD')
DEFAULT_FROM_EMAIL = 'noreply@sudominio.com'
```

### 4. Recopilar Archivos Estáticos

```bash
# Configurar STATIC_ROOT en settings.py
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

# Ejecutar collectstatic
python manage.py collectstatic --noinput
```

### 5. Servidor Web (Gunicorn + Nginx)

#### Instalar Gunicorn

```bash
pip install gunicorn

# Probar Gunicorn
gunicorn --bind 0.0.0.0:8000 workflowup.wsgi:application
```

#### Configurar Nginx (ejemplo)

```nginx
server {
    listen 80;
    server_name sudominio.com www.sudominio.com;

    location = /favicon.ico { access_log off; log_not_found off; }

    location /static/ {
        root /ruta/a/workflowup2/workflowup;
    }

    location / {
        include proxy_params;
        proxy_pass http://127.0.0.1:8000;
    }
}
```

### 6. Servicio Systemd (Linux)

Crear `/etc/systemd/system/workflowup.service`:

```ini
[Unit]
Description=WorkflowUp Django Application
After=network.target

[Service]
User=www-data
Group=www-data
WorkingDirectory=/ruta/a/workflowup2/workflowup
Environment="PATH=/ruta/a/workflowup2/py-env/bin"
ExecStart=/ruta/a/workflowup2/py-env/bin/gunicorn --workers 3 --bind 127.0.0.1:8000 workflowup.wsgi:application

[Install]
WantedBy=multi-user.target
```

Activar el servicio:

```bash
sudo systemctl daemon-reload
sudo systemctl start workflowup
sudo systemctl enable workflowup
sudo systemctl status workflowup
```

### 7. Respaldos de Base de Datos

```bash
# Crear script de respaldo (backup.sh)
#!/bin/bash
mysqldump -u admindb -p workflowup2 > /ruta/backups/workflowup_$(date +%Y%m%d_%H%M%S).sql

# Dar permisos de ejecución
chmod +x backup.sh

# Programar en crontab (respaldo diario a las 2 AM)
crontab -e
# Agregar línea:
0 2 * * * /ruta/a/backup.sh
```

### 8. Monitoreo y Logs

```python
# Configurar logging en settings.py
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'file': {
            'level': 'ERROR',
            'class': 'logging.FileHandler',
            'filename': '/var/log/workflowup/django.log',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'ERROR',
            'propagate': True,
        },
    },
}
```

---

## Lista de Verificación Post-Instalación

- [ ] Python 3.13 instalado y funcionando
- [ ] MySQL 8.0 instalado y ejecutándose
- [ ] Entorno virtual creado y activado
- [ ] Dependencias instaladas desde requirements.txt
- [ ] Base de datos creada (workflowup2)
- [ ] Usuario de base de datos creado (admindb)
- [ ] Migraciones aplicadas correctamente
- [ ] Usuarios de prueba creados
- [ ] Servidor de desarrollo inicia sin errores
- [ ] Página de login accesible en el navegador
- [ ] Login exitoso con usuario admin
- [ ] Login exitoso con usuario regular
- [ ] Panel de administración Django accesible
- [ ] Pruebas del sistema pasan (python manage.py test)
- [ ] Verificación del sistema sin errores (python manage.py check)

---

## Comandos de Referencia Rápida

```bash
# Activar entorno virtual
source py-env/bin/activate  # macOS/Linux
py-env\Scripts\activate     # Windows

# Iniciar servidor
cd workflowup
python manage.py runserver

# Aplicar migraciones
python manage.py migrate

# Crear superusuario
python manage.py createsuperuser

# Ejecutar pruebas
python manage.py test

# Verificar configuración
python manage.py check

# Resetear base de datos (desarrollo)
python reset_db.py
python manage.py migrate
python setup_users.py

# Desactivar entorno virtual
deactivate
```

---

## Información de Contacto y Soporte

**Desarrollador:** Iván Peñaloza
**Email:** i.pealozazamora@uandresbello.edu
**Institución:** Universidad Andrés Bello
**Año:** 2025

Para problemas técnicos o consultas sobre la instalación, contactar al desarrollador.

---

**Documento:** Manual de Instalación WorkflowUp v1.0
**Última Actualización:** Diciembre 2025
**Versión de Django:** 5.2.8
**Versión de Python:** 3.13
