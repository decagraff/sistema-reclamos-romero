# API REST - Documentación de Endpoints

## 🌐 Base URL

**Desarrollo:** `http://localhost:5000/api`  
**Producción:** `https://sistema-reclamos.romeroempresas.com/api`

---

## 🔐 Autenticación

La mayoría de endpoints requieren autenticación mediante JWT Token.

**Header requerido:**
```
Authorization: Bearer {token}
```

**Ejemplo:**
```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## 📋 MÓDULO: AUTENTICACIÓN

### POST `/api/auth/register`
Registrar nuevo usuario (cliente)

**Acceso:** Público

**Request Body:**
```json
{
  "email": "cliente@ejemplo.com",
  "password": "MiPassword123!",
  "nombres": "Juan",
  "apellidos": "Pérez García",
  "telefono": "987654321",
  "tipoDocumento": "DNI",
  "numeroDocumento": "12345678",
  "departamento": "Lima"
}
```

**Response 201 Created:**
```json
{
  "success": true,
  "message": "Usuario registrado exitosamente",
  "data": {
    "userId": 1,
    "email": "cliente@ejemplo.com",
    "emailVerificado": false
  }
}
```

**Errores:**
- `400 Bad Request`: Datos inválidos o email ya existe
- `500 Internal Server Error`: Error del servidor

---

### POST `/api/auth/login`
Iniciar sesión

**Acceso:** Público

**Request Body:**
```json
{
  "email": "cliente@ejemplo.com",
  "password": "MiPassword123!"
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "a1b2c3d4e5f6...",
    "expiresIn": 86400,
    "user": {
      "id": 1,
      "email": "cliente@ejemplo.com",
      "nombres": "Juan",
      "apellidos": "Pérez García",
      "rol": "CLIENTE"
    }
  }
}
```

**Errores:**
- `401 Unauthorized`: Credenciales incorrectas
- `403 Forbidden`: Usuario inactivo

---

### POST `/api/auth/refresh`
Refrescar token expirado

**Acceso:** Público

**Request Body:**
```json
{
  "refreshToken": "a1b2c3d4e5f6..."
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 86400
  }
}
```

---

### POST `/api/auth/forgot-password`
Solicitar recuperación de contraseña

**Acceso:** Público

**Request Body:**
```json
{
  "email": "cliente@ejemplo.com"
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Si el email existe, recibirás instrucciones para recuperar tu contraseña"
}
```

---

### POST `/api/auth/reset-password`
Cambiar contraseña con token

**Acceso:** Público

**Request Body:**
```json
{
  "token": "reset-token-uuid",
  "newPassword": "NuevaPassword123!"
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Contraseña actualizada exitosamente"
}
```

---

## 📋 MÓDULO: RECLAMOS

### POST `/api/reclamos`
Crear nuevo reclamo

**Acceso:** Público (sin autenticación) o Autenticado

**Request Body:**
```json
{
  "nombres": "Juan",
  "apellidos": "Pérez García",
  "email": "cliente@ejemplo.com",
  "telefono": "987654321",
  "tipoDocumento": "DNI",
  "numeroDocumento": "12345678",
  "departamento": "Lima",
  "domicilioNotificaciones": "Av. Principal 123",
  "empresaDistribuidora": "Transportes Romero",
  "motivoId": 11,
  "explicacion": "Descripción detallada del problema...",
  "accionRequerida": "Solicito que se revise el caso y se resuelva...",
  "tieneRepresentante": false,
  "esClienteEmpresa": true,
  "numeroSuministro": "SUM-2025-001",
  "archivos": [
    {
      "nombre": "evidencia.pdf",
      "base64": "JVBERi0xLjQKJeLjz9MKMSAwIG9iago8..."
    }
  ]
}
```

**Response 201 Created:**
```json
{
  "success": true,
  "message": "Reclamo registrado exitosamente",
  "data": {
    "id": 1,
    "codigo": "REC-2025-0001",
    "estado": "NUEVO",
    "fechaReclamo": "2025-11-08T10:30:00Z"
  }
}
```

**Errores:**
- `400 Bad Request`: Datos inválidos
- `413 Payload Too Large`: Archivos muy pesados

---

### GET `/api/reclamos`
Listar todos los reclamos (Admin)

**Acceso:** Requiere autenticación (Rol: AGENTE, SUPERVISOR, ADMIN)

**Query Parameters:**
- `page` (default: 1)
- `pageSize` (default: 20, max: 100)
- `estado` (opcional)
- `agenteId` (opcional)
- `fechaInicio` (opcional, formato: YYYY-MM-DD)
- `fechaFin` (opcional)
- `buscar` (búsqueda en código, nombre, email)

**Ejemplo:** `/api/reclamos?page=1&pageSize=20&estado=NUEVO`

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": 1,
        "codigo": "REC-2025-0001",
        "nombres": "Juan Pérez García",
        "email": "cliente@ejemplo.com",
        "estado": {
          "id": 1,
          "nombre": "NUEVO",
          "color": "#3B82F6"
        },
        "motivo": {
          "id": 11,
          "nombre": "Mala calidad de Producto/Servicio"
        },
        "prioridad": "MEDIA",
        "fechaReclamo": "2025-11-08T10:30:00Z",
        "agenteAsignado": null
      }
    ],
    "pagination": {
      "page": 1,
      "pageSize": 20,
      "totalPages": 5,
      "totalItems": 95
    }
  }
}
```

