# Propuesta Comercial - Sistema de Gestión de Reclamos

## 📋 Información General

**Cliente:** Transportes Romero  
**Proyecto:** Sistema Integral de Gestión de Reclamos y Encuestas de Satisfacción  
**Fecha de Propuesta:** Noviembre 2025  
**Vigencia:** 30 días

---

## 🎯 Resumen Ejecutivo

Transportes Romero requiere un sistema profesional para gestionar reclamos de clientes, cumpliendo con las normativas de Indecopi sobre Libro de Reclamaciones, y medir la satisfacción mediante encuestas automatizadas.

Este documento presenta **3 opciones** de implementación que se ajustan a diferentes necesidades y presupuestos, todas incluyen las funcionalidades core para el cumplimiento normativo.

---

## 📦 PAQUETES DISPONIBLES

### Comparativa Rápida

| Característica | BÁSICO | PROFESIONAL ⭐ | PREMIUM |
|----------------|--------|----------------|---------|
| **Precio** | **S/. 25,000** | **S/. 42,000** | **S/. 58,000** |
| **Tiempo** | 10-12 semanas | 16-20 semanas | 22-26 semanas |
| Formulario público reclamos | ✅ | ✅ | ✅ |
| Consulta pública por código | ✅ | ✅ | ✅ |
| Panel administrativo completo | ✅ | ✅ | ✅ |
| Sistema de estados y seguimiento | ✅ | ✅ | ✅ |
| Notificaciones por email | ✅ | ✅ | ✅ |
| Gestión de encuestas | ✅ | ✅ | ✅ |
| Dashboard con métricas | Básico | Avanzado | Premium |
| Reportes para Indecopi | ✅ | ✅ | ✅ |
| Exportación Excel | ✅ | ✅ | ✅ |
| Exportación PDF | ❌ | ✅ | ✅ |
| **Portal del Cliente** | ❌ | ✅ | ✅ |
| Login y registro de clientes | ❌ | ✅ | ✅ |
| Dashboard personal cliente | ❌ | ✅ | ✅ |
| Sistema de comentarios | ❌ | ✅ | ✅ |
| Códigos QR automáticos | ❌ | ✅ | ✅ |
| **Chat en Tiempo Real** | ❌ | ❌ | ✅ |
| Notificaciones push en tiempo real | ❌ | ❌ | ✅ |
| API REST documentada | ❌ | ❌ | ✅ |
| Estadísticas avanzadas con IA | ❌ | ❌ | ✅ |
| Capacitación incluida | ❌ | ❌ | 1 sesión |
| Garantía | 30 días | 60 días | 90 días |
| Soporte post-entrega | 1 mes | 3 meses | 6 meses |

---

## 💼 PAQUETE 1: BÁSICO

### **Inversión: S/. 25,000**
### **Tiempo de Implementación: 10-12 semanas**

#### ✅ Funcionalidades Incluidas

**Módulo de Reclamos:**
- Formulario público web para registro de reclamos
- Captura de todos los campos requeridos por Indecopi
- Subida de archivos adjuntos (hasta 5 archivos de 5MB c/u)
- Generación automática de código único (REC-2025-XXXX)
- Consulta pública de estado por código (sin necesidad de login)
- Panel administrativo para gestión interna
- Sistema de estados: Nuevo, En Revisión, En Proceso, Resuelto, Cerrado, etc.
- Asignación de casos a agentes
- Sistema de comentarios internos
- Historial completo de cambios

**Notificaciones Automáticas:**
- Email de confirmación al registrar reclamo
- Notificación al cambiar de estado
- Notificación al resolver reclamo
- Alertas a administradores de nuevos casos

**Módulo de Encuestas:**
- Creador de encuestas básicas
- Envío automático post-resolución
- Captura de respuestas
- Visualización de resultados

**Reportes y Dashboard:**
- Dashboard básico con métricas principales:
  - Total de reclamos
  - Reclamos por estado
  - Reclamos resueltos vs pendientes
- Reporte para Indecopi con formato establecido
- Exportación a Excel (.xlsx)

**Gestión de Usuarios:**
- Sistema de roles: Admin, Supervisor, Agente
- Login con email y contraseña
- Permisos por rol

**Seguridad:**
- Autenticación JWT
- Contraseñas encriptadas
- HTTPS obligatorio
- Validaciones de datos

**Infraestructura:**
- Base de datos PostgreSQL
- Backend ASP.NET Core 8.0
- Frontend React + TypeScript
- Diseño responsive (móvil, tablet, desktop)

#### 📦 Entregables

- ✅ Sistema completo instalado y funcionando
- ✅ Base de datos configurada
- ✅ Código fuente
- ✅ Documentación técnica básica
- ✅ Manual de usuario en PDF
- ✅ 2 sesiones de capacitación (2 horas c/u)

