# Manual de Usuario - WorkflowUp

## Tabla de Contenidos
1. [Introducción](#introducción)
2. [Acceso al Sistema](#acceso-al-sistema)
3. [Roles y Permisos](#roles-y-permisos)
4. [Navegación General](#navegación-general)
5. [Módulo de Administración de Usuarios](#módulo-de-administración-de-usuarios)
6. [Módulo de Workflows](#módulo-de-workflows)
7. [Gestión de Contraseñas](#gestión-de-contraseñas)
8. [Preguntas Frecuentes](#preguntas-frecuentes)
9. [Solución de Problemas Comunes](#solución-de-problemas-comunes)

---

## Introducción

### ¿Qué es WorkflowUp?

WorkflowUp es una aplicación web de gestión de proyectos y flujos de trabajo con control de acceso basado en roles (RBAC). El sistema permite administrar workflows de liberación de software con procesos secuenciales que involucran múltiples roles: SCM, Release Manager y QA.

### Características Principales

- **Control de Acceso por Roles:** 5 roles distintos con permisos específicos
- **Gestión de Workflows:** Creación y seguimiento de flujos de trabajo de liberación
- **Aprobaciones Secuenciales:** Proceso de revisión por etapas (Línea Base → RM → Diferencias → QA)
- **Planes de Prueba QA:** Gestión de pruebas con seguimiento de avance y resultados
- **Registro de Actividades:** Auditoría completa de todas las acciones del sistema
- **Gestión de Usuarios:** Administración centralizada de usuarios y roles

### Requisitos del Navegador

WorkflowUp es compatible con las versiones actuales de:
- Google Chrome (recomendado)
- Mozilla Firefox
- Safari
- Microsoft Edge

---

## Acceso al Sistema

### Inicio de Sesión

1. Abrir el navegador web
2. Navegar a la URL del sistema: `http://127.0.0.1:8000/` (desarrollo) o la URL proporcionada por su administrador
3. Ingresar su **nombre de usuario** (solo letras minúsculas)
4. Ingresar su **contraseña**
5. Hacer clic en el botón **"Ingresar"**

![Pantalla de Login]
- **Campo Usuario:** Solo acepta letras minúsculas (a-z)
- **Campo Contraseña:** Sensible a mayúsculas/minúsculas
- **Enlace "¿Olvidó su contraseña?":** Para recuperación de contraseña

### Cerrar Sesión

1. Hacer clic en **"Cerrar Sesión"** en el menú de navegación
2. Será redirigido a la pantalla de inicio de sesión

### Primera Vez en el Sistema

Al ingresar por primera vez:
1. Use las credenciales proporcionadas por su administrador
2. Se recomienda cambiar su contraseña inmediatamente (ver sección [Cambiar Contraseña](#cambiar-contraseña))
3. Familiarícese con las opciones disponibles según su rol

---

## Roles y Permisos

WorkflowUp implementa 5 roles con permisos específicos:

### 1. Administrador

**Permisos:**
- Acceso completo a **Administración de Usuarios**
- Crear, editar y desactivar usuarios
- Asignar roles a usuarios
- Acceso al dashboard de workflows
- Cambiar contraseña propia

**Menú de Navegación:**
- Administración de Usuarios
- Workflow
- Cambiar Contraseña
- Cerrar Sesión

**Responsabilidades:**
- Gestionar usuarios del sistema
- Asignar roles apropiados
- Mantener usuarios activos/inactivos

### 2. Jefe de Proyecto

**Permisos:**
- **Crear workflows** de liberación
- Solicitar procesos de aprobación (Línea Base, RM Rev, Diff Info, QA)
- Crear y gestionar **planes de prueba QA**
- Visualizar estado de workflows propios
- Cambiar contraseña propia

**Menú de Navegación:**
- Workflow
- Crear Workflow
- Cambiar Contraseña
- Cerrar Sesión

**Responsabilidades:**
- Iniciar workflows de liberación
- Coordinar proceso de aprobación
- Crear planes de prueba para QA
- Dar seguimiento a workflows

### 3. SCM (Software Configuration Management)

**Permisos:**
- Visualizar workflows asignados
- Aprobar/rechazar **Línea Base**
- Aprobar/rechazar **Informe de Diferencias (Diff Info)**
- Ingresar código de línea base
- Cambiar contraseña propia

**Menú de Navegación:**
- Workflow
- Cambiar Contraseña
- Cerrar Sesión

**Responsabilidades:**
- Crear y registrar línea base del proyecto
- Generar informe de diferencias
- Aprobar o rechazar solicitudes de configuración

### 4. Release Manager

**Permisos:**
- Visualizar workflows asignados
- Aprobar/rechazar **Revisión RM**
- Ingresar código RM
- Cambiar contraseña propia

**Menú de Navegación:**
- Workflow
- Cambiar Contraseña
- Cerrar Sesión

**Responsabilidades:**
- Revisar solicitudes de liberación
- Asignar códigos RM
- Aprobar o rechazar liberaciones

### 5. QA (Quality Assurance)

**Permisos:**
- Visualizar workflows asignados
- Ejecutar **pruebas del plan QA**
- Actualizar **avance de pruebas** (0-100%)
- Marcar pruebas como **Aprobado/No aprobado**
- Aprobar/rechazar proceso QA completo
- Cambiar contraseña propia

**Menú de Navegación:**
- Workflow
- Cambiar Contraseña
- Cerrar Sesión

**Responsabilidades:**
- Ejecutar pruebas del plan
- Reportar avance y resultados
- Aprobar o rechazar proceso QA

---

## Navegación General

### Estructura del Menú

El menú de navegación se encuentra en la parte superior de todas las páginas y varía según el rol del usuario:

**Barra de Navegación:**
- **Logo/Título:** "WorkflowUp" (hace clic para volver al dashboard)
- **Enlaces de Navegación:** Varían según el rol (ver sección Roles)
- **Información del Usuario:** Muestra nombre y rol en el dashboard

### Dashboard Principal

El dashboard es la pantalla principal después de iniciar sesión. Su contenido varía según el rol:

#### Dashboard - Administrador
- Mensaje de bienvenida con nombre y rol
- Acceso rápido a Administración de Usuarios

#### Dashboard - Jefe de Proyecto
- **Lista de Workflows:** Tabla con todos los workflows creados
- **Filtros:**
  - ID Proyecto (desplegable)
  - Estado Workflow (Nuevo/Activo)
  - Rango de fechas (desde/hasta)
- **Columnas de la tabla:**
  - ID Workflow
  - ID Proyecto
  - Nombre Proyecto
  - Componente
  - Estado Workflow
  - Proceso Actual
  - Estado Proceso
  - Fecha Creación
  - Acciones (Ver Detalles)
- **Botón:** "Crear Nuevo Workflow"

#### Dashboard - SCM
- **Lista de Workflows:** Workflows en proceso de Línea Base o Diff Info
- **Columnas:**
  - ID Workflow
  - ID Proyecto
  - Nombre Proyecto
  - Jefe de Proyecto
  - Proceso
  - Estado Proceso
  - Acciones (Ver Detalles)

#### Dashboard - Release Manager
- **Lista de Workflows:** Workflows en proceso RM Rev
- **Columnas:**
  - ID Workflow
  - ID Proyecto
  - Nombre Proyecto
  - Jefe de Proyecto
  - Estado Proceso
  - Acciones (Ver Detalles)

#### Dashboard - QA
- **Lista de Workflows:** Workflows en proceso QA
- **Columnas:**
  - ID Workflow
  - ID Proyecto
  - Nombre Proyecto
  - Jefe de Proyecto
  - Estado Proceso
  - Acciones (Ver Detalles)

---

## Módulo de Administración de Usuarios

**Acceso:** Solo disponible para usuarios con rol **Administrador**

### Listar Usuarios

**Ruta:** Menú → Administración de Usuarios

**Funcionalidades:**

1. **Tabla de Usuarios**
   - ID
   - Usuario (username)
   - Nombre Completo
   - Email
   - Rol
   - Estado (Activo/Inactivo)
   - Acciones (Editar)

2. **Búsqueda y Filtros**
   - **Búsqueda:** Campo de texto que busca en username, nombre, apellido y email
   - **Filtro por Rol:** Desplegable con todos los roles disponibles
   - **Filtro por Estado:** Activo/Inactivo
   - **Botón "Buscar"**
   - **Botón "Limpiar Filtros"**

3. **Paginación**
   - Muestra 10 usuarios por página
   - Navegación: Primera, Anterior, Siguiente, Última

4. **Botón "Crear Usuario"**
   - Ubicado en la parte superior derecha

### Crear Usuario

**Pasos:**

1. Hacer clic en **"Crear Usuario"**
2. Completar el formulario:

   **Campos Obligatorios:**
   - **Usuario (Username):**
     - Solo letras minúsculas (a-z)
     - Único en el sistema
     - Máximo 15 caracteres
   - **Nombre:** Nombre del usuario
   - **Apellido:** Apellido del usuario
   - **Email:**
     - Formato válido de email
     - Único en el sistema
   - **Rol:** Seleccionar de la lista desplegable
     - Administrador
     - Jefe de Proyecto
     - SCM
     - Release Manager
     - QA
   - **Contraseña:** Mínimo 8 caracteres
   - **Confirmar Contraseña:** Debe coincidir con la contraseña

3. Hacer clic en **"Crear Usuario"**
4. Si hay errores, se mostrarán mensajes indicando qué corregir
5. Si es exitoso, será redirigido a la lista de usuarios con mensaje de confirmación

**Validaciones Automáticas:**
- Username se convierte automáticamente a minúsculas
- Email debe ser único
- Username debe ser único
- Las contraseñas deben coincidir
- Username solo acepta letras (sin números ni caracteres especiales)

### Editar Usuario

**Pasos:**

1. En la lista de usuarios, hacer clic en **"Editar"** junto al usuario deseado
2. Se mostrarán los datos actuales del usuario
3. **Campos Editables:**
   - **Rol:** Cambiar el rol del usuario
   - **Activo:** Marcar/desmarcar para activar/desactivar usuario
4. **Campos de Solo Lectura:**
   - Username
   - Nombre
   - Apellido
   - Email
5. Hacer clic en **"Actualizar Usuario"**
6. Confirmación de actualización exitosa

**Notas Importantes:**
- No se pueden editar los datos personales (nombre, apellido, email) desde esta interfaz
- No se puede cambiar la contraseña de otros usuarios
- Para cambiar username, debe crear un nuevo usuario

### Desactivar Usuario

**¿Por qué desactivar en lugar de eliminar?**
- El sistema NO permite eliminar usuarios físicamente
- Se usa el campo "Activo" para desactivar usuarios

**Pasos:**

1. Hacer clic en **"Editar"** junto al usuario
2. Desmarcar la casilla **"Activo"**
3. Hacer clic en **"Actualizar Usuario"**
4. El usuario no podrá iniciar sesión, pero sus datos se conservan

**Reactivar Usuario:**
- Seguir los mismos pasos pero marcar la casilla "Activo"

---

## Módulo de Workflows

### Conceptos Básicos

#### ¿Qué es un Workflow?

Un workflow representa un **proceso de liberación de software** que pasa por 4 etapas secuenciales:

1. **Línea Base** (SCM): Creación de la línea base del código
2. **RM Rev** (Release Manager): Revisión y asignación de código RM
3. **Diff Info** (SCM): Generación de informe de diferencias
4. **QA** (Quality Assurance): Pruebas de calidad

#### Estados del Workflow

- **Nuevo:** Workflow recién creado
- **Activo:** Workflow en proceso de aprobación
- **Cancelado:** Workflow cancelado por el Jefe de Proyecto
- **Cerrado:** Workflow completado (todas las etapas aprobadas)

#### Estados de Proceso

- **No Iniciado:** Proceso no solicitado aún
- **En Proceso:** Proceso solicitado, esperando aprobación
- **Ok:** Proceso aprobado
- **No Ok:** Proceso rechazado (se puede re-solicitar)

---

### Para Jefe de Proyecto

#### Crear Nuevo Workflow

**Pasos:**

1. En el dashboard, hacer clic en **"Crear Nuevo Workflow"**
2. Completar el formulario:

   **Campos Obligatorios:**
   - **ID Proyecto:** Código del proyecto (máx. 8 caracteres)
   - **Nombre Proyecto:** Nombre descriptivo (máx. 70 caracteres)
   - **Jefe de Proyecto:** Se pre-completa con su username
   - **Descripción Proyecto:** Descripción detallada
   - **Componente:** Componente a liberar (máx. 30 caracteres)
   - **QA Estimado:** Fecha estimada para QA (formato: DD/MM/AAAA)
   - **PAP Estimado:** Fecha estimada para PAP (formato: DD/MM/AAAA)
     - **IMPORTANTE:** PAP Estimado debe ser posterior a QA Estimado

3. Hacer clic en **"Crear Workflow"**
4. Será redirigido al detalle del workflow creado

**Validaciones:**
- PAP Estimado > QA Estimado
- Todos los campos obligatorios deben estar completos
- Fechas en formato válido

#### Ver Detalle del Workflow

**Acceso:** Dashboard → Hacer clic en "Ver" en la columna Acciones

**Secciones del Detalle:**

**1. Información General**
- ID Workflow
- ID Proyecto
- Nombre Proyecto
- Descripción
- Componente
- Jefe de Proyecto
- Fecha Creación
- QA Estimado
- PAP Estimado

**2. Información de Liberación**
- **Release:** (editable hasta solicitar RM Rev)
- **Línea Base:** (rellenado por SCM)
- **Código RM:** (rellenado por Release Manager)

**Botón "Editar Fechas":** Permite actualizar QA Estimado y PAP Estimado

**3. Gestión de Procesos**

**Botones de Solicitud de Procesos:**

**a) Botón "Solicitar Línea Base"**
- **Habilitado cuando:** Workflow está creado y no se ha solicitado aún
- **Al hacer clic:**
  - Modal solicita confirmación
  - Opcionalmente agregar comentario
  - Crea actividad en estado "En Proceso"
  - SCM verá el workflow en su dashboard

**b) Botón "Editar Release y Solicitar RM Rev"**
- **Habilitado cuando:**
  - Línea Base está aprobada (Ok) O
  - RM Rev fue rechazado (No Ok) y se quiere re-solicitar
- **Al hacer clic:**
  - Modal solicita ingresar código de Release (obligatorio)
  - Opcionalmente agregar comentario
  - Actualiza campo Release
  - Crea actividad RM Rev en estado "En Proceso"
  - Release Manager verá el workflow

**c) Botón "Solicitar Diff Info"**
- **Habilitado cuando:**
  - RM Rev está aprobado (Ok) O
  - Diff Info fue rechazado (No Ok) y se quiere re-solicitar
- **Al hacer clic:**
  - Modal solicita confirmación
  - Opcionalmente agregar comentario
  - Crea actividad Diff Info en estado "En Proceso"
  - SCM verá el workflow

**d) Botón "Solicitar QA"**
- **Habilitado cuando:**
  - Diff Info está aprobado (Ok) O
  - QA fue rechazado (No Ok) y se quiere re-solicitar
  - Existe al menos un plan de prueba creado
- **Al hacer clic:**
  - Modal solicita confirmación
  - Opcionalmente agregar comentario
  - Crea actividad QA en estado "En Proceso"
  - QA verá el workflow

**4. Estado de Procesos**

Tabla mostrando el estado de cada proceso:
- Proceso
- Estado
- Comentario (si existe)
- Fecha

**5. Registro de Actividades**

Tabla con todas las actividades del workflow:
- ID Actividad
- Fecha
- Usuario
- Estado Workflow
- Proceso
- Estado Proceso
- Actividad
- Comentario

**6. Botón "Cancelar Workflow"**
- Ubicado al final de la página
- Permite cancelar el workflow completo
- Requiere confirmación
- Solo disponible si el workflow no está ya Cancelado o Cerrado

#### Crear Plan de Pruebas QA

**Acceso:** Detalle del Workflow → Pestaña "Plan de Pruebas QA" → "Agregar Prueba"

**Pasos:**

1. En el detalle del workflow, hacer clic en la pestaña **"Plan de Pruebas QA"**
2. Hacer clic en **"Agregar Prueba"**
3. Completar el formulario:
   - **Prueba:** Descripción de la prueba (máx. 80 caracteres)
   - ID Prueba se asigna automáticamente de forma secuencial
4. Hacer clic en **"Agregar Prueba"**
5. La prueba aparecerá en la tabla con:
   - ID Prueba
   - Descripción
   - Avance: 0%
   - Resultado: No iniciado

**Notas:**
- Se pueden agregar múltiples pruebas
- Las pruebas se numeran automáticamente (1, 2, 3, ...)
- El QA podrá ver y ejecutar estas pruebas
- Debe haber al menos una prueba para solicitar QA

#### Editar Información del Workflow

**Editar Fechas:**

1. En el detalle del workflow, hacer clic en **"Editar Fechas"**
2. Modificar QA Estimado y/o PAP Estimado
3. Recordar: PAP Estimado > QA Estimado
4. Hacer clic en **"Actualizar Fechas"**

**Editar Release:**
- Solo se puede editar al solicitar RM Rev
- Usar el botón "Editar Release y Solicitar RM Rev"

---

### Para SCM (Software Configuration Management)

#### Dashboard SCM

**Visualización:**
- Workflows con proceso "Línea Base" en estado "En Proceso"
- Workflows con proceso "Diff Info" en estado "En Proceso"

#### Ver Detalle del Workflow (SCM)

**Acceso:** Dashboard → Hacer clic en "Ver"

**Información Visible:**
- Datos generales del workflow
- Estado de procesos
- Registro de actividades

**Acciones Disponibles:**

**1. Para Línea Base:**

**a) Editar Línea Base y Aprobar**
- **Cuándo:** Proceso Línea Base está en "En Proceso"
- **Pasos:**
  1. Hacer clic en **"Editar Línea Base y Aprobar"**
  2. Modal solicita:
     - **Línea Base:** Código de la línea base (obligatorio, máx. 80 caracteres)
     - **Comentario:** Opcional
  3. Hacer clic en **"Aprobar"**
  4. Se actualiza el campo Línea Base del workflow
  5. Se crea actividad con estado "Ok"
  6. Jefe de Proyecto puede continuar con RM Rev

**b) Rechazar Línea Base**
- **Cuándo:** Proceso Línea Base está en "En Proceso"
- **Pasos:**
  1. Hacer clic en **"Rechazar"**
  2. Modal solicita:
     - **Comentario:** OBLIGATORIO al rechazar
  3. Hacer clic en **"Rechazar"**
  4. Se crea actividad con estado "No Ok"
  5. Jefe de Proyecto puede re-solicitar

**2. Para Diff Info:**

**a) Aprobar Diff Info**
- **Cuándo:** Proceso Diff Info está en "En Proceso"
- **Pasos:**
  1. Hacer clic en **"Aprobar"**
  2. Modal solicita:
     - **Comentario:** Opcional
  3. Hacer clic en **"Aprobar"**
  4. Se crea actividad con estado "Ok"
  5. Jefe de Proyecto puede continuar con QA

**b) Rechazar Diff Info**
- **Cuándo:** Proceso Diff Info está en "En Proceso"
- **Pasos:**
  1. Hacer clic en **"Rechazar"**
  2. Modal solicita:
     - **Comentario:** OBLIGATORIO al rechazar
  3. Hacer clic en **"Rechazar"**
  4. Se crea actividad con estado "No Ok"
  5. Jefe de Proyecto puede re-solicitar

**Reglas Importantes:**
- El comentario es OBLIGATORIO al rechazar
- Al aprobar Línea Base, debe ingresar el código de línea base
- Solo puede actuar cuando el proceso está "En Proceso"

---

### Para Release Manager

#### Dashboard Release Manager

**Visualización:**
- Workflows con proceso "RM Rev" en estado "En Proceso"

#### Ver Detalle del Workflow (RM)

**Acceso:** Dashboard → Hacer clic en "Ver"

**Información Visible:**
- Datos generales del workflow
- Campo Release (visible el código ingresado por Jefe de Proyecto)
- Estado de procesos
- Registro de actividades

**Acciones Disponibles:**

**a) Editar Código RM y Aprobar**
- **Cuándo:** Proceso RM Rev está en "En Proceso"
- **Pasos:**
  1. Hacer clic en **"Editar Código RM y Aprobar"**
  2. Modal solicita:
     - **Código RM:** Código asignado (obligatorio, formato: 9 caracteres)
     - **Comentario:** Opcional
  3. Hacer clic en **"Aprobar"**
  4. Se actualiza el campo Código RM del workflow
  5. Se crea actividad con estado "Ok"
  6. Jefe de Proyecto puede continuar con Diff Info

**b) Rechazar RM Rev**
- **Cuándo:** Proceso RM Rev está en "En Proceso"
- **Pasos:**
  1. Hacer clic en **"Rechazar"**
  2. Modal solicita:
     - **Comentario:** OBLIGATORIO al rechazar
  3. Hacer clic en **"Rechazar"**
  4. Se crea actividad con estado "No Ok"
  5. Jefe de Proyecto puede editar Release y re-solicitar

**Reglas Importantes:**
- El comentario es OBLIGATORIO al rechazar
- Al aprobar, debe ingresar el Código RM (9 caracteres)
- Solo puede actuar cuando el proceso está "En Proceso"

---

### Para QA (Quality Assurance)

#### Dashboard QA

**Visualización:**
- Workflows con proceso "QA" en estado "En Proceso"

#### Ver Detalle del Workflow (QA)

**Acceso:** Dashboard → Hacer clic en "Ver"

**Información Visible:**
- Datos generales del workflow
- Estado de procesos
- **Plan de Pruebas QA** (tabla interactiva)
- Registro de actividades

#### Ejecutar Pruebas

**Tabla de Pruebas:**

Columnas:
- **ID Prueba:** Número secuencial
- **Prueba:** Descripción de la prueba
- **Avance:** Barra de progreso y porcentaje (0-100%)
- **Resultado:** Estado de la prueba
  - No iniciado
  - En proceso
  - Aprobado
  - No aprobado
- **Acciones:** Controles interactivos

**Actualizar Avance de Prueba:**

1. En la columna **Avance**, hay un control deslizante (slider)
2. Arrastrar el slider para ajustar el porcentaje (0-100%)
3. El avance se actualiza automáticamente (AJAX)
4. La barra de progreso se actualiza visualmente
5. Estados automáticos según avance:
   - 0%: "No iniciado"
   - 1-99%: "En proceso"
   - 100%: El QA decide si "Aprobado" o "No aprobado"

**Marcar Resultado de Prueba:**

1. En la columna **Resultado**, hay un botón con el estado actual
2. Para pruebas al 100%, hacer clic en el botón
3. Alterna entre:
   - **Aprobado:** Prueba exitosa (botón verde)
   - **No aprobado:** Prueba fallida (botón rojo)
4. El resultado se actualiza automáticamente

**Indicador de Progreso General:**
- En la parte superior de la tabla se muestra el progreso total
- Calcula el promedio de todas las pruebas
- Ejemplo: "Progreso General: 75%"

#### Aprobar o Rechazar Proceso QA

**Condiciones para Aprobar:**
- Todas las pruebas deben estar al 100%
- Todas las pruebas deben estar marcadas como "Aprobado"

**a) Aprobar QA**
- **Cuándo:** Todas las pruebas aprobadas
- **Pasos:**
  1. Verificar que todas las pruebas estén completadas y aprobadas
  2. Hacer clic en **"Aprobar QA"**
  3. Modal solicita:
     - **Comentario:** Opcional
  4. Hacer clic en **"Aprobar"**
  5. Se crea actividad con estado "Ok"
  6. El workflow cambia a estado "Cerrado" (proceso completo)

