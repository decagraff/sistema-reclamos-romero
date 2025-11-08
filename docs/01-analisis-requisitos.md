# Análisis de Requisitos del Sistema

## 📸 Fuentes de Información

Este análisis se basa en:
1. ✅ Imagen 1: Matriz de la Plataforma de Gestión
2. ✅ Imagen 2: Módulos del Sistema
3. ✅ Formulario HTML actual de Transportes Romero

---

## 🎯 Requisitos Funcionales

### 1. MÓDULO DE GESTIÓN DE RECLAMOS

#### 1.1 Registro de Reclamos (Múltiples Canales)

**RF-001: Libro Reclamación Virtual (Enlace Web)**
- El sistema debe permitir registro de reclamos vía formulario web
- Formato: Igual al formulario actual de la web
- Gestión de Alertas: Sistema de notificaciones por email
- Registro: Códigos 070, 071, 072 (según tipo)
- Seguimiento: Tracking en tiempo real
- Estadísticas: Generación automática de reportes

**RF-002: Libro Reclamación Digital (QR)**
- El sistema debe generar códigos QR únicos
- Al escanear, redirigir al formulario web
- Formato: Idéntico al web
- Mismo flujo de gestión que el virtual

**RF-003: Libro Reclamación Físico (Registro Manual)**
- El sistema debe permitir carga manual de reclamos físicos
- Requiere escaneo de documentos
- Admin puede digitalizar reclamos en papel

**RF-004: Libro Reclamación por Correo**
- El sistema debe capturar emails entrantes
- Procesar y convertir en tickets
- Formato igual al web

**RF-005: Consulta Pública de Estado**
- Sin necesidad de login
- Por código único de reclamo
- Muestra: estado actual, fecha, respuestas

#### 1.2 Campos del Formulario de Reclamo

**Obligatorios:**
- Fecha de reclamo (auto)
- Nombres y apellidos
- Teléfono
- Email
- Explicación del reclamo
- Acción requerida que se realice
- ¿Datos del Representante Legal? (Sí/No)
- ¿Eres Cliente? (Sí/No)
- Subir archivo

**Opcionales:**
- Empresa distribuidora
- Tipo de documento (DNI/RUC)
- N° de documento
- Departamento
- Domicilio para notificaciones
- Motivo del reclamo (dropdown)
- Número de suministro (si es cliente)

**Dropdown: Motivos del Reclamo (15 opciones)**
1. Negativa a la instalación del suministro
2. Excesiva facturación
3. Excesivo consumo
4. Corte del servicio
5. Recupero de energía
6. Cobro indebido
7. Negativa al cambio de opción tarifaria
8. Negativa al incremento de la capacidad solicitada
9. Reembolso de aportes o contribuciones
10. Reubicación de instalaciones bajo responsabilidad
11. Mala calidad de Producto/Servicio
12. Deudas de terceros
13. Otras cuestiones vinculadas a la prestación del servicio
14. Inconformidad con la actuación de un funcionario
15. Inconformidad con los trabajos realizados
16. Inconformidad con el proceso de venta
17. En desacuerdo con el proceso de instalación del servicio

#### 1.3 Gestión Interna de Reclamos

**RF-010: Panel Administrativo**
- Dashboard con métricas principales
- Lista de reclamos con filtros
- Búsqueda avanzada
- Ordenamiento por fecha, estado, prioridad

**RF-011: Visualización de Reclamo**
- Ver todos los datos del formulario
- Ver archivos adjuntos
- Ver historial de cambios
- Ver comunicaciones

**RF-012: Asignación de Casos**
- Asignar reclamo a agente específico
- Reasignar si es necesario
- Notificar al agente asignado

