# Flujos del Sistema - Diagramas Completos

## 🔄 Flujo General del Sistema

```mermaid
graph TB
    Start[Cliente necesita hacer reclamo] --> Decision{¿Tiene cuenta?}
    
    Decision -->|No| FormPublico[Formulario Público]
    Decision -->|Sí| Login[Login al Portal]
    
    FormPublico --> SubmitForm[Envía formulario]
    Login --> Portal[Portal del Cliente]
    Portal --> FormPrivado[Crear nuevo reclamo]
    FormPrivado --> SubmitForm
    
    SubmitForm --> Validacion{¿Datos válidos?}
    Validacion -->|No| Error[Mostrar errores]
    Error --> FormPublico
    
    Validacion -->|Sí| GenerarCodigo[Generar código único REC-2025-XXXX]
    GenerarCodigo --> GuardarBD[(Guardar en BD)]
    GuardarBD --> EmailCliente[Enviar email confirmación]
    EmailCliente --> AlertaAdmin[Alertar administradores]
    
    AlertaAdmin --> PanelAdmin[Panel Administrativo]
    PanelAdmin --> AsignarAgente[Supervisor asigna a agente]
    AsignarAgente --> EmailAgente[Notificar al agente]
    
    EmailAgente --> Procesar[Agente procesa reclamo]
    Procesar --> CambioEstado[Cambiar estado]
    CambioEstado --> EmailCambioEstado[Notificar cliente]
    
    Procesar --> Responder[Agregar respuesta]
    Responder --> EmailRespuesta[Notificar cliente]
    
    Procesar --> Resolver{¿Resuelto?}
    Resolver -->|No| Procesar
    Resolver -->|Sí| MarcarResuelto[Marcar como RESUELTO]
    
    MarcarResuelto --> EmailResolucion[Notificar cliente]
    EmailResolucion --> EnviarEncuesta[Enviar encuesta automática]
    
    EnviarEncuesta --> ClienteEvalua{¿Cliente responde?}
    ClienteEvalua -->|Sí| GuardarEncuesta[(Guardar respuesta)]
    ClienteEvalua -->|No| Recordatorio[Recordatorio en 3 días]
    
    GuardarEncuesta --> Cerrar[Cerrar reclamo]
    Recordatorio --> ClienteEvalua
    
    Cerrar --> End[Fin del proceso]
```

---

## 📝 Flujo 1: Registro de Reclamo (Público)

```mermaid
sequenceDiagram
    participant C as Cliente
    participant W as Formulario Web
    participant API as Backend API
    participant BD as Base de Datos
    participant Email as Servicio Email
    participant Admin as Panel Admin
    
    C->>W: Ingresa a página de reclamos
    W->>C: Muestra formulario
    
    C->>W: Llena datos y adjunta archivos
    W->>W: Validación frontend
    
    C->>W: Click en "Enviar"
    W->>API: POST /api/reclamos
    
    API->>API: Validar datos
    API->>API: Generar código único
    API->>BD: INSERT reclamo
    BD-->>API: Reclamo guardado (ID: 1)
    
    API->>BD: INSERT archivos
    API->>BD: INSERT notificación
    
    API->>Email: Enviar confirmación al cliente
    Email-->>C: Email con código REC-2025-0001
    
    API->>Email: Alertar administradores
    Email-->>Admin: Email de nuevo reclamo
    
    API-->>W: 201 Created + código
    W->>C: Muestra mensaje de éxito y código
    
    Note over C: Cliente puede consultar estado<br/>con el código recibido
```

---

## 🔐 Flujo 2: Login y Portal del Cliente

