# Sistema de Gestión de Reclamos y Encuestas - Transportes Romero

## 📋 Descripción del Proyecto

Sistema web integral para la gestión de reclamos y encuestas de satisfacción del cliente, cumpliendo con las normativas de Indecopi y permitiendo múltiples canales de registro con **códigos únicos por medio**.

**Cliente:** Transportes Romero  
**Tipo:** Aplicación Web Completa  
**Estado:** En Planificación

---

## 🎯 Objetivo Principal

Crear una plataforma profesional que permita a Transportes Romero:
- Gestionar reclamos de clientes de manera eficiente
- Cumplir con normativas legales (Libro de Reclamaciones - Indecopi)
- Medir la satisfacción del cliente mediante encuestas
- Generar reportes y estadísticas para toma de decisiones
- Identificar claramente el canal de origen de cada reclamo
- Notificar automáticamente cuando se generen reportes

---

## ✨ Características Principales

### Módulo de Reclamos
- ✅ Registro público de reclamos (sin necesidad de login)
- ✅ **Código único por canal:** WEB-2025-0001, QR-2025-0001, EMAIL-2025-0001, FISICO-2025-0001
- ✅ Consulta de estado por código único
- ✅ Panel administrativo para gestión interna
- ✅ Sistema de estados y seguimiento
- ✅ Notificaciones automáticas por email
- ✅ Asignación de casos a agentes
- ✅ Historial completo de cada reclamo
- ✅ Carga de archivos adjuntos (hasta 5 archivos de 5MB c/u)
- ✅ Sistema de comentarios/respuestas

### Módulo de Encuestas
- ✅ Creador de encuestas personalizadas
- ✅ Envío automático post-resolución
- ✅ Análisis de resultados
- ✅ Historial de encuestas respondidas

### Reportes y Dashboard
- ✅ Dashboard con métricas en tiempo real
- ✅ Reportes para Indecopi
- ✅ Exportación a Excel/PDF
- ✅ **Notificaciones automáticas de reportes:** Al generar un reporte, notifica tanto a quien lo generó como a los destinatarios
- ✅ Estadísticas por canal de ingreso
- ✅ Gráficos y tendencias

### Portal del Cliente (Opcional según paquete)
- ✅ Registro y login de clientes
- ✅ Dashboard personal
- ✅ Ver todos mis reclamos
- ✅ Seguimiento en tiempo real
- ✅ Perfil editable

### Chat en Tiempo Real (Solo Premium)
- ✅ Comunicación instantánea cliente-agente
- ✅ Notificaciones push en tiempo real
- ✅ Historial de conversaciones

---

## 🚀 Innovaciones del Sistema

### 1. Códigos Únicos por Canal de Ingreso

El sistema genera códigos que identifican claramente el medio por el cual ingresó el reclamo:

```
WEB-2025-0001      → Registro por formulario web
QR-2025-0001       → Escaneo de código QR
EMAIL-2025-0001    → Recepción por correo electrónico
FISICO-2025-0001   → Digitalización de reclamo físico
```

**Ventajas:**
- ✅ Identificación inmediata del canal de origen
- ✅ Estadísticas precisas por canal
- ✅ Optimización de recursos según canal preferido
- ✅ Numeración independiente por cada medio
- ✅ Mejor experiencia de soporte
- ✅ Análisis de efectividad por canal

**Ejemplo de uso:**
```sql
-- Estadísticas por canal
SELECT 
    canal,
    COUNT(*) as total_reclamos,
    ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (), 2) as porcentaje
FROM reclamos
WHERE EXTRACT(YEAR FROM fecha_reclamo) = 2025
GROUP BY canal
ORDER BY total_reclamos DESC;

-- Resultado:
-- WEB:    120 reclamos (48%)
-- QR:     80 reclamos  (32%)
-- EMAIL:  35 reclamos  (14%)
-- FISICO: 15 reclamos  (6%)
```

---

### 2. Sistema de Notificaciones de Reportes

Cuando un usuario (administrador o supervisor) genera un reporte:

**Flujo completo:**
1. Usuario solicita generar reporte (PDF o Excel)
2. Sistema procesa en background
3. Al completar, **automáticamente**:
   - ✅ Envía email al generador: *"Tu reporte está listo"*
   - ✅ Crea notificación en el sistema con link de descarga
   - ✅ Si especificó destinatarios:
     - Email a cada uno: *"Te compartieron un reporte"*
     - Notificación en sus dashboards
4. Historial completo de reportes generados

**Beneficios:**
- ✅ No hay que estar pendiente del proceso
- ✅ Descarga inmediata desde el email
- ✅ Compartir reportes con otros usuarios fácilmente
- ✅ Trazabilidad completa de quién generó qué

---

## 🛠️ Stack Tecnológico

### Backend
- **Framework:** ASP.NET Core 8.0 Web API
- **Lenguaje:** C#
- **Base de Datos:** PostgreSQL 15+
- **ORM:** Entity Framework Core
- **Autenticación:** JWT (JSON Web Tokens)
- **Notificaciones:** SignalR (tiempo real - opcional)