---

### GET `/api/reclamos/{id}`
Ver detalle completo de un reclamo

**Acceso:** Requiere autenticación (Admin) o debe ser el dueño del reclamo (Cliente)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "codigo": "REC-2025-0001",
    "fechaReclamo": "2025-11-08T10:30:00Z",
    "nombres": "Juan",
    "apellidos": "Pérez García",
    "email": "cliente@ejemplo.com",
    "telefono": "987654321",
    "tipoDocumento": "DNI",
    "numeroDocumento": "12345678",
    "departamento": "Lima",
    "domicilioNotificaciones": "Av. Principal 123",
    "empresaDistribuidora": "Transportes Romero",
    "motivo": {
      "id": 11,
      "nombre": "Mala calidad de Producto/Servicio"
    },
    "explicacion": "Descripción detallada...",
    "accionRequerida": "Solicito que se revise...",
    "estado": {
      "id": 2,
      "nombre": "EN REVISIÓN",
      "color": "#F59E0B"
    },
    "prioridad": "MEDIA",
    "agenteAsignado": {
      "id": 5,
      "nombres": "María",
      "apellidos": "González"
    },
    "fechaAsignacion": "2025-11-08T11:00:00Z",
    "archivos": [
      {
        "id": 1,
        "nombreOriginal": "evidencia.pdf",
        "url": "/api/archivos/download/1",
        "tamanioBytes": 245678,
        "fechaSubida": "2025-11-08T10:30:00Z"
      }
    ],
    "comentarios": [
      {
        "id": 1,
        "usuario": "Agente López",
        "contenido": "Estamos revisando su caso...",
        "esInterno": false,
        "fechaCreacion": "2025-11-08T12:00:00Z"
      }
    ],
    "historialEstados": [
      {
        "estadoAnterior": "NUEVO",
        "estadoNuevo": "EN REVISIÓN",
        "usuario": "Supervisor Ramírez",
        "fecha": "2025-11-08T11:00:00Z"
      }
    ]
  }
}
```

**Errores:**
- `404 Not Found`: Reclamo no existe
- `403 Forbidden`: No tiene permisos

---

### GET `/api/reclamos/consultar`
Consulta pública de reclamo por código

**Acceso:** Público (sin autenticación)

**Query Parameters:**
- `codigo` (requerido)

**Ejemplo:** `/api/reclamos/consultar?codigo=REC-2025-0001`

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "codigo": "REC-2025-0001",
    "fechaReclamo": "2025-11-08T10:30:00Z",
    "estado": {
      "nombre": "EN PROCESO",
      "color": "#8B5CF6"
    },
    "motivo": "Mala calidad de Producto/Servicio",
    "respuestasOficiales": [
      {
        "contenido": "Estamos trabajando en su caso...",
        "fecha": "2025-11-08T14:00:00Z"
      }
    ]
  }
}
```