**RF-013: Gestión de Estados**
Los reclamos deben poder tener los siguientes estados:
1. **NUEVO** - Recién ingresado
2. **EN REVISIÓN** - Asignado y siendo evaluado
3. **EN PROCESO** - Se está trabajando en la solución
4. **ESPERANDO CLIENTE** - Requiere información adicional
5. **RESUELTO** - Solución implementada
6. **CERRADO** - Cliente confirmó satisfacción
7. **REABIERTO** - Cliente no quedó satisfecho
8. **RECHAZADO** - Reclamo no procede (con justificación)

**RF-014: Sistema de Comentarios/Respuestas**
- Agregar respuestas al reclamo
- Historial de comunicaciones
- Adjuntar archivos como evidencia
- Registro de fecha/hora y usuario

**RF-015: Notificaciones Automáticas (TODOS LOS PAQUETES)**
El sistema debe enviar emails automáticos en:
- Registro exitoso del reclamo (con código único)
- Cambio de estado
- Respuesta del agente
- Recordatorios de tiempo
- Encuesta de satisfacción (post-resolución)

**RF-016: Historial de Reclamos**
- Ver reclamos anteriores del mismo cliente
- Filtrar por fecha, estado, motivo
- Exportar historial

---

### 2. MÓDULO DE GESTIÓN DE ENCUESTAS

**RF-020: Creador de Encuestas**
- Crear encuestas personalizadas
- Tipos de pregunta: texto, opción múltiple, escala
- Publicar link único
- Programar envío automático

**RF-021: Envío Automático Post-Resolución**
- Al marcar reclamo como "RESUELTO" → enviar encuesta
- Link personalizado por email
- Una encuesta por reclamo

**RF-022: Sistema de Respuesta**
- Interfaz simple para el cliente
- Guardar respuestas en BD
- Marcar como completada

**RF-023: Análisis de Resultados**
- Ver respuestas individuales
- Estadísticas agregadas
- Gráficos de satisfacción
- Exportar resultados

**RF-024: Historial de Encuestas**
- Listar todas las encuestas creadas
- Ver tasas de respuesta
- Filtrar por fecha

---

### 3. REPORTES Y ESTADÍSTICAS

**RF-030: Dashboard Administrativo**

Métricas mostradas (según imagen 2):
- **Clientes:** Total de clientes registrados (ej: 100)
- **Encuestas:** Total enviadas/respondidas
- **Reclamos Solucionados:** Total (ej: 30)
- **Reclamos Pendientes:** Total (ej: 20)

Adicionales:
- Nuevos hoy
- En proceso
- Tiempo promedio de resolución
- Satisfacción del cliente (%)

**RF-031: Reportes para Indecopi**
- Formato específico requerido por ley
- Todos los reclamos del período
- Datos del reclamante
- Motivo y resolución
- Exportación a PDF/Excel

**RF-032: Estadísticas Avanzadas**
- Reclamos por categoría
- Tendencias mensuales
- Agentes más efectivos
- SLA cumplido/incumplido
- Gráficos interactivos

**RF-033: Exportaciones**
- Excel (.xlsx)
- PDF
- CSV
- Filtros personalizados

---

### 4. PORTAL DEL CLIENTE (Paquetes Profesional y Premium)

**RF-040: Registro y Autenticación**
- Registro con email/contraseña
- Verificación de email
- Login con JWT
- Recuperación de contraseña

**RF-041: Dashboard Personal**
- Ver todos mis reclamos
- Estados actuales
- Últimas actualizaciones
- Encuestas pendientes

**RF-042: Detalle de Mis Reclamos**
- Ver información completa
- Ver respuestas del equipo
- Agregar comentarios adicionales
- Descargar comprobantes

**RF-043: Perfil de Usuario**
- Editar datos personales
- Cambiar contraseña
- Ver historial completo

---

### 5. CHAT EN TIEMPO REAL (Solo Paquete Premium)

**RF-050: Sistema de Chat**
- Chat bidireccional cliente-agente
- Notificaciones en tiempo real con SignalR
- Historial de conversaciones
- Estado online/offline

---

## 📊 Requisitos No Funcionales

### RNF-001: Rendimiento
- Tiempo de carga < 3 segundos
- Soportar 100 usuarios simultáneos (inicial)
- Base de datos optimizada con índices