#### ⚙️ Soporte y Garantía

- **Garantía:** 30 días de corrección de bugs
- **Soporte:** 1 mes de soporte técnico vía email/WhatsApp (horario laboral)
- **Actualizaciones:** No incluidas

#### 💰 Forma de Pago

- **40% al firmar contrato:** S/. 10,000
- **30% a la mitad del proyecto:** S/. 7,500
- **30% al entregar:** S/. 7,500

#### ⏱️ Cronograma

| Fase | Duración | Entregable |
|------|----------|------------|
| 1. Diseño y planificación | 2 semanas | Mockups y BD |
| 2. Desarrollo backend | 4 semanas | API funcional |
| 3. Desarrollo frontend | 3 semanas | Interfaz completa |
| 4. Testing y ajustes | 2 semanas | Sistema estable |
| 5. Deploy y capacitación | 1 semana | Sistema en producción |

---

## 💼 PAQUETE 2: PROFESIONAL ⭐ (RECOMENDADO)

### **Inversión: S/. 42,000**
### **Tiempo de Implementación: 16-20 semanas**

#### ✅ TODO LO DEL PAQUETE BÁSICO +

**Portal del Cliente:**
- Sistema de registro para clientes
- Login personalizado
- Dashboard personal con:
  - Todos mis reclamos en un solo lugar
  - Estado actual de cada reclamo
  - Historial completo
- Ver detalle completo de cada reclamo propio
- Sistema de comentarios bidireccional (cliente-empresa)
- Perfil de usuario editable
- Notificaciones internas en el portal

**Reportes Avanzados:**
- Dashboard avanzado con gráficos interactivos:
  - Tendencias mensuales
  - Reclamos por categoría
  - Tiempo promedio de resolución
  - Satisfacción del cliente (%)
  - Agentes más efectivos
- Reportes personalizados con filtros avanzados
- Exportación a PDF profesional (con logo y formato)
- Reporte ejecutivo mensual automatizado

**Funcionalidades Adicionales:**
- Generador automático de códigos QR para acceso rápido
- Sistema de priorización de reclamos (Alta, Media, Baja, Urgente)
- Alertas de vencimiento SLA (tiempo de respuesta)
- Campos personalizables en formularios
- Múltiples canales de ingreso (Web, QR, Email)
- Sistema de archivos mejorado con vista previa

**Diseño Mejorado:**
- UI/UX profesional y moderno
- Animaciones y transiciones suaves
- Diseño personalizado según brand de Transportes Romero

#### 📦 Entregables

- ✅ Todo lo del Paquete Básico
- ✅ Portal del cliente completo
- ✅ Sistema de reportes avanzados
- ✅ Códigos QR para cada reclamo
- ✅ Documentación técnica completa
- ✅ Manual de usuario detallado
- ✅ **4 sesiones de capacitación** (2 horas c/u)
  - 2 para administradores/supervisores
  - 2 para agentes

#### ⚙️ Soporte y Garantía

- **Garantía:** 60 días de corrección de bugs
- **Soporte:** 3 meses de soporte técnico vía email/WhatsApp
- **Actualizaciones menores:** 3 meses incluidos
- **Mantenimiento:** Prioridad en solicitudes

#### 💰 Forma de Pago

- **40% al firmar contrato:** S/. 16,800
- **30% a la mitad del proyecto:** S/. 12,600
- **30% al entregar:** S/. 12,600

#### ⏱️ Cronograma

| Fase | Duración | Entregable |
|------|----------|------------|
| 1. Planificación y diseño | 2 semanas | Diseño completo aprobado |
| 2. Infraestructura | 1 semana | BD y setup |
| 3. Módulo de reclamos | 5 semanas | Core funcional |
| 4. Portal del cliente | 4 semanas | Portal completo |
| 5. Encuestas y reportes | 3 semanas | Módulos adicionales |
| 6. Testing integral | 2 semanas | Sistema probado |
| 7. Deploy y capacitación | 1 semana | En producción |

---

## 💼 PAQUETE 3: PREMIUM

### **Inversión: S/. 58,000**
### **Tiempo de Implementación: 22-26 semanas**

#### ✅ TODO LO DEL PAQUETE PROFESIONAL +

**Chat en Tiempo Real:**
- Sistema de chat bidireccional cliente-agente
- Notificaciones en tiempo real con SignalR
- Indicadores de "escribiendo..."
- Historial completo de conversaciones
- Estado online/offline
- Chat interno entre agentes

**Notificaciones Push en Tiempo Real:**
- Notificaciones instantáneas en el navegador
- Sin necesidad de recargar la página
- Centro de notificaciones completo
- Alertas sonoras configurables