**Errores:**
- `404 Not Found`: Código no existe

---

### GET `/api/reclamos/mis-reclamos`
Ver mis propios reclamos (Cliente autenticado)

**Acceso:** Requiere autenticación (Rol: CLIENTE)

**Query Parameters:**
- `page` (default: 1)
- `pageSize` (default: 10)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": 1,
        "codigo": "REC-2025-0001",
        "motivo": "Mala calidad de Producto/Servicio",
        "estado": {
          "nombre": "EN PROCESO",
          "color": "#8B5CF6"
        },
        "fechaReclamo": "2025-11-08T10:30:00Z",
        "ultimaActualizacion": "2025-11-08T14:00:00Z"
      }
    ],
    "pagination": {
      "page": 1,
      "pageSize": 10,
      "totalPages": 1,
      "totalItems": 3
    }
  }
}
```

---

### PUT `/api/reclamos/{id}/estado`
Cambiar estado de un reclamo

**Acceso:** Requiere autenticación (Rol: AGENTE, SUPERVISOR, ADMIN)

**Request Body:**
```json
{
  "nuevoEstadoId": 3,
  "observaciones": "Se procede a resolver el caso..."
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Estado actualizado exitosamente",
  "data": {
    "estadoAnterior": "EN REVISIÓN",
    "estadoNuevo": "EN PROCESO"
  }
}
```

**Errores:**
- `400 Bad Request`: Cambio de estado inválido
- `403 Forbidden`: No tiene permisos

---

### POST `/api/reclamos/{id}/comentarios`
Agregar comentario a un reclamo

**Acceso:** Requiere autenticación (Admin o dueño del reclamo)

**Request Body:**
```json
{
  "contenido": "Necesito información adicional sobre...",
  "esInterno": false,
  "esRespuestaOficial": true
}
```

**Response 201 Created:**
```json
{
  "success": true,
  "message": "Comentario agregado exitosamente",
  "data": {
    "id": 5,
    "contenido": "Necesito información adicional...",
    "fechaCreacion": "2025-11-08T15:00:00Z"
  }
}
```

---

### POST `/api/reclamos/{id}/asignar`
Asignar reclamo a un agente

**Acceso:** Requiere autenticación (Rol: SUPERVISOR, ADMIN)

**Request Body:**
```json
{
  "agenteId": 5
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Reclamo asignado exitosamente",
  "data": {
    "agenteAsignado": {
      "id": 5,
      "nombres": "María González"
    },
    "fechaAsignacion": "2025-11-08T16:00:00Z"
  }
}
```

---

### POST `/api/reclamos/{id}/archivos`
Subir archivos adicionales a un reclamo

**Acceso:** Requiere autenticación

**Request Body (multipart/form-data):**
```
archivos: [file1.pdf, file2.jpg]
```

**Response 201 Created:**
```json
{
  "success": true,
  "message": "Archivos subidos exitosamente",
  "data": {
    "archivosSubidos": 2,
    "archivos": [
      {
        "id": 10,
        "nombreOriginal": "file1.pdf",
        "url": "/api/archivos/download/10"
      }
    ]
  }
}
```

---

## 📋 MÓDULO: ENCUESTAS

### POST `/api/encuestas`
Crear nueva encuesta

**Acceso:** Requiere autenticación (Rol: SUPERVISOR, ADMIN)

**Request Body:**
```json
{
  "titulo": "Encuesta de Satisfacción Post-Resolución",
  "descripcion": "Queremos conocer su opinión sobre la atención recibida",
  "esPostResolucion": true,
  "preguntas": [
    {
      "textoPregunta": "¿Cómo califica la atención recibida?",
      "tipo": "ESCALA",
      "obligatoria": true,
      "orden": 1,
      "opciones": {
        "min": 1,
        "max": 5,
        "etiquetaMin": "Muy mala",
        "etiquetaMax": "Excelente"
      }
    },
    {
      "textoPregunta": "¿Su problema fue resuelto satisfactoriamente?",
      "tipo": "SI_NO",
      "obligatoria": true,
      "orden": 2
    },
    {
      "textoPregunta": "Comentarios adicionales",
      "tipo": "TEXTO",
      "obligatoria": false,
      "orden": 3
    }
  ]
}
```

**Response 201 Created:**
```json
{
  "success": true,
  "message": "Encuesta creada exitosamente",
  "data": {
    "id": 1,
    "titulo": "Encuesta de Satisfacción Post-Resolución",
    "activa": true,
    "totalPreguntas": 3
  }
}
```

---

### GET `/api/encuestas`
Listar encuestas

**Acceso:** Requiere autenticación (Rol: SUPERVISOR, ADMIN)

**Response 200 OK:**
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "titulo": "Encuesta de Satisfacción Post-Resolución",
      "activa": true,
      "esPostResolucion": true,
      "totalPreguntas": 3,
      "totalRespuestas": 45,
      "fechaCreacion": "2025-10-01T10:00:00Z"
    }
  ]
}
```