**b) Rechazar QA**
- **Cuándo:** Una o más pruebas no son satisfactorias
- **Pasos:**
  1. Hacer clic en **"Rechazar QA"**
  2. Modal solicita:
     - **Comentario:** OBLIGATORIO al rechazar
  3. Hacer clic en **"Rechazar"**
  4. Se crea actividad con estado "No Ok"
  5. Jefe de Proyecto puede re-solicitar QA

**Reglas Importantes:**
- No se puede aprobar QA si hay pruebas pendientes o no aprobadas
- El comentario es OBLIGATORIO al rechazar
- Los cambios en avance y resultado se guardan automáticamente

---

## Gestión de Contraseñas

### Cambiar Contraseña

**Acceso:** Menú → Cambiar Contraseña (disponible para todos los usuarios autenticados)

**Pasos:**

1. Hacer clic en **"Cambiar Contraseña"** en el menú
2. Completar el formulario:
   - **Contraseña Actual:** Su contraseña actual
   - **Nueva Contraseña:** Nueva contraseña deseada
   - **Confirmar Nueva Contraseña:** Repetir la nueva contraseña
3. Hacer clic en **"Cambiar Contraseña"**
4. Si es exitoso, será redirigido al dashboard con mensaje de confirmación

**Validaciones:**
- La contraseña actual debe ser correcta
- La nueva contraseña debe tener mínimo 8 caracteres (según configuración Django)
- Las contraseñas nuevas deben coincidir
- La nueva contraseña no puede ser igual a la actual