**API REST Documentada:**
- API completa para integraciones futuras
- Documentación Swagger/OpenAPI
- Webhooks para eventos importantes
- Posibilidad de integrar con otros sistemas (ERP, CRM)

**Dashboard Ejecutivo Avanzado:**
- Métricas estratégicas en tiempo real
- Gráficos interactivos avanzados (Recharts)
- Predicciones y tendencias con análisis de datos
- KPIs personalizables
- Vista comparativa por períodos
- Exportación de cualquier gráfico

**Estadísticas con IA:**
- Detección automática de patrones en reclamos
- Sugerencias de respuestas basadas en casos similares
- Clasificación automática de prioridad
- Análisis de sentimiento en comentarios

**Funcionalidades Premium:**
- Sistema de backup automático diario
- Logs de auditoría completos
- Recuperación de datos eliminados
- Multi-idioma (Español/Inglés)
- Modo oscuro para la interfaz

#### 📦 Entregables

- ✅ Todo lo del Paquete Profesional
- ✅ Chat en tiempo real completo
- ✅ API REST documentada
- ✅ Dashboard ejecutivo avanzado
- ✅ Sistema de backup automático
- ✅ Documentación técnica exhaustiva
- ✅ Manual de administrador
- ✅ Manual de usuario final
- ✅ **1 sesión de capacitación presencial** (4 horas)
  - Para todo el equipo
  - En las instalaciones del cliente

#### ⚙️ Soporte y Garantía

- **Garantía:** 90 días de corrección de bugs
- **Soporte:** 6 meses de soporte técnico prioritario
- **Actualizaciones:** 6 meses de actualizaciones incluidas
- **Mantenimiento:** Acceso prioritario para nuevos requerimientos
- **Consultoría:** 2 horas mensuales de consultoría técnica (6 meses)

#### 💰 Forma de Pago

- **40% al firmar contrato:** S/. 23,200
- **30% a la mitad del proyecto:** S/. 17,400
- **30% al entregar:** S/. 17,400

#### ⏱️ Cronograma

| Fase | Duración | Entregable |
|------|----------|------------|
| 1. Planificación detallada | 2 semanas | Plan completo |
| 2. Infraestructura y diseño | 2 semanas | Setup avanzado |
| 3. Módulo de reclamos | 5 semanas | Core completo |
| 4. Portal del cliente | 4 semanas | Portal full |
| 5. Chat en tiempo real | 3 semanas | SignalR funcional |
| 6. Encuestas y reportes | 2 semanas | Módulos adicionales |
| 7. Dashboard avanzado y API | 3 semanas | Premium features |
| 8. Testing y optimización | 3 semanas | Sistema optimizado |
| 9. Deploy y capacitación | 1 semana | Producción + training |

---

## 💻 REQUERIMIENTOS TÉCNICOS

### Lo que el Cliente Debe Proporcionar:

1. **Hosting:**
   - VPS Ubuntu 22.04+ (recomendado: 4GB RAM, 2 CPU, 50GB SSD)
   - Acceso SSH root
   - O podemos gestionar el hosting (costo adicional)

2. **Dominio:**
   - Dominio propio (ej: reclamos.romeroempresas.com)
   - Acceso al panel de DNS

3. **Email:**
   - Cuenta SendGrid o Mailgun para envío de emails
   - O podemos configurar (costo adicional)

4. **Contenido:**
   - Logo de la empresa en formato vectorial
   - Colores corporativos (códigos hex)
   - Textos legales si aplican

### Stack Tecnológico:

