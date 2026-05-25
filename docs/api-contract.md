# `docs/api-contract.md`

# Especificación de API REST

## Sistema: Planificador de Viajes a Japón

# 1. Introducción

## 1.1 Propósito

El presente documento describe los contratos de la API REST del sistema “Planificador de Viajes a Japón”.

La API permitirá la comunicación entre el frontend desarrollado en Angular y el backend desarrollado en Node.js.

# 2. Consideraciones generales

- La API seguirá arquitectura REST
- El intercambio de información se realizará en formato JSON
- Los endpoints protegidos requerirán autenticación mediante JWT
- El usuario autenticado será obtenido desde el token JWT
- Las operaciones de actualización parcial utilizarán el método PATCH
- Las coordenadas geográficas serán utilizadas para integración con Leaflet y OpenStreetMap
- Google Maps será utilizado únicamente como navegación externa

# 3. Autenticación

## POST /auth/login

Autentica un usuario dentro del sistema.

### Request

```json
{
  "usuario": "juan",
  "password": "123456"
}
```

### Response

```json
{
  "token": "jwt-token",
  "usuario": {
    "id": 1,
    "usuario": "juan",
    "rol": "USUARIO"
  }
}
```

---

## POST /auth/register

Registra un nuevo usuario.

### Request

```json
{
  "usuario": "juan",
  "password": "123456"
}
```

### Response

```json
{
  "message": "Usuario registrado correctamente"
}
```

# 4. Actividades

## POST /activities/global

Crea una actividad global.

### Request

```json
{
  "nombre": "Visita a Senso-ji",
  "duracion": 120,
  "costo": 0,
  "direccion": "Asakusa, Tokyo",
  "latitud": 35.7148,
  "longitud": 139.7967,
  "imagen": "https://...",
  "descripcion": "Templo histórico",
  "categoria": "Cultural",
  "prefecturaId": 13
}
```

### Response

```json
{
  "message": "Actividad creada correctamente"
}
```

---

## POST /activities/private

Crea una actividad personalizada.

### Request

```json
{
  "nombre": "Cena tradicional",
  "duracion": 90,
  "costo": 40,
  "direccion": "Kyoto",
  "latitud": 35.0116,
  "longitud": 135.7681,
  "descripcion": "Cena japonesa",
  "categoria": "Gastronomía",
  "prefecturaId": 26
}
```

### Response

```json
{
  "message": "Actividad creada correctamente"
}
```

---

## GET /activities

Obtiene actividades globales y actividades privadas del usuario autenticado aplicando filtros opcionales.

### Query Params

- categoria
- prefecturaId
- nombre
- esGlobal

### Ejemplo

```http
GET /activities?categoria=Cultural&prefecturaId=13
```

### Response

```json
[
  {
    "id": 1,
    "nombre": "Visita a Senso-ji",
    "duracion": 120,
    "costo": 0,
    "direccion": "Asakusa, Tokyo",
    "latitud": 35.7148,
    "longitud": 139.7967,
    "categoria": "Cultural",
    "esGlobal": true
  }
]
```

---

## GET /activities/:id

Obtiene una actividad específica.

### Response

```json
{
  "id": 1,
  "nombre": "Visita a Senso-ji",
  "duracion": 120,
  "costo": 0,
  "direccion": "Asakusa, Tokyo",
  "latitud": 35.7148,
  "longitud": 139.7967,
  "descripcion": "Templo histórico",
  "categoria": "Cultural"
}
```

---

## PATCH /activities/:id

Actualiza parcialmente una actividad.

### Request

```json
{
  "nombre": "Actividad actualizada",
  "duracion": 150
}
```

### Consideraciones

- Todos los campos son opcionales
- Solo se modificarán los campos enviados en la solicitud

### Response

```json
{
  "message": "Actividad modificada correctamente"
}
```

---

## DELETE /activities/:id

Elimina una actividad.

### Response