**Recomendaciones de Seguridad:**
- Use contraseñas fuertes (combinación de letras, números y símbolos)
- No reutilice contraseñas de otros sistemas
- Cambie su contraseña periódicamente
- No comparta su contraseña con nadie

### Recuperar Contraseña

**¿Cuándo usar?** Cuando olvidó su contraseña y no puede iniciar sesión

**Pasos:**

1. En la página de login, hacer clic en **"¿Olvidó su contraseña?"**
2. Ingresar su **dirección de email** registrada en el sistema
3. Hacer clic en **"Enviar"**
4. Recibirá un email con instrucciones
   - **En desarrollo:** El enlace aparece en la consola del servidor
   - **En producción:** Llegará a su email
5. Hacer clic en el enlace del email
6. Ingresar su **nueva contraseña**
7. Confirmar la **nueva contraseña**
8. Hacer clic en **"Cambiar Contraseña"**
9. Será redirigido al login con confirmación
10. Iniciar sesión con su nueva contraseña

**Notas:**
- El enlace de recuperación expira después de cierto tiempo
- Solo se puede usar el enlace una vez
- Si no recibe el email, verifique su carpeta de spam
- Contacte al administrador si no puede recuperar su contraseña

---

## Preguntas Frecuentes

### Generales

**P: ¿Puedo cambiar mi nombre de usuario?**
R: No, el nombre de usuario no se puede cambiar una vez creado. Si necesita un nuevo username, contacte al administrador para crear una nueva cuenta.