- **Backend:** ASP.NET Core 8.0 (C#)
- **Frontend:** React 18 + TypeScript
- **Base de Datos:** PostgreSQL 15+
- **Servidor Web:** Nginx
- **SSL:** Let's Encrypt (gratis)

---

## 💰 COSTOS MENSUALES ADICIONALES (Estimados)

Estos costos son responsabilidad del cliente y NO están incluidos en los paquetes:

| Servicio | Costo Mensual |
|----------|---------------|
| **VPS Hosting** | S/. 100 - 200 |
| **Dominio .com.pe** | S/. 10 (anual S/. 120) |
| **SendGrid (Emails)** | S/. 50 - 100 |
| **Backup Externo** | S/. 30 - 50 |
| **TOTAL MENSUAL** | **S/. 190 - 350** |

**Primer año total:** S/. 2,280 - 4,200 en infraestructura

---

## 📞 SERVICIOS POST-ENTREGA (Opcionales)

### Paquetes de Soporte Mensual

#### Soporte Básico - S/. 500/mes
- Respuesta en 48 horas hábiles
- Corrección de bugs
- Consultas técnicas por email
- 2 horas de cambios menores/mes

#### Soporte Profesional - S/. 800/mes
- Respuesta en 24 horas
- Todo lo del básico +
- 5 horas de desarrollo/mes
- Actualizaciones de seguridad
- Monitoreo proactivo

#### Soporte Premium - S/. 1,200/mes
- Respuesta en 4 horas
- Todo lo del profesional +
- 10 horas de desarrollo/mes
- Nuevas funcionalidades
- Reuniones mensuales
- Optimizaciones continuas

### Servicios Adicionales (Por Demanda)

- **Nuevas funcionalidades:** S/. 70/hora
- **Capacitaciones adicionales:** S/. 300/sesión (2 horas)
- **Integración con otros sistemas:** Cotización según complejidad
- **Migración de datos:** Desde S/. 1,500
- **Diseño personalizado:** Desde S/. 2,000

---

## ✅ QUÉ INCLUYEN TODOS LOS PAQUETES

### Diseño y Planificación
- ✅ Reunión de levantamiento de requerimientos
- ✅ Diseño de base de datos completo
- ✅ Mockups/wireframes de pantallas principales
- ✅ Plan de proyecto detallado

### Desarrollo
- ✅ Código limpio y documentado
- ✅ Arquitectura escalable
- ✅ Buenas prácticas de desarrollo
- ✅ Control de versiones con Git

### Testing
- ✅ Pruebas unitarias
- ✅ Pruebas de integración
- ✅ Pruebas de usuario (UAT)
- ✅ Corrección de bugs encontrados

### Despliegue
- ✅ Configuración del servidor
- ✅ Instalación del sistema
- ✅ Configuración de SSL/HTTPS
- ✅ Optimización de rendimiento

### Entregables
- ✅ Sistema completo funcionando
- ✅ Código fuente
- ✅ Base de datos configurada
- ✅ Documentación técnica
- ✅ Manual de usuario
- ✅ Capacitación del equipo

### Garantía
- ✅ Corrección de bugs en período de garantía
- ✅ Soporte técnico post-entrega
- ✅ Atención de consultas

---

## 📋 CONDICIONES GENERALES

### Vigencia de la Propuesta
- Esta propuesta es válida por **30 días** desde su emisión

### Inicio del Proyecto
- El proyecto inicia al recibir el primer pago (40%)
- Se requiere firma de contrato antes del inicio

### Cambios en el Alcance
- Cambios solicitados fuera del alcance original serán cotizados aparte
- Pueden afectar el tiempo de entrega

### Propiedad Intelectual
- El cliente tendrá propiedad total del código fuente al completar el pago
- Durante el desarrollo, los derechos pertenecen al desarrollador

### Responsabilidades del Cliente
- Proporcionar acceso a recursos necesarios
- Feedback oportuno durante el desarrollo
- Aprobaciones en tiempos acordados
- Proporcionar contenido y assets

### Confidencialidad
- Toda información del proyecto será tratada con confidencialidad
- Se puede firmar NDA si el cliente lo requiere

---

## 🎯 RECOMENDACIÓN

Para **Transportes Romero**, considerando:
- ✅ Es una empresa establecida con visión de crecimiento
- ✅ Necesidad de cumplimiento normativo (Indecopi)
- ✅ Volumen esperado de reclamos
- ✅ Importancia de la experiencia del cliente

### Recomendamos: **PAQUETE PROFESIONAL (S/. 42,000)**

**¿Por qué?**
- Incluye portal del cliente (diferenciador importante)
- Reportes avanzados para toma de decisiones
- Mejor relación calidad-precio
- Dashboard profesional para gerencia
- Soporte extendido (3 meses)
- Tiempo de implementación razonable (16-20 semanas)

El **Paquete Básico** cumple con lo mínimo legal pero carece de portal para clientes.

El **Paquete Premium** es excelente si planean crecer rápido y necesitan integraciones, pero tiene mayor inversión inicial.

---

## 📞 PRÓXIMOS PASOS

1. **Revisar propuesta** con su equipo
2. **Reunión de aclaraciones** si tienen dudas
3. **Seleccionar el paquete** que mejor se ajuste
4. **Firma de contrato** y primer pago
5. **Kickoff meeting** - inicio del proyecto

---

## 📧 CONTACTO

**Desarrollador:** Deca  
**Email:** [tu-email]  
**Teléfono/WhatsApp:** [tu-telefono]  
**Portfolio:** https://decatron.net

---

**Nota:** Esta propuesta puede ser ajustada según necesidades específicas del cliente. Los precios son en soles peruanos (PEN) e incluyen IGV.

---

**Fecha de emisión:** Noviembre 2025  
**Válido hasta:** Diciembre 2025  
**Versión:** 1.0