---

### GET `/api/encuestas/{id}`
Ver detalle de encuesta

**Acceso:** Requiere autenticación (Admin) o Token de encuesta (Cliente)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "titulo": "Encuesta de Satisfacción Post-Resolución",
    "descripcion": "Queremos conocer su opinión...",
    "preguntas": [
      {
        "id": 1,
        "textoPregunta": "¿Cómo califica la atención recibida?",
        "tipo": "ESCALA",
        "obligatoria": true,
        "orden": 1,
        "opciones": {
          "min": 1,
          "max": 5,
          "etiquetaMin": "Muy mala",
          "etiquetaMax": "Excelente"
        }
      }
    ]
  }
}
```

---

### POST `/api/encuestas/{id}/responder`
Responder encuesta

**Acceso:** Requiere token de encuesta (enviado por email)

**Request Body:**
```json
{
  "reclamoId": 1,
  "token": "encuesta-token-uuid",
  "respuestas": [
    {
      "preguntaId": 1,
      "respuesta": "5"
    },
    {
      "preguntaId": 2,
      "respuesta": "SI"
    },
    {
      "preguntaId": 3,
      "respuesta": "Excelente atención, muy agradecido"
    }
  ],
  "calificacionGeneral": 5
}
```

**Response 201 Created:**
```json
{
  "success": true,
  "message": "Gracias por responder la encuesta",
  "data": {
    "encuestaCompletada": true
  }
}
```

---

### GET `/api/encuestas/{id}/resultados`
Ver resultados de encuesta

**Acceso:** Requiere autenticación (Rol: SUPERVISOR, ADMIN, EJECUTIVO)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "encuestaId": 1,
    "titulo": "Encuesta de Satisfacción Post-Resolución",
    "totalRespuestas": 45,
    "calificacionPromedio": 4.2,
    "resultadosPorPregunta": [
      {
        "preguntaId": 1,
        "textoPregunta": "¿Cómo califica la atención?",
        "tipo": "ESCALA",
        "promedio": 4.2,
        "distribucion": {
          "1": 2,
          "2": 3,
          "3": 8,
          "4": 15,
          "5": 17
        }
      }
    ]
  }
}
```

---

## 📋 MÓDULO: REPORTES

### GET `/api/reportes/dashboard`
Obtener métricas del dashboard

**Acceso:** Requiere autenticación (Rol: AGENTE+)