**P: ¿Por qué mi usuario solo acepta letras minúsculas?**
R: Es una regla de validación del sistema. Los nombres de usuario deben ser solo letras minúsculas (a-z) sin números, espacios ni caracteres especiales.

**P: ¿Puedo tener múltiples roles?**
R: No, cada usuario tiene asignado un solo rol. Si necesita realizar funciones de múltiples roles, contacte al administrador.

**P: ¿Qué sucede si mi cuenta está inactiva?**
R: No podrá iniciar sesión. Contacte al administrador para reactivar su cuenta.

### Workflows

**P: ¿Puedo editar un workflow después de creado?**
R: Puede editar las fechas estimadas (QA Estimado, PAP Estimado) y el campo Release (hasta solicitar RM Rev). Otros campos no son editables.

**P: ¿Puedo eliminar un workflow?**
R: No se pueden eliminar workflows. Puede cancelarlos usando el botón "Cancelar Workflow".

**P: ¿Qué pasa si rechazan mi solicitud?**
R: Puede revisar el comentario del rechazo en el registro de actividades y volver a solicitar el proceso después de hacer las correcciones necesarias.

**P: ¿En qué orden debo solicitar los procesos?**
R: El orden es secuencial y obligatorio:
1. Línea Base (SCM)
2. RM Rev (Release Manager)
3. Diff Info (SCM)
4. QA (Quality Assurance)