```json
{
  "message": "Actividad eliminada correctamente"
}
```

# 5. Planes

## POST /plans

Crea un nuevo plan.

### Request

```json
{
  "nombre": "Viaje Japón 2027",
  "fechaDesde": "2027-04-10",
  "fechaHasta": "2027-04-25"
}
```

### Response

```json
{
  "id": 1,
  "message": "Plan creado correctamente"
}
```

---

## GET /plans

Obtiene los planes del usuario autenticado.

### Response

```json
[
  {
    "id": 1,
    "nombre": "Viaje Japón 2027",
    "fechaDesde": "2027-04-10",
    "fechaHasta": "2027-04-25"
  }
]
```

---

## GET /plans/:id

Obtiene un plan específico junto con sus actividades.

### Response

```json
{
  "id": 1,
  "nombre": "Viaje Japón 2027",
  "actividades": [
    {
      "actividadId": 5,
      "nombre": "Senso-ji",
      "fecha": "2027-04-12",
      "horaDesde": "10:00",
      "horaHasta": "12:00"
    }
  ]
}
```

---

## PATCH /plans/:id

Actualiza parcialmente un plan.

### Request

```json
{
  "nombre": "Viaje Japón Primavera"
}
```

### Consideraciones

- Todos los campos son opcionales
- Solo se actualizarán los campos enviados

### Response

```json
{
  "message": "Plan actualizado correctamente"
}
```

---

## DELETE /plans/:id

Elimina un plan.

### Response

```json
{
  "message": "Plan eliminado correctamente"
}
```

# 6. Actividades dentro del plan

## POST /plans/:id/activities

Agrega una actividad a un plan.

### Request

```json
{
  "actividadId": 5,
  "fecha": "2027-04-12",
  "horaDesde": "10:00",
  "horaHasta": "12:00"
}
```

### Response

```json
{
  "message": "Actividad agregada correctamente"
}
```

---

## PATCH /plans/:planId/activities/:activityId

Actualiza parcialmente una actividad planificada.

### Request

```json
{
  "horaDesde": "14:00",
  "horaHasta": "16:00"
}
```

### Consideraciones

- Todos los campos son opcionales
- Solo se actualizarán los campos enviados

### Response

```json
{
  "message": "Actividad del plan modificada correctamente"
}
```

---

## DELETE /plans/:planId/activities/:activityId

Elimina una actividad del plan.

### Response

```json
{
  "message": "Actividad eliminada del plan correctamente"
}
```

# 7. Foro

## POST /publications

Publica un plan en el foro.

### Request

```json
{
  "planId": 1
}
```

### Response

```json
{
  "message": "Plan publicado correctamente"
}
```

---

## GET /publications

Obtiene publicaciones ordenadas por likes.

### Response

```json
[
  {
    "id": 1,
    "likes": 25
  }
]
```

---

## DELETE /publications/:id

Elimina una publicación.

### Response

```json
{
  "message": "Publicación eliminada correctamente"
}
```

---

## POST /publications/:id/comments

Agrega un comentario.

### Request

```json
{
  "contenido": "Excelente plan"
}
```

### Response

```json
{
  "message": "Comentario agregado correctamente"
}
```

---

## DELETE /comments/:id

Elimina un comentario.

### Response

```json
{
  "message": "Comentario eliminado correctamente"
}
```

---

## POST /publications/:id/likes

Agrega un like.

### Response

```json
{
  "message": "Like agregado correctamente"
}
```

---

## DELETE /publications/:id/likes

Elimina un like.

### Response

```json
{
  "message": "Like eliminado correctamente"
}
```

# 8. Consideraciones finales

La API fue diseñada siguiendo principios REST y separación de responsabilidades entre frontend y backend.

El sistema prioriza simplicidad, mantenibilidad y extensibilidad, permitiendo futuras funcionalidades relacionadas con exploración geográfica, interacción social y recomendaciones basadas en ubicación.