**Query Parameters:**
- `fechaInicio` (opcional)
- `fechaFin` (opcional)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "totalClientes": 100,
    "totalReclamos": 250,
    "reclamosNuevos": 15,
    "reclamosEnProceso": 45,
    "reclamosPendientes": 20,
    "reclamosSolucionados": 30,
    "reclamosCerrados": 140,
    "satisfaccionPromedio": 4.3,
    "tiempoPromedioResolucionDias": 5.2,
    "slaCumplido": 85,
    "reclamosPorEstado": [
      {
        "estado": "NUEVO",
        "cantidad": 15,
        "porcentaje": 6
      }
    ],
    "reclamosPorMotivo": [
      {
        "motivo": "Mala calidad de servicio",
        "cantidad": 45,
        "porcentaje": 18
      }
    ],
    "tendenciaMensual": [
      {
        "mes": "2025-01",
        "nuevos": 20,
        "resueltos": 18
      }
    ]
  }
}
```

---

### POST `/api/reportes/generar`
Generar reporte personalizado

**Acceso:** Requiere autenticación (Rol: SUPERVISOR, ADMIN, EJECUTIVO)

**Request Body:**
```json
{
  "tipoReporte": "INDECOPI",
  "formato": "PDF",
  "fechaInicio": "2025-01-01",
  "fechaFin": "2025-11-08",
  "filtros": {
    "estados": ["RESUELTO", "CERRADO"],
    "motivos": [11, 12]
  }
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Reporte generado exitosamente",
  "data": {
    "urlDescarga": "/api/reportes/download/temp-uuid-12345",
    "nombreArchivo": "Reporte_Indecopi_2025.pdf",
    "expiraEn": "2025-11-08T18:00:00Z"
  }
}
```

---

### GET `/api/reportes/download/{tempId}`
Descargar reporte generado

**Acceso:** Requiere autenticación

**Response:** Stream del archivo (PDF o Excel)

---

### GET `/api/reportes/estadisticas`
Estadísticas avanzadas

**Acceso:** Requiere autenticación (Rol: EJECUTIVO, ADMIN)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "agentesMasEfectivos": [
      {
        "agenteId": 5,
        "nombre": "María González",
        "reclamosResueltos": 45,
        "tiempoPromedioResolucion": 4.2,
        "satisfaccionPromedio": 4.5
      }
    ],
    "horasPicoReclamos": [
      {
        "hora": 10,
        "cantidad": 25
      }
    ],
    "motivosMasFrecuentes": [
      {
        "motivo": "Mala calidad de servicio",
        "cantidad": 45,
        "tendencia": "creciente"
      }
    ]
  }
}
```

---

## 📋 MÓDULO: USUARIOS

### GET `/api/usuarios`
Listar usuarios

**Acceso:** Requiere autenticación (Rol: ADMIN)

**Query Parameters:**
- `rol` (opcional)
- `page` (default: 1)
- `pageSize` (default: 20)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": 1,
        "email": "admin@romeroempresas.com",
        "nombres": "Administrador",
        "apellidos": "Sistema",
        "rol": "ADMINISTRADOR",
        "activo": true,
        "fechaRegistro": "2025-01-01T00:00:00Z"
      }
    ],
    "pagination": {
      "page": 1,
      "pageSize": 20,
      "totalItems": 15
    }
  }
}
```

---

### GET `/api/usuarios/{id}`
Ver perfil de usuario

**Acceso:** Requiere autenticación (Admin o propio usuario)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "email": "cliente@ejemplo.com",
    "nombres": "Juan",
    "apellidos": "Pérez García",
    "telefono": "987654321",
    "tipoDocumento": "DNI",
    "numeroDocumento": "12345678",
    "departamento": "Lima",
    "domicilio": "Av. Principal 123",
    "rol": "CLIENTE",
    "esCliente": true,
    "numeroSuministro": "SUM-2025-001",
    "emailVerificado": true,
    "fechaRegistro": "2025-10-01T10:00:00Z",
    "ultimoAcceso": "2025-11-08T09:30:00Z"
  }
}
```

---

### PUT `/api/usuarios/{id}`
Actualizar perfil

**Acceso:** Requiere autenticación (Propio usuario o Admin)

**Request Body:**
```json
{
  "nombres": "Juan Carlos",
  "apellidos": "Pérez García",
  "telefono": "987654321",
  "domicilio": "Nueva dirección 456"
}
```

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Perfil actualizado exitosamente"
}
```

---

### DELETE `/api/usuarios/{id}`
Eliminar usuario (soft delete)

**Acceso:** Requiere autenticación (Rol: ADMIN)

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Usuario desactivado exitosamente"
}
```