No puede saltar pasos.

**P: ¿Puedo crear workflows para otros jefes de proyecto?**
R: No, solo puede crear workflows asignados a su propio username (si es Jefe de Proyecto).

### Plan de Pruebas QA

**P: ¿Cuántas pruebas puedo agregar?**
R: No hay límite, pero debe haber al menos una prueba para solicitar QA.

**P: ¿Puedo eliminar una prueba?**
R: Actualmente no se permite eliminar pruebas una vez creadas.

**P: ¿Qué pasa si una prueba no aprobada?**
R: El QA debe marcar la prueba como "No aprobado" y luego puede rechazar el proceso QA completo para que el Jefe de Proyecto tome acciones correctivas.

### Administración de Usuarios

**P: ¿Puedo eliminar un usuario?**
R: No se permite eliminar usuarios físicamente. Debe desactivarlos marcando el campo "Activo" como falso.

**P: ¿Puedo cambiar la contraseña de otro usuario?**
R: No, ni siquiera el administrador puede cambiar contraseñas de otros usuarios. Use la función de recuperación de contraseña.

**P: ¿Qué pasa con los workflows si desactivo un usuario?**
R: Los workflows existentes se mantienen. El usuario desactivado aparecerá en el historial pero no podrá realizar nuevas acciones.