```mermaid
sequenceDiagram
    participant C as Cliente
    participant UI as Frontend
    participant API as Backend API
    participant BD as Base de Datos
    
    C->>UI: Ingresa email y contraseña
    UI->>API: POST /api/auth/login
    
    API->>BD: SELECT usuario WHERE email
    BD-->>API: Usuario encontrado
    
    API->>API: Verificar password_hash
    
    alt Password correcto
        API->>API: Generar JWT token
        API-->>UI: 200 OK + token
        UI->>UI: Guardar token en localStorage
        UI->>C: Redirigir a Dashboard
        
        C->>UI: Ver mis reclamos
        UI->>API: GET /api/reclamos/mis-reclamos<br/>(Header: Authorization: Bearer token)
        API->>API: Validar token
        API->>BD: SELECT reclamos WHERE usuario_id
        BD-->>API: Lista de reclamos
        API-->>UI: 200 OK + reclamos[]
        UI->>C: Muestra lista de reclamos
    else Password incorrecto
        API-->>UI: 401 Unauthorized
        UI->>C: Mostrar error
    end
```

---

## 👨‍💼 Flujo 3: Gestión Interna de Reclamo

```mermaid
stateDiagram-v2
    [*] --> NUEVO: Cliente registra reclamo
    
    NUEVO --> EN_REVISION: Supervisor revisa
    note right of EN_REVISION
        - Supervisor evalúa prioridad
        - Asigna a agente
        - Notifica por email
    end note
    
    EN_REVISION --> EN_PROCESO: Agente acepta caso
    note right of EN_PROCESO
        - Agente investiga
        - Agrega comentarios internos
        - Solicita información si necesita
    end note
    
    EN_PROCESO --> ESPERANDO_CLIENTE: Necesita info del cliente
    note right of ESPERANDO_CLIENTE
        - Email automático al cliente
        - Espera respuesta
        - Timer de seguimiento
    end note
    
    ESPERANDO_CLIENTE --> EN_PROCESO: Cliente responde
    
    EN_PROCESO --> RESUELTO: Agente resuelve
    note right of RESUELTO
        - Agente marca como resuelto
        - Agrega solución/respuesta
        - Email automático al cliente
        - Encuesta automática enviada
    end note
    
    RESUELTO --> CERRADO: Cliente satisfecho
    note right of CERRADO
        - Cliente responde encuesta positiva
        - O pasan 7 días sin reclamo
        - Estado final
    end note
    
    RESUELTO --> REABIERTO: Cliente no satisfecho
    note right of REABIERTO
        - Cliente indica no estar conforme
        - Vuelve a EN_PROCESO
        - Asignado a supervisor
    end note
    
    REABIERTO --> EN_PROCESO: Supervisor reasigna
    
    EN_REVISION --> RECHAZADO: No procede
    note right of RECHAZADO
        - Con justificación obligatoria
        - Email al cliente explicando
        - Estado final
    end note
    
    CERRADO --> [*]
    RECHAZADO --> [*]
```

---

## 📊 Flujo 4: Envío de Encuesta Post-Resolución

```mermaid
flowchart TD
    A[Agente marca reclamo como RESUELTO] --> B{¿Ya se envió<br/>encuesta?}
    
    B -->|Sí| Z[No hacer nada]
    B -->|No| C[Sistema detecta cambio a RESUELTO]
    
    C --> D[Obtener encuesta activa<br/>de tipo post-resolución]
    D --> E{¿Existe<br/>encuesta?}
    
    E -->|No| F[Log de advertencia]
    E -->|Sí| G[Generar link único<br/>con token]
    
    G --> H[Crear registro en<br/>encuestas_respuestas<br/>estado: PENDIENTE]
    
    H --> I[Preparar email con link]
    I --> J[Enviar email al cliente]
    
    J --> K{Email<br/>enviado OK?}
    K -->|No| L[Reintentar en 5 min]
    K -->|Sí| M[Marcar como enviada]
    
    L --> N{¿3 intentos<br/>fallidos?}
    N -->|Sí| O[Alerta a admin]
    N -->|No| J
    
    M --> P[Esperar respuesta del cliente]
    P --> Q{¿Cliente<br/>respondió?}
    
    Q -->|Sí| R[Guardar respuestas en BD]
    R --> S[Marcar encuesta como COMPLETADA]
    
    Q -->|No después<br/>de 3 días| T[Enviar recordatorio]
    T --> U{¿Ya pasaron<br/>7 días?}
    
    U -->|No| P
    U -->|Sí| V[Marcar como EXPIRADA]
    
    S --> W[Cerrar reclamo automáticamente]
    V --> W
    
    W --> X[Estado final: CERRADO]
```

