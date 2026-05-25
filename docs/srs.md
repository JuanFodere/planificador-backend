# Especificación de Requerimientos del Sistema (SRS)

## Sistema: Planificador de Viajes a Japón

# 1. Introducción

## 1.1 Propósito

El presente documento tiene como objetivo definir los requerimientos funcionales y no funcionales del sistema “Planificador de Viajes a Japón”, así como describir su comportamiento esperado, actores involucrados y reglas de negocio.

Este documento servirá como base para el diseño, desarrollo y validación del sistema.

## 1.2 Alcance del sistema

El sistema permitirá a los usuarios planificar viajes a Japón mediante la creación de planes personalizados, gestionar actividades y compartir planes en un foro público.

El sistema incluirá:

- Gestión de planes de viaje
- Gestión de actividades dentro de los planes
- Exploración de actividades mediante mapa interactivo por prefecturas
- Selección de ubicaciones geográficas mediante mapa interactivo
- Visualización de ubicación de actividades mediante integración con Google Maps
- Interacción social mediante foro (likes y comentarios)

### Funcionalidades fuera de alcance

El sistema NO contemplará:

- Procesamiento de pagos o reservas reales
- Integración con sistemas de transporte (trenes, vuelos, etc.)
- Recomendaciones automáticas
- Integración con APIs externas de turismo
- Chat en tiempo real entre usuarios
- Exportación de planes

## 1.3 Definiciones

- **Plan de viaje:** Representa un viaje completo definido por un usuario, incluyendo información general y actividades planificadas.
- **Actividad:** Evento, paseo, tour o lugar de interés con información descriptiva.
- **Actividad personalizada:** Actividad creada por un usuario y visible únicamente para dicho usuario.
- **Actividad global:** Actividad creada por un administrador y visible para todos los usuarios.
- **Prefectura:** División territorial de Japón utilizada para agrupar actividades.
- **Foro:** Espacio donde los usuarios publican planes.
- **Mapa interactivo:** Componente visual que permite explorar prefecturas y seleccionar ubicaciones geográficas.
- **Ubicación geográfica:** Coordenadas de latitud y longitud asociadas a una actividad.

# 2. Descripción general

## 2.1 Perspectiva del sistema

El sistema será una aplicación web que permitirá la interacción entre usuarios y la gestión de información relacionada con viajes.

El sistema integrará un mapa interactivo utilizando Leaflet y OpenStreetMap para la exploración geográfica y selección de ubicaciones.

También permitirá la apertura de ubicaciones externas mediante Google Maps.

## 2.2 Actores del sistema

### Visitante (no autenticado)

Puede visualizar actividades y planes publicados.

### Usuario registrado

Puede crear planes, gestionar actividades, publicar contenido y participar en el foro.

### Administrador

Puede gestionar actividades globales y moderar contenido del foro.

## 2.3 Funcionalidades principales

- Creación y gestión de planes de viaje
- Gestión de actividades dentro de planes
- Exploración de actividades mediante mapa interactivo
- Selección de ubicaciones geográficas en mapa
- Publicación de planes en foro
- Interacción social (likes y comentarios)

## 2.4 Restricciones

- El sistema será accesible mediante navegador web
- Se requerirá conexión a internet
- Se utilizará Leaflet junto con OpenStreetMap para funcionalidades geográficas
- El sistema utilizará Google Maps únicamente como servicio externo de navegación

# 3. Requerimientos específicos

## 3.1 Reglas de negocio

- RN01: Un usuario podrá tener un máximo de 8 planes
- RN02: Los planes serán privados por defecto
- RN03: Solo los planes publicados serán visibles en el foro
- RN04: Se permite solapamiento de actividades
- RN05: La duración de actividades puede ser modificada por el usuario
- RN06: Las actividades globales serán gestionadas por administradores
- RN07: Las actividades de usuario serán privadas
- RN08: Solo usuarios registrados pueden interactuar en el foro
- RN09: Los usuarios pueden dar y quitar likes
- RN10: Los planes se ordenan por cantidad de likes
- RN11: Los usuarios pueden eliminar sus publicaciones
- RN12: El administrador puede eliminar cualquier publicación
- RN13: Las actividades deberán almacenar coordenadas geográficas
- RN14: La ubicación de las actividades será seleccionada mediante un mapa interactivo

## 3.2 Requerimientos funcionales

### 3.2.1 Usuarios

- RF01: Registrar usuario
- RF02: Autenticar usuario

### 3.2.2 Planes de viaje

- RF03: Crear plan de viaje
- RF04: Editar plan
- RF05: Eliminar plan
- RF06: Validar límite de planes

### 3.2.3 Actividades dentro del plan

- RF07: Agregar actividad a plan
- RF08: Definir fecha y hora de actividades
- RF09: Modificar duración de actividades
- RF10: Eliminar actividad del plan

### 3.2.4 Actividades

- RF11: Visualizar actividades
- RF12: Visualizar detalles de actividad
- RF13: Filtrar actividades por categoría
- RF14: Buscar actividades
- RF15: Filtrar actividades por prefectura
- RF16: Crear actividades personalizadas
- RF17: Administrar actividades globales
- RF18: Seleccionar ubicación geográfica mediante mapa
- RF19: Visualizar ubicación externa en Google Maps

### 3.2.5 Exploración geográfica

- RF20: Mostrar mapa interactivo de Japón por prefecturas
- RF21: Permitir seleccionar una prefectura y visualizar actividades asociadas
- RF22: Visualizar actividades desde el mapa interactivo

### 3.2.6 Foro

- RF23: Publicar plan
- RF24: Visualizar planes
- RF25: Ordenar por likes
- RF26: Dar like
- RF27: Quitar like
- RF28: Comentar
- RF29: Eliminar publicación propia
- RF30: Moderar publicaciones

## 3.3 Requerimientos no funcionales

- RNF01: El sistema deberá responder a las solicitudes en un tiempo menor a 2 segundos en condiciones normales de uso
- RNF02: Las contraseñas de los usuarios deberán almacenarse utilizando funciones de hash seguras
- RNF03: La interfaz deberá ser responsive y adaptarse a distintos dispositivos

# 4. Casos de uso

- UC01: Crear plan de viaje
- UC02: Gestionar actividades del plan
- UC03: Explorar actividades por mapa
- UC04: Visualizar actividad
- UC05: Crear actividad personalizada
- UC06: Seleccionar ubicación geográfica
- UC07: Publicar plan
- UC08: Dar/Quitar like
- UC09: Comentar plan
- UC10: Moderar contenido
- UC11: Crear actividad global

# 5. Consideraciones finales

El sistema propuesto busca equilibrar funcionalidad, simplicidad y valor para el usuario, incorporando elementos de planificación, exploración geográfica e interacción social.

Este documento servirá como base para las siguientes etapas de diseño, modelado y desarrollo.