---

## Solución de Problemas Comunes

### No Puedo Iniciar Sesión

**Problema:** Error "Credenciales inválidas"

**Soluciones:**
1. Verificar que el nombre de usuario esté en minúsculas
2. Verificar que la contraseña sea correcta (sensible a mayúsculas)
3. Verificar que su cuenta esté activa (contactar administrador)
4. Intentar recuperar contraseña si la olvidó
5. Limpiar cookies y caché del navegador

### Error "Permiso Denegado"

**Problema:** Al intentar acceder a una página aparece "Permission Denied"

**Soluciones:**
1. Verificar que su rol tenga permisos para esa funcionalidad
2. Solo Administradores pueden acceder a Administración de Usuarios
3. Solo Jefes de Proyecto pueden crear workflows
4. Cada rol tiene acceso limitado a ciertas funciones
5. Contactar administrador si cree que debería tener acceso

### Los Botones Están Deshabilitados

**Problema:** Botones de solicitud de procesos aparecen deshabilitados (gris)

**Soluciones:**
1. Verificar que el proceso anterior esté aprobado
2. Para RM Rev: Verificar que haya ingresado el campo Release
3. Para QA: Verificar que exista al menos un plan de prueba
4. Para SCM: Verificar que haya ingresado Línea Base
5. Revisar el registro de actividades para ver el estado actual