---

## 🔔 Flujo 5: Sistema de Notificaciones

```mermaid
graph TB
    Event[Evento del Sistema] --> TipoEvento{Tipo de Evento}
    
    TipoEvento -->|Nuevo Reclamo| N1[Notif: Cliente + Admins]
    TipoEvento -->|Cambio Estado| N2[Notif: Cliente + Agente]
    TipoEvento -->|Nueva Respuesta| N3[Notif: Cliente]
    TipoEvento -->|Asignación| N4[Notif: Agente asignado]
    TipoEvento -->|Vencimiento SLA| N5[Notif: Supervisor + Agente]
    
    N1 --> CrearNotif[Crear registro en tabla notificaciones]
    N2 --> CrearNotif
    N3 --> CrearNotif
    N4 --> CrearNotif
    N5 --> CrearNotif
    
    CrearNotif --> Cola[Agregar a cola de envío]
    Cola --> Procesador[Procesador de notificaciones<br/>Job cada 1 minuto]
    
    Procesador --> Obtener[Obtener notificaciones<br/>pendientes enviada=FALSE]
    
    Obtener --> Iterar[Iterar cada notificación]
    Iterar --> Template[Cargar template de email]
    Template --> Reemplazar[Reemplazar variables]
    
    Reemplazar --> Enviar[Enviar vía SendGrid/Mailgun]
    
    Enviar --> Resultado{¿Enviado OK?}
    
    Resultado -->|Sí| ActualizarOK[UPDATE enviada=TRUE<br/>fecha_envio=NOW]
    Resultado -->|No| ActualizarError[UPDATE error=mensaje]
    
    ActualizarError --> Reintentos{¿Menos de<br/>3 reintentos?}
    Reintentos -->|Sí| ReintentosProgramar[Reintentar en siguiente ejecución]
    Reintentos -->|No| AlertaAdmin[Alertar a administrador]
    
    ActualizarOK --> Fin[Fin]
    ReintentosProgramar --> Fin
    AlertaAdmin --> Fin
```

---

## 📱 Flujo 6: Consulta Pública de Estado

```mermaid
sequenceDiagram
    participant C as Cliente
    participant UI as Página Pública
    participant API as Backend API
    participant BD as Base de Datos
    
    C->>UI: Ingresa a "Consultar Estado"
    UI->>C: Muestra formulario con campo código
    
    C->>UI: Ingresa código: REC-2025-0001
    UI->>API: GET /api/reclamos/consultar?codigo=REC-2025-0001
    
    API->>BD: SELECT reclamo WHERE codigo
    
    alt Reclamo encontrado
        BD-->>API: Datos del reclamo
        API->>BD: SELECT estado actual
        API->>BD: SELECT historial_estados
        API->>BD: SELECT comentarios públicos
        
        API-->>UI: 200 OK + datos públicos
        UI->>C: Muestra información:<br/>- Estado actual<br/>- Fecha de registro<br/>- Respuestas oficiales<br/>- Próximos pasos
    else Código no existe
        BD-->>API: No encontrado
        API-->>UI: 404 Not Found
        UI->>C: Mensaje: "Código no encontrado"
    end
```

---

## 📁 Flujo 7: Subida de Archivos