### RNF-002: Seguridad
- Autenticación JWT
- Contraseñas hasheadas (bcrypt)
- Validación de datos en frontend y backend
- Protección contra SQL Injection
- HTTPS obligatorio
- Roles y permisos estrictos

### RNF-003: Usabilidad
- Interfaz intuitiva y clara
- Responsive (móvil, tablet, desktop)
- Mensajes de error descriptivos
- Confirmaciones de acciones críticas

### RNF-004: Compatibilidad
- Chrome, Firefox, Safari, Edge (últimas 2 versiones)
- Dispositivos móviles iOS y Android

### RNF-005: Disponibilidad
- Uptime objetivo: 99.5%
- Backup diario automático
- Logs de errores

### RNF-006: Mantenibilidad
- Código limpio y documentado
- Arquitectura modular
- API REST bien estructurada
- Documentación Swagger

### RNF-007: Escalabilidad
- Arquitectura preparada para crecimiento
- Base de datos normalizada
- Posibilidad de agregar más módulos

---

## 👥 Roles del Sistema

### Cliente (Público)
- Registrar reclamos sin login
- Consultar estado por código
- Responder encuestas

### Cliente Registrado (Opcional)
- Todo lo del público +
- Ver historial completo
- Dashboard personal
- Recibir notificaciones

### Agente de Soporte
- Ver reclamos asignados
- Responder y actualizar estados
- Agregar comentarios
- Subir evidencias

### Supervisor
- Todo lo del agente +
- Asignar casos a agentes
- Ver todos los reclamos
- Reportes básicos
- Crear encuestas

### Administrador
- Control total del sistema
- Gestión de usuarios
- Configuraciones
- Reportes avanzados
- Acceso a estadísticas completas

### Ejecutivo/Gerencia
- Solo lectura
- Dashboards ejecutivos
- Reportes estratégicos
- Exportaciones

---

## 📋 Reglas de Negocio

### RN-001: Código Único de Reclamo
- Formato: REC-YYYY-NNNN
- Ejemplo: REC-2025-0001
- Autoincremental por año

### RN-002: Tiempos de Respuesta (SLA)
- Reclamo NUEVO → EN REVISIÓN: 24 horas
- EN REVISIÓN → EN PROCESO: 48 horas
- EN PROCESO → RESUELTO: 7 días hábiles (depende del tipo)

### RN-003: Notificaciones Obligatorias
- Cliente SIEMPRE recibe email al:
  - Registrar reclamo
  - Cambiar estado
  - Agregar respuesta
  - Marcar como resuelto

### RN-004: Archivos Adjuntos
- Formatos permitidos: PDF, JPG, PNG, DOC, DOCX
- Tamaño máximo: 5 MB por archivo
- Máximo 5 archivos por reclamo

### RN-005: Encuestas Post-Resolución
- Solo se envían cuando estado = "RESUELTO"
- Una vez por reclamo
- Válidas por 7 días

### RN-006: Datos Obligatorios de Indecopi
Según normativa, cada reclamo debe tener:
- Fecha y hora exacta
- Datos completos del reclamante
- Motivo claro
- Respuesta de la empresa
- Fecha de resolución
- Estado final

---

## 🔄 Integraciones Futuras (No en MVP)

- Sistema ERP de la empresa
- WhatsApp Business API
- SMS para notificaciones
- Integración con CRM
- Analytics avanzado (Google Analytics, Mixpanel)

---

## 📝 Notas Adicionales

- El sistema debe cumplir con la **normativa peruana de Indecopi** sobre Libro de Reclamaciones
- Los datos personales deben tratarse según **Ley de Protección de Datos Personales (Ley N° 29733)**
- Todos los paquetes incluyen notificaciones por email
- La capacitación solo está incluida en el paquete Premium (1 sesión)

---

**Documento actualizado:** Noviembre 2025  
**Versión:** 1.0