### Frontend
- **Framework:** React 18
- **Lenguaje:** TypeScript
- **UI Library:** Material-UI / Ant Design
- **Estado:** Context API / Redux (según complejidad)
- **HTTP Client:** Axios

### Infraestructura
- **Servidor:** Ubuntu VPS (Nginx)
- **Proxy:** Cloudflare
- **Emails:** SendGrid / Mailgun
- **Storage:** Sistema de archivos local

### Herramientas de Desarrollo
- **Control de Versiones:** Git / GitHub
- **Documentación API:** Swagger/OpenAPI
- **Logs:** Serilog
- **Testing:** xUnit (backend), Jest (frontend)

---

## 📁 Estructura del Repositorio

```
sistema-reclamos-romero/
├── README.md                       # Este archivo
├── .gitignore                      # Archivos a ignorar en Git
├── docs/                           # Documentación técnica
│   ├── 01-analisis-requisitos.md  # Requisitos funcionales completos
│   ├── 02-base-datos.md           # 15 tablas + códigos por canal
│   ├── 03-arquitectura-tecnica.md # Stack y arquitectura completa
│   ├── 04-flujos-sistema.md       # 13 diagramas de flujo (Mermaid)
│   └── 05-api-endpoints.md        # 40+ endpoints documentados
└── propuesta/                      # Documentación comercial
    └── presupuesto-comercial.md   # 3 paquetes con modelo por etapas
```

---

## 📦 Paquetes Disponibles (Modelo de Pago por Etapas)

### Comparativa Rápida

| Característica | BÁSICO | PROFESIONAL ⭐ | PREMIUM |
|----------------|--------|----------------|---------|
| **Inversión Inicial** | **S/. 25,000** | **S/. 42,000** | **S/. 58,000** |
| **Modelo de Pago** | Por etapas | Por etapas | Por etapas |
| **Duración Estimada** | 10-12 semanas | 16-20 semanas | 22-26 semanas |
| Formulario público reclamos | ✅ | ✅ | ✅ |
| Código único por canal | ✅ | ✅ | ✅ |
| Consulta pública por código | ✅ | ✅ | ✅ |
| Panel administrativo completo | ✅ | ✅ | ✅ |
| Sistema de estados y seguimiento | ✅ | ✅ | ✅ |
| Notificaciones por email | ✅ | ✅ | ✅ |
| Notificaciones de reportes | ✅ | ✅ | ✅ |
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
| Estadísticas avanzadas | ❌ | ❌ | ✅ |
| Capacitación incluida | ❌ | ❌ | 1 sesión (4hrs) |
| Garantía | 30 días | 60 días | 90 días |
| Soporte post-entrega | 1 mes | 3 meses | 6 meses |

**💡 Recomendado:** Paquete Profesional - Mejor relación calidad-precio con portal del cliente incluido.

[Ver propuesta comercial completa](./propuesta/presupuesto-comercial.md)

---

## 💰 Ventajas del Modelo por Etapas

### Flexibilidad Total
- Pagas solo por lo completado
- Puedes detener el proyecto después de cualquier etapa
- Ajustas prioridades según necesidades
- Menor riesgo inicial

### Visibilidad Constante
- Entregables concretos en cada etapa
- Revisión y aprobación continua
- Feedback inmediato
- Control del presupuesto

### Ejemplo de Pagos (Paquete Profesional S/. 42,000):
- **ETAPA 1:** Diseño y Planificación - S/. 3,000
- **ETAPA 2:** Fundación del Sistema - S/. 5,000
- **ETAPA 3:** Módulo de Reclamos Core - S/. 8,000
- **ETAPA 4:** Gestión Interna - S/. 5,000
- **ETAPA 5:** Encuestas y Reportes - S/. 3,000
- **ETAPA 6:** Testing y Deploy - S/. 1,000
- **ETAPA 7:** Portal del Cliente - S/. 9,000
- **ETAPA 8:** Reportes Avanzados - S/. 5,000
- **ETAPA 9:** Entrega Final - S/. 3,000

Cada etapa se paga 50% al inicio y 50% al completar.

---

## 📊 Entidades Principales del Sistema

Base de datos con **15 tablas** diseñadas profesionalmente:

1. **Usuarios** - Clientes, agentes, administradores
2. **Roles** - Permisos del sistema
3. **Reclamos** - Con código único por canal
4. **Estados_Reclamo** - 8 estados del ciclo de vida
5. **Motivos_Reclamo** - 17 motivos predefinidos
6. **Comentarios** - Comunicación bidireccional
7. **Archivos** - Evidencias adjuntas
8. **Historial_Estados** - Trazabilidad completa
9. **Encuestas** - Plantillas de satisfacción
10. **Preguntas** - Preguntas de encuestas
11. **Encuestas_Respuestas** - Respuestas de clientes
12. **Notificaciones** - Sistema de alertas (incluye reportes)
13. **Reportes_Generados** - Historial con destinatarios
14. **Configuraciones** - Parámetros del sistema
15. **Logs_Auditoria** - Registro de acciones

[Ver diseño completo de base de datos](./docs/02-base-datos.md)