```mermaid
flowchart LR
    A[Cliente selecciona archivos] --> B{Validar<br/>Frontend}
    
    B -->|Formato inválido| C[Mostrar error]
    B -->|Tamaño > 5MB| C
    B -->|Más de 5 archivos| C
    
    B -->|OK| D[Convertir a Base64<br/>o FormData]
    
    D --> E[POST /api/archivos/upload]
    E --> F[Backend recibe archivos]
    
    F --> G{Validar<br/>Backend}
    G -->|Error| H[400 Bad Request]
    
    G -->|OK| I[Generar nombre único<br/>UUID + extensión]
    I --> J[Guardar en storage<br/>/uploads/2025/11/]
    
    J --> K{¿Guardado OK?}
    K -->|No| L[500 Error servidor]
    
    K -->|Sí| M[INSERT en tabla archivos]
    M --> N[Asociar a reclamo_id]
    
    N --> O[Retornar info del archivo:<br/>- ID<br/>- URL<br/>- Nombre]
    
    O --> P[Frontend muestra<br/>archivo subido]
    
    C --> End[Fin]
    H --> End
    L --> End
    P --> End
```

---

## 🔄 Flujo 8: Cambio de Estado con Validaciones

```mermaid
graph TD
    A[Agente/Admin solicita<br/>cambiar estado] --> B{¿Tiene<br/>permisos?}
    
    B -->|No| C[403 Forbidden]
    B -->|Sí| D{¿Cambio<br/>válido?}
    
    D -->|No| E[400 Bad Request<br/>Ej: CERRADO → NUEVO]
    
    D -->|Sí| F{¿Requiere<br/>comentario?}
    
    F -->|Sí y no hay| G[400 Debe agregar comentario]
    F -->|No o ya tiene| H[UPDATE reclamos<br/>estado_id = nuevo]
    
    H --> I[INSERT historial_estados]
    I --> J{¿Estado es<br/>RESUELTO?}
    
    J -->|Sí| K[Registrar fecha_resolucion]
    K --> L[Calcular SLA cumplido]
    L --> M[Programar envío encuesta]
    
    J -->|No| N{¿Estado es<br/>CERRADO?}
    
    N -->|Sí| O[Registrar fecha_cierre]
    N -->|No| P[Solo actualizar estado]
    
    M --> Q[Crear notificación]
    O --> Q
    P --> Q
    
    Q --> R[Enviar email cliente]
    R --> S[200 OK]
    
    C --> End[Fin]
    E --> End
    G --> End
    S --> End
```

---

## 📈 Flujo 9: Generación de Reportes

```mermaid
sequenceDiagram
    participant A as Admin/Supervisor
    participant UI as Dashboard
    participant API as Backend
    participant BD as PostgreSQL
    participant Export as Librería Export
    
    A->>UI: Click en "Generar Reporte"
    UI->>A: Muestra opciones:<br/>- Tipo: Indecopi/General<br/>- Fecha inicio/fin<br/>- Formato: PDF/Excel
    
    A->>UI: Selecciona opciones y confirma
    UI->>API: POST /api/reportes/generar
    
    API->>API: Validar permisos
    API->>BD: Query compleja con filtros
    
    Note over BD: SELECT reclamos<br/>JOIN estados, usuarios, motivos<br/>WHERE fecha BETWEEN x AND y<br/>ORDER BY fecha DESC
    
    BD-->>API: Datos (puede ser 1000+ registros)
    
    API->>API: Procesar y agrupar datos
    
    alt Formato PDF
        API->>Export: Generar PDF con datos
        Export-->>API: Archivo PDF en memoria
    else Formato Excel
        API->>Export: Generar XLSX con datos
        Export-->>API: Archivo XLSX en memoria
    end
    
    API->>API: Guardar archivo temporal
    API-->>UI: 200 OK + URL descarga
    
    UI->>A: Botón "Descargar Reporte"
    A->>UI: Click descargar
    UI->>API: GET /api/reportes/download/temp-file-uuid
    API-->>UI: Stream del archivo
    UI->>A: Descarga iniciada
    
    Note over API: Job limpia archivos temp<br/>después de 1 hora
```

---

## 🎯 Flujo 10: Chat en Tiempo Real (Solo Premium)

