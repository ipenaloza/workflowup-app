# WorkflowUp - Sistema Django de Control de Acceso Basado en Roles

Una aplicación web completa desarrollada en Django 5.2.8 que implementa control de acceso basado en roles (RBAC) para gestión de proyectos y flujos de trabajo. Incluye autenticación personalizada de usuarios, administración de usuarios y controles de acceso específicos por rol.

## Características

- **Modelo de Usuario Personalizado** con 5 roles distintos
- **Módulo de Administración de Usuarios** (acceso solo para administradores)
- **Navegación Basada en Roles** (dinámica según el rol del usuario)
- **Autenticación Completa** (inicio de sesión, cierre de sesión, cambio de contraseña, recuperación de contraseña)
- **Panel de Workflow** (todos los usuarios autenticados)
- **Interfaz Responsiva** con Tailwind CSS
- **Características de Seguridad** (protección CSRF, protección XSS, hash de contraseñas)
- **Eliminación Lógica** (los usuarios pueden desactivarse, no eliminarse)

## Roles de Usuario

1. **Administrador** - Acceso completo al sistema incluyendo gestión de usuarios
2. **Jefe de Proyecto** - Capacidades de gestión de proyectos
3. **SCM** - Gestión de Configuración de Software
4. **Release Manager** - Gestión de lanzamientos
5. **QA** - Aseguramiento de Calidad

## Inicio Rápido

### Requisitos Previos

- Python 3.13
- MySQL 8.0+
- Entorno virtual (ya configurado en `py-env/`)

### Iniciar la Aplicación

```bash
# Navegar al directorio del proyecto
cd /Users/ipenaloza/WorkflowUp/@_version_2/workflowup2/workflowup

# Ejecutar el servidor de desarrollo
python manage.py runserver
```

Abrir el navegador en: **http://127.0.0.1:8000/**

## Documentación

Este proyecto incluye documentación completa:

## Estructura del Proyecto

```
workflowup2/
├── README.md                        # Este archivo
├── QUICK_START.md                   # Guía de inicio rápido
├── IMPLEMENTATION_SUMMARY.md        # Documentación técnica
├── TESTING_GUIDE.md                 # Lista de verificación de pruebas
├── CLAUDE.md                        # Resumen del proyecto
├── reset_db.py                      # Utilidad de reinicio de base de datos
├── setup_users.py                   # Creación de usuarios de prueba
├── py-env/                          # Entorno virtual
└── workflowup/                      # Proyecto Django
    ├── manage.py
    ├── templates/                   # Plantillas globales
    ├── users_admin/                 # App de administración de usuarios
    ├── workflow/                    # App de workflow
    └── workflowup/                  # Paquete de configuración
```

## Stack Tecnológico

- **Backend:** Django 5.2.8
- **Base de Datos:** MySQL 8.0
- **Python:** 3.13
- **Frontend:** HTML5, Tailwind CSS (CDN)
- **Autenticación:** Sistema de autenticación integrado de Django

## Detalles de Características Clave

### Modelo de Usuario Personalizado
- Extiende `AbstractUser` de Django
- Campo adicional `role` con 5 opciones
- Restricción de email único
- Nombre y apellido requeridos
- Protección contra eliminación física

### Administración de Usuarios
- **Vista de Lista:** Búsqueda, filtros, paginación
- **Vista de Creación:** Creación completa de usuarios con validación
- **Vista de Actualización:** Editar solo rol y estado activo
- **Sin Eliminación:** Eliminación física prevenida
- **Control de Acceso:** Requiere rol de Administrador

### Sistema de Autenticación
- Inicio de sesión en URL raíz (`/`)
- Autenticación basada en sesiones
- Cambio de contraseña para usuarios autenticados
- Recuperación de contraseña basada en email
- Backend de email de consola (desarrollo)

### Aplicación Workflow
- Panel principal después del inicio de sesión
- Muestra nombre y rol del usuario
- Accesible para todos los usuarios autenticados
- Marcador de posición para funciones futuras

### Navegación Basada en Roles
- **Administrador:** Admin de Usuarios + Workflow + Cambio de Contraseña
- **Otros Roles:** Workflow + Cambio de Contraseña
- Dinámica según rol del usuario
- Implementada mediante procesador de contexto

### Características de Seguridad
- Protección CSRF en todos los formularios
- Hash de contraseñas (PBKDF2)
- Prevención XSS (auto-escape)
- Prevención de inyección SQL (ORM)
- Gestión de sesiones
- Decoradores de login requerido

## Desarrollo

### Comandos Comunes

```bash
# Crear migraciones
python workflowup/manage.py makemigrations

# Aplicar migraciones
python workflowup/manage.py migrate

# Crear superusuario
python workflowup/manage.py createsuperuser

# Shell de Django
python workflowup/manage.py shell

# Ejecutar pruebas
python workflowup/manage.py test

# Verificar problemas
python workflowup/manage.py check
```

## URLs

- **Raíz:** `/` - Página de inicio de sesión
- **Cerrar sesión:** `/logout/`
- **Cambio de contraseña:** `/password-change/`
- **Recuperar contraseña:** `/password-reset/`
- **Admin de Usuarios:** `/usuarios/` (solo admin)
- **Workflow:** `/workflow/`
- **Admin de Django:** `/admin/`

## Pruebas

Ver **TESTING_GUIDE.md** para lista de verificación completa de pruebas incluyendo:

- Pruebas de flujo de autenticación
- Pruebas de autorización (basadas en roles)
- Operaciones CRUD de usuarios
- Gestión de contraseñas
- Verificación UI/UX
- Pruebas de seguridad
- Casos límite

## Configuración

### Base de Datos

```python
# workflowup/workflowup/settings.py
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

### Email (Desarrollo)

```python
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
```

Los emails de recuperación de contraseña se imprimen en la terminal durante el desarrollo.


Antes de desplegar en producción:

1. **Seguridad**
   - Cambiar SECRET_KEY
   - Establecer DEBUG = False
   - Configurar ALLOWED_HOSTS
   - Usar variables de entorno para secretos

2. **Email**
   - Configurar ajustes SMTP
   - Probar entrega de emails

3. **Base de Datos**
   - Usar base de datos de producción
   - Configurar respaldos automatizados

4. **Archivos Estáticos**
   - Ejecutar collectstatic
   - Configurar servidor web

5. **Monitoreo**
   - Configurar registro de errores
   - Configurar monitoreo de aplicación


### Problemas Comunes

**No puedo iniciar sesión:** Verificar usuario/contraseña, verificar que el usuario esté activo

**Permiso denegado:** Verificar que el usuario tenga el rol correcto (Administrador para admin de usuarios)

**Plantillas no encontradas:** Verificar TEMPLATES DIRS en settings.py

**Errores de base de datos:** Ejecutar `python reset_db.py` y migrar nuevamente

## Créditos

- **Desarrollador:** Iván Peñaloza
- **Institución:** Universidad Andrés Bello
- **Tipo de Proyecto:** Proyecto de título
- **Año:** 2025
- **Framework:** Django 5.2.8

## Licencia

Uso Educativo/Académico

## Contacto

Para preguntas o problemas relacionados con este proyecto:
- Email: i.pealozazamora@uandresbello.edu

---

**¡Comienza a usar WorkflowUp hoy!** Ver QUICK_START.md para empezar.
