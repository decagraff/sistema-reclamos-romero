# Sistema de Gestión de Reclamos y Encuestas - Transportes Romero

## 📋 Descripción del Proyecto

Sistema web integral para la gestión de reclamos y encuestas de satisfacción del cliente, cumpliendo con las normativas de Indecopi y permitiendo múltiples canales de registro (web, QR, email, físico).

**Desarrollado para:** Transportes Romero  
**Tipo:** Aplicación Web Completa  
**Estado:** En Planificación

---

## 🎯 Objetivo Principal

Crear una plataforma profesional que permita a Transportes Romero:
- Gestionar reclamos de clientes de manera eficiente
- Cumplir con normativas legales (Libro de Reclamaciones - Indecopi)
- Medir la satisfacción del cliente mediante encuestas
- Generar reportes y estadísticas para toma de decisiones
- Mejorar los tiempos de respuesta y atención al cliente

---

## ✨ Características Principales

### Módulo de Reclamos
- ✅ Registro público de reclamos (sin necesidad de login)
- ✅ Consulta de estado por código único
- ✅ Panel administrativo para gestión interna
- ✅ Sistema de estados y seguimiento
- ✅ Notificaciones automáticas por email
- ✅ Asignación de casos a agentes
- ✅ Historial completo de cada reclamo
- ✅ Carga de archivos adjuntos
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
- ✅ Estadísticas y gráficos

### Portal del Cliente (Opcional según paquete)
- ✅ Registro y login de clientes
- ✅ Dashboard personal
- ✅ Ver todos mis reclamos
- ✅ Seguimiento en tiempo real
- ✅ Perfil editable

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
- **Storage:** Sistema de archivos local / AWS S3

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
├── docs/                           # Documentación técnica
│   ├── 01-analisis-requisitos.md
│   ├── 02-base-datos.md
│   ├── 03-arquitectura-tecnica.md
│   ├── 04-flujos-sistema.md
│   └── 05-api-endpoints.md
├── propuesta/                      # Documentación comercial
│   └── presupuesto-comercial.md
└── diagramas/                      # Diagramas del sistema
    ├── flujo-reclamo.md
    ├── modelo-bd.md
    └── arquitectura.md
```

---

## 📦 Paquetes Disponibles

### PAQUETE BÁSICO - S/. 25,000
- Sistema de reclamos completo
- Consulta pública por código
- Panel administrativo
- Notificaciones email
- Encuestas básicas
- Reportes básicos
- Dashboard simple

### PAQUETE PROFESIONAL - S/. 42,000 ⭐ (RECOMENDADO)
- Todo lo del Básico +
- Portal del cliente con login
- Dashboard personal del cliente
- Sistema de comentarios
- Reportes avanzados Indecopi
- Exportación PDF/Excel profesional
- Códigos QR automáticos

### PAQUETE PREMIUM - S/. 58,000
- Todo lo del Profesional +
- Chat en tiempo real (SignalR)
- Notificaciones push en tiempo real
- API REST documentada
- Dashboard ejecutivo avanzado
- Estadísticas con gráficos interactivos
- 1 sesión de capacitación incluida

---

## ⏱️ Tiempos de Desarrollo Estimados

| Paquete | Duración | Horas |
|---------|----------|-------|
| **Básico** | 10-12 semanas | 400-500 hrs |
| **Profesional** | 16-20 semanas | 650-800 hrs |
| **Premium** | 22-26 semanas | 900-1,100 hrs |

---

## 📊 Entidades Principales del Sistema

1. **Usuarios** (clientes, agentes, administradores)
2. **Reclamos** (núcleo del sistema)
3. **Estados** (nuevo, en proceso, resuelto, etc.)
4. **Comentarios** (comunicación interna)
5. **Archivos** (evidencias adjuntas)
6. **Encuestas** (preguntas y respuestas)
7. **Notificaciones** (alertas y emails)

---

## 🔐 Roles y Permisos

1. **Cliente** - Registrar y ver sus reclamos
2. **Agente de Soporte** - Gestionar reclamos asignados
3. **Supervisor** - Asignar casos y ver reportes
4. **Administrador** - Control total del sistema
5. **Ejecutivo** - Solo lectura y reportes estratégicos

---

## 🚀 Roadmap de Implementación

### Fase 1: Fundación (2 semanas)
- Setup del proyecto
- Base de datos
- Autenticación básica

### Fase 2: Módulo de Reclamos (5-6 semanas)
- Formulario público
- Panel administrativo
- Gestión de estados
- Notificaciones email

### Fase 3: Portal del Cliente (4 semanas) - Opcional
- Registro/Login
- Dashboard personal
- Sistema de comentarios

### Fase 4: Encuestas (2 semanas)
- Creador de encuestas
- Sistema de respuestas
- Análisis de resultados

### Fase 5: Reportes y Dashboard (2 semanas)
- Dashboard administrativo
- Reportes Indecopi
- Exportaciones

### Fase 6: Testing y Deploy (2 semanas)
- Testing integral
- Corrección de bugs
- Deploy a producción
- Documentación final

---

## 📞 Contacto

**Desarrollador:** Deca (Decatron)  
**Repositorio:** [https://github.com/decagraff/sistema-reclamos-romero](https://github.com/decagraff/sistema-reclamos-romero)

---

## 📄 Licencia

Este proyecto es propietario de Transportes Romero.  
Todos los derechos reservados © 2025

---

## 🔗 Enlaces Útiles

- [Documentación Técnica Completa](./docs/)
- [Propuesta Comercial](./propuesta/presupuesto-comercial.md)
- [Diagramas del Sistema](./diagramas/)
- [Normativa Indecopi - Libro de Reclamaciones](https://www.indecopi.gob.pe/)

---

**Última actualización:** Noviembre 2025  
**Versión:** 1.0.0 (Planificación)