```mermaid
sequenceDiagram
    participant C as Cliente
    participant UI as Frontend React
    participant SignalR as SignalR Hub
    participant API as Backend
    participant BD as Base de Datos
    
    C->>UI: Abre detalle de reclamo
    UI->>SignalR: Conectar WebSocket
    SignalR-->>UI: Conexión establecida
    
    UI->>SignalR: JoinGroup(reclamoId)
    
    Note over UI,SignalR: Cliente conectado a canal<br/>del reclamo específico
    
    C->>UI: Escribe mensaje y envía
    UI->>API: POST /api/mensajes
    
    API->>BD: INSERT comentario
    BD-->>API: Comentario guardado (ID: 123)
    
    API->>SignalR: SendToGroup(reclamoId, mensaje)
    
    SignalR-->>UI: Broadcast mensaje a todos<br/>conectados al grupo
    
    UI->>C: Muestra mensaje en tiempo real
    
    Note over C: Agente recibe notificación<br/>instantánea si está conectado
    
    alt Agente responde
        Note over SignalR: Mismo flujo pero desde<br/>panel de agente
        SignalR-->>UI: Mensaje del agente
        UI->>C: Notificación y mensaje visible
    end
    
    C->>UI: Cierra ventana
    UI->>SignalR: LeaveGroup(reclamoId)
    UI->>SignalR: Desconectar
```

---

## 🔐 Flujo 11: Recuperación de Contraseña

```mermaid
flowchart TD
    A[Cliente: "Olvidé mi contraseña"] --> B[Ingresa email]
    B --> C[POST /api/auth/forgot-password]
    
    C --> D{¿Email<br/>existe?}
    
    D -->|No| E[Responder OK de todos modos<br/>seguridad: no revelar si email existe]
    D -->|Sí| F[Generar token único<br/>UUID + timestamp]
    
    F --> G[UPDATE usuarios<br/>SET reset_token, reset_expiry]
    
    G --> H[Crear link:<br/>https://sistema.com/reset?token=XXX]
    
    H --> I[Enviar email con link]
    I --> J[Mostrar mensaje:<br/>Revisa tu email]
    
    E --> J
    
    J --> K[Cliente abre email]
    K --> L[Click en link]
    
    L --> M[GET /reset-password?token=XXX]
    M --> N{¿Token<br/>válido?}
    
    N -->|Expirado| O[Error: Link expirado]
    N -->|Inválido| O
    N -->|OK| P[Formulario nueva contraseña]
    
    P --> Q[Cliente ingresa nueva password]
    Q --> R[POST /api/auth/reset-password]
    
    R --> S[Validar token nuevamente]
    S --> T[Hashear nueva password]
    T --> U[UPDATE usuarios<br/>password_hash]
    U --> V[Limpiar reset_token]
    
    V --> W[Enviar email confirmación]
    W --> X[Redirigir a login]
    
    O --> End
    X --> End
```

---

## ⏰ Flujo 12: Jobs Automáticos (Background Tasks)

```mermaid
gantt
    title Tareas Programadas del Sistema
    dateFormat HH:mm
    axisFormat %H:%M
    
    section Cada Minuto
    Procesar notificaciones pendientes    :00:00, 1m
    
    section Cada 5 Minutos
    Verificar SLA vencidos                :00:00, 5m
    Reintentar emails fallidos            :00:05, 5m
    
    section Cada Hora
    Limpiar archivos temporales           :00:00, 1h
    Actualizar estadísticas caché         :00:00, 1h
    
    section Diario (2 AM)
    Backup de base de datos               :02:00, 1h
    Limpiar logs antiguos                 :03:00, 30m
    Generar reporte diario                :03:30, 30m
    Enviar recordatorios SLA              :04:00, 30m
    
    section Semanal (Domingo 3 AM)
    Limpiar notificaciones leídas >90d    :03:00, 1h
    Archivar reclamos antiguos            :04:00, 2h
    Optimizar índices BD                  :06:00, 1h
```

---

**Nota:** Todos estos flujos están implementados en el sistema y pueden adaptarse según los requerimientos específicos del cliente.

---

**Documento actualizado:** Noviembre 2025  
**Versión:** 1.0