### No Puedo Aprobar QA

**Problema:** Botón "Aprobar QA" no está disponible

**Soluciones:**
1. Verificar que todas las pruebas estén al 100%
2. Verificar que todas las pruebas estén marcadas como "Aprobado"
3. Si hay alguna prueba "No aprobado", debe rechazar el proceso QA
4. Refrescar la página por si los cambios no se reflejaron

### El Slider de Avance No Funciona

**Problema:** No puedo actualizar el avance de las pruebas

**Soluciones:**
1. Verificar conexión a internet (usa AJAX)
2. Refrescar la página
3. Verificar que el proceso QA esté en estado "En Proceso"
4. Limpiar caché del navegador
5. Intentar con otro navegador

### No Recibo Email de Recuperación

**Problema:** No llega el email para recuperar contraseña

**Soluciones:**
1. **En desarrollo:** El enlace aparece en la consola del servidor, no en email
2. Verificar carpeta de spam/correo no deseado
3. Verificar que el email registrado sea correcto
4. Esperar unos minutos (puede haber demora)
5. Contactar al administrador del sistema

### Error al Crear Workflow

**Problema:** Errores de validación al crear workflow

**Soluciones:**
1. Verificar que PAP Estimado sea posterior a QA Estimado
2. Verificar formato de fechas (DD/MM/AAAA)
3. Verificar que todos los campos obligatorios estén completos
4. Verificar longitud máxima de campos
5. Revisar mensajes de error específicos en el formulario