---

## 📋 MÓDULO: NOTIFICACIONES

### GET `/api/notificaciones`
Listar mis notificaciones

**Acceso:** Requiere autenticación

**Query Parameters:**
- `page` (default: 1)
- `pageSize` (default: 20)
- `soloNoLeidas` (default: false)

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": 1,
        "tipo": "SISTEMA",
        "asunto": "Cambio de estado en su reclamo",
        "contenido": "Su reclamo REC-2025-0001 ha cambiado a EN PROCESO",
        "reclamoId": 1,
        "leida": false,
        "fechaCreacion": "2025-11-08T14:00:00Z"
      }
    ],
    "noLeidas": 5,
    "pagination": {
      "page": 1,
      "pageSize": 20,
      "totalItems": 25
    }
  }
}
```

---

### PUT `/api/notificaciones/{id}/leer`
Marcar notificación como leída

**Acceso:** Requiere autenticación

**Response 200 OK:**
```json
{
  "success": true,
  "message": "Notificación marcada como leída"
}
```

---

### GET `/api/notificaciones/no-leidas`
Contar notificaciones no leídas

**Acceso:** Requiere autenticación

**Response 200 OK:**
```json
{
  "success": true,
  "data": {
    "cantidad": 5
  }
}
```

---

## 🔔 MÓDULO: SIGNALR (Solo Premium)

### Hub: `/hubs/chat`

**Eventos del servidor al cliente:**

#### `ReceiveMessage`
Mensaje nuevo en chat
```json
{
  "reclamoId": 1,
  "usuarioId": 5,
  "usuario": "Agente López",
  "mensaje": "Hola, ¿en qué puedo ayudarte?",
  "fecha": "2025-11-08T10:00:00Z"
}
```

#### `UserOnline`
Usuario conectado
```json
{
  "usuarioId": 5,
  "nombre": "Agente López"
}
```

#### `UserOffline`
Usuario desconectado
```json
{
  "usuarioId": 5
}
```

**Métodos del cliente al servidor:**

#### `JoinReclamoGroup`
Unirse al canal de un reclamo
```javascript
connection.invoke("JoinReclamoGroup", reclamoId);
```

#### `SendMessage`
Enviar mensaje
```javascript
connection.invoke("SendMessage", reclamoId, mensaje);
```

---

## 📝 Códigos de Estado HTTP

- **200 OK**: Operación exitosa
- **201 Created**: Recurso creado
- **204 No Content**: Operación exitosa sin contenido
- **400 Bad Request**: Datos inválidos
- **401 Unauthorized**: No autenticado
- **403 Forbidden**: Sin permisos
- **404 Not Found**: Recurso no encontrado
- **409 Conflict**: Conflicto (ej: email ya existe)
- **413 Payload Too Large**: Archivos muy grandes
- **500 Internal Server Error**: Error del servidor

---

## 📝 Formato de Respuesta Estándar

### Respuesta Exitosa
```json
{
  "success": true,
  "message": "Mensaje descriptivo opcional",
  "data": { /* datos */ }
}
```

### Respuesta de Error
```json
{
  "success": false,
  "error": {
    "code": "INVALID_DATA",
    "message": "Los datos proporcionados son inválidos",
    "details": {
      "email": "El email no tiene un formato válido",
      "password": "La contraseña debe tener al menos 8 caracteres"
    }
  }
}
```

---

## 🔒 Limitación de Peticiones (Rate Limiting)

**Límites por endpoint:**
- Endpoints públicos: 100 peticiones por 15 minutos por IP
- Endpoints autenticados: 1000 peticiones por hora por usuario
- Subida de archivos: 10 peticiones por hora por usuario

**Header de respuesta cuando se excede:**
```
HTTP 429 Too Many Requests
Retry-After: 900
```

---

**Documento actualizado:** Noviembre 2025  
**Versión:** 1.0