---

## 🔐 Roles y Permisos

1. **Cliente** - Registrar y ver sus reclamos
2. **Agente de Soporte** - Gestionar reclamos asignados
3. **Supervisor** - Asignar casos y ver reportes
4. **Administrador** - Control total del sistema
5. **Ejecutivo** - Solo lectura y reportes estratégicos

---

## 💻 Requerimientos del Cliente

### Lo que debe proporcionar Transportes Romero:

1. **Hosting:**
   - VPS Ubuntu 22.04+ (recomendado: 4GB RAM, 2 CPU, 50GB SSD)
   - Acceso SSH root
   - *O podemos gestionar el hosting (costo adicional)*

2. **Dominio:**
   - Dominio propio (ej: reclamos.romeroempresas.com)
   - Acceso al panel de DNS

3. **Email:**
   - Cuenta SendGrid o Mailgun para envío de emails
   - *O podemos configurar (costo adicional)*

4. **Contenido:**
   - Logo de la empresa en formato vectorial (SVG, AI, o PNG alta resolución)
   - Colores corporativos (códigos hexadecimales)
   - Textos legales si aplican

### Costos Mensuales Adicionales (Estimados)

Estos costos son responsabilidad del cliente y NO están incluidos en los paquetes:

| Servicio | Costo Mensual |
|----------|---------------|
| VPS Hosting | S/. 100 - 200 |
| Dominio .com.pe | S/. 10 (anual S/. 120) |
| SendGrid (Emails) | S/. 50 - 100 |
| Backup Externo | S/. 30 - 50 |
| **TOTAL MENSUAL** | **S/. 190 - 350** |

**Primer año total infraestructura:** S/. 2,280 - 4,200

---

## 📄 Propiedad Intelectual

### Derechos del Código y Sistema

- **Durante el desarrollo:** Los derechos pertenecen al desarrollador
- **Al completar el pago total:** Transferencia completa de derechos al cliente (Transportes Romero)
- **Código fuente:** Entregado al finalizar el proyecto completo
- **Uso del código:** El cliente puede modificar, usar y distribuir libremente después del pago final
- **Mantenimiento:** El cliente puede contratar a otros desarrolladores si lo desea

**Importante:** Hasta completar el 100% del pago acordado, los derechos de propiedad intelectual permanecen con el desarrollador.

---

## 🚀 Roadmap de Implementación

### Enfoque Incremental por Etapas

Cada paquete se desarrolla en etapas con entregables concretos:

**Ejemplo: Paquete Profesional (16-20 semanas)**

1. **Semanas 1-2:** Diseño y Planificación
2. **Semanas 3-4:** Fundación del Sistema
3. **Semanas 5-8:** Módulo de Reclamos Core
4. **Semanas 9-10:** Gestión Interna
5. **Semanas 11-12:** Encuestas y Reportes
6. **Semanas 13:** Testing y Deploy Básico
7. **Semanas 14-17:** Portal del Cliente
8. **Semanas 18-19:** Reportes Avanzados y QR
9. **Semanas 20:** Optimización y Entrega Final

Al final de cada etapa hay revisión y aprobación antes de continuar.

---

## ✅ QUÉ INCLUYEN TODOS LOS PAQUETES

- ✅ Diseño UI/UX profesional
- ✅ Código limpio y documentado
- ✅ Arquitectura escalable
- ✅ Responsive design (móvil, tablet, desktop)
- ✅ Testing y corrección de bugs
- ✅ Deploy en servidor
- ✅ Documentación técnica
- ✅ Manual de usuario
- ✅ Notificaciones por email automáticas
- ✅ Cumplimiento normativo Indecopi
- ✅ Códigos únicos por canal
- ✅ Notificaciones de reportes

---

## 🔗 Enlaces Útiles

- [Análisis de Requisitos Completo](./docs/01-analisis-requisitos.md)
- [Diseño de Base de Datos (15 tablas)](./docs/02-base-datos.md)
- [Arquitectura Técnica Detallada](./docs/03-arquitectura-tecnica.md)
- [Flujos del Sistema (13 diagramas)](./docs/04-flujos-sistema.md)
- [API REST Endpoints (40+)](./docs/05-api-endpoints.md)
- [Propuesta Comercial Completa](./propuesta/presupuesto-comercial.md)
- [Normativa Indecopi - Libro de Reclamaciones](https://www.indecopi.gob.pe/)

---

## 📞 Contacto

**Desarrollador:** Deca  
**Email:** anthonydeca@decatron.net 
**Repositorio:** https://github.com/decagraff/sistema-reclamos-romero

---

## 📝 Notas Importantes

- Esta propuesta es válida por **30 días** desde su emisión
- Los precios están en **soles peruanos (PEN)**
- El código fuente se entrega al completar el 100% del pago
- Garantía y soporte varían según el paquete seleccionado
- Modelo de pago flexible por etapas para menor riesgo

---

**Última actualización:** Noviembre 2025  
**Versión:** 1.1 - Códigos por Canal + Notificaciones de Reportes + Modelo por Etapas  
**Documento:** Planificación Completa