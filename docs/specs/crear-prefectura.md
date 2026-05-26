# Feature Specification – Crear Prefectura

## Sistema: Planificador de Viajes a Japón

# 1. Objetivo

Permitir a un administrador crear nuevas prefecturas dentro del sistema.

Las prefecturas serán utilizadas para:

- clasificar actividades
- filtrar actividades
- explorar actividades mediante mapa interactivo

# 2. Actores

- Administrador

# 3. Reglas de negocio

- Solo administradores pueden crear prefecturas
- El nombre de la prefectura debe ser único
- El nombre es obligatorio
- Una prefectura no puede eliminarse si tiene actividades asociadas
- Las prefecturas serán visibles para todos los usuarios

# 4. Flujo funcional

## 4.1 Crear prefectura

1. El administrador accede a “Administrar prefecturas”
2. El sistema muestra formulario de creación
3. El administrador ingresa el nombre
4. Confirma la operación
5. El sistema valida los datos
6. El sistema registra la prefectura
7. El sistema muestra mensaje de éxito

# 5. Componentes frontend involucrados

## Components

```text
prefectures
create-prefecture
```

Responsabilidad:
- mostrar listado
- renderizar formulario
- manejar validaciones visuales

---

## Services

```text
prefectures.service.ts
```

Responsabilidad:
- comunicación HTTP con backend
- gestión de prefecturas

---

## Models

```text
prefecture.model.ts
```

# 6. Endpoints involucrados

## POST /prefectures

Crea una prefectura.

---

## GET /prefectures

Obtiene todas las prefecturas.

# 7. Modelo de datos involucrado

## Tabla Prefectura

Campos utilizados:

- id
- nombre

---

## Relación con Actividad

- una prefectura puede contener múltiples actividades

# 8. Validaciones frontend

- nombre obligatorio
- longitud máxima del nombre
- eliminar espacios innecesarios

# 9. Validaciones backend

- usuario autenticado
- usuario administrador
- nombre único
- sanitización de datos

# 10. Casos borde

## 10.1 Nombre duplicado

Resultado:
- backend rechaza solicitud
- mostrar mensaje de error

---

## 10.2 Usuario sin permisos

Resultado:
- backend responde 403 Forbidden

---

## 10.3 Nombre vacío

Resultado:
- impedir envío del formulario

# 11. Criterios de aceptación

- el administrador puede crear prefecturas
- las prefecturas quedan registradas correctamente
- el sistema impide nombres duplicados
- las prefecturas aparecen en listados y filtros
- las prefecturas pueden utilizarse en actividades

# 12. Consideraciones técnicas

- utilizar Angular standalone components
- utilizar Reactive Forms
- centralizar llamadas HTTP en services
- proteger endpoints mediante JWT
- validar permisos en backend