### La Página Se Ve Mal

**Problema:** Diseño roto o estilos no cargan

**Soluciones:**
1. Refrescar la página (Ctrl+F5 o Cmd+Shift+R)
2. Limpiar caché del navegador
3. Verificar conexión a internet (Tailwind CSS usa CDN)
4. Actualizar navegador a última versión
5. Intentar con otro navegador

### Sesión Expirada

**Problema:** Se cierra la sesión automáticamente

**Soluciones:**
1. La sesión expira después de inactividad
2. Volver a iniciar sesión
3. No usar múltiples pestañas con diferentes sesiones
4. Contactar administrador si el problema persiste

---

## Contacto y Soporte

### Información del Sistema

- **Nombre:** WorkflowUp
- **Versión Django:** 5.2.8
- **Versión Python:** 3.13
- **Desarrollador:** Iván Peñaloza
- **Institución:** Universidad Andrés Bello

### Soporte Técnico

**Para problemas técnicos o consultas:**
- **Email:** i.pealozazamora@uandresbello.edu
- **Tipo de soporte:** Problemas técnicos, bugs, consultas sobre funcionalidades

**Al reportar un problema, incluir:**
1. Descripción detallada del problema
2. Pasos para reproducir el error
3. Rol de usuario
4. Navegador y versión
5. Capturas de pantalla si es posible

### Administrador del Sistema

Para temas relacionados con:
- Creación o reactivación de cuentas
- Asignación o cambio de roles
- Problemas de acceso
- Solicitudes de nuevas funcionalidades

Contactar al administrador designado en su organización.

---

## Glosario

**Workflow:** Flujo de trabajo de liberación de software que pasa por múltiples etapas de aprobación.

**RBAC:** Role-Based Access Control (Control de Acceso Basado en Roles). Sistema de permisos según el rol del usuario.

**SCM:** Software Configuration Management (Gestión de Configuración de Software). Rol encargado de líneas base y diferencias.

**RM:** Release Manager (Gestor de Liberaciones). Rol encargado de revisar y aprobar liberaciones.

**QA:** Quality Assurance (Aseguramiento de Calidad). Rol encargado de ejecutar pruebas.

**Línea Base:** Versión del código fuente tomada como referencia para el workflow.

**Diff Info:** Informe de Diferencias. Documento que muestra cambios entre versiones.

**PAP:** Paso a Producción. Fecha en que el código se despliega a producción.

**Actividad:** Registro inmutable de una acción en el workflow (auditoría).

**Plan de Pruebas:** Conjunto de pruebas que QA debe ejecutar para validar el workflow.

---

**Documento:** Manual de Usuario WorkflowUp v1.0
**Última Actualización:** Diciembre 2025
**Audiencia:** Usuarios finales del sistema WorkflowUp
