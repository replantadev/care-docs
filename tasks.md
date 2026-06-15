---
title: Tareas de mantenimiento
layout: default
---

# Tareas de mantenimiento

Care ejecuta todas las tareas via **Action Scheduler** (WooCommerce) para garantizar que no afectan al rendimiento del sitio en produccion. Cada tarea es independiente: si una falla, las demas continuan.

## Actualizaciones (`task-updates`)

Gestiona el ciclo completo de actualizaciones de WordPress.

**Flujo:**
1. Detecta actualizaciones disponibles (core, plugins, temas)
2. Crea backup del sitio antes de actualizar
3. Aplica las actualizaciones
4. Ejecuta health check post-update
5. Si el sitio no responde: rollback automatico

**Configuracion:**
- Modo: Manual / Automatico / Solo seguridad
- Exclusiones: plugins o temas a no actualizar automaticamente
- Ventana de mantenimiento: hora del dia para ejecutar

Disponible en: Semilla, Raiz, Ecosistema

---

## Health Check (`task-health`)

Revision periodica del estado del sitio.

Comprueba:
- Conectividad HTTP (respuesta 200)
- Conexion a base de datos
- Version PHP vs. recomendada
- Espacio en disco disponible
- Disponibilidad de WooCommerce (si aplica)
- Respuesta del REST API de WordPress

Disponible en: Semilla, Raiz, Ecosistema

---

## Seguridad (`task-security`)

Escaneo de vulnerabilidades e integridad del sitio.

Comprueba:
- Plugins con vulnerabilidades conocidas (via WPVulnDB)
- Cambios en archivos criticos (wp-config.php, .htaccess)
- Usuarios administradores no reconocidos
- Intentos de login fallidos excesivos
- Permisos de archivos inseguros

Disponible en: Raiz, Ecosistema

---

## Rendimiento WPO (`task-wpo`)

Optimizacion de base de datos y cache.

Incluye:
- Limpieza de revisiones antiguas de posts
- Vaciado de cache de objetos (si hay plugin activo)
- Optimizacion de tablas de base de datos
- Limpieza de transients expirados

Disponible en: Raiz, Ecosistema

---

## Core Web Vitals (`task-cwv`)

Monitorizacion de metricas de experiencia de usuario.

Mide y alerta sobre:
- LCP (Largest Contentful Paint) > 2.5s
- CLS (Cumulative Layout Shift) > 0.1
- FID / INP elevados

Disponible en: Ecosistema

---

## Errores 404 (`task-404`)

Registro y analisis de URLs no encontradas.

- Registra las 404 mas frecuentes con origen (referrer)
- Sugiere redirecciones para las mas impactantes
- Alerta si una URL critica pasa a 404

Disponible en: Raiz, Ecosistema

---

## Anomalias (`task-anomaly`)

Deteccion de comportamientos inusuales.

Detecta:
- Picos de trafico inesperados
- Caidas de trafico respecto a la semana anterior
- Errores PHP / JS elevados
- Tasa de errores de formularios

Disponible en: Ecosistema

---

## Medios huerfanos (`task-orphan-media`)

Identificacion y limpieza de archivos de media sin usar.

- Lista archivos de la biblioteca de medios sin adjuntar a ningun post
- Limpieza manual desde el panel o automatica (segun configuracion)
- No elimina nunca sin confirmacion o habilitacion explicita

Disponible en: Ecosistema

---

## SEO basico (`task-seo`)

Revision de elementos SEO fundamentales.

Comprueba:
- Titulo y descripcion de la home
- Robots.txt accesible
- Sitemap presente y accesible
- Canonical tags en posts principales
- Links rotos en paginas clave

Disponible en: Ecosistema

---

## Staging (`task-staging`)

Gestion del entorno de desarrollo/pruebas.

- Sincronizacion de base de datos de produccion a staging
- Desactivacion de emails en staging
- Activacion/desactivacion de modo mantenimiento en staging

Disponible en: Ecosistema

---

## Backup (`integrations-backup`)

Copia de seguridad externa via Backblaze B2.

- Backup completo (BD + archivos) subido a Backblaze B2 con prefijo `{dominio}/backup_{fecha}/`
- Backup previo automatico antes de aplicar actualizaciones
- Frecuencia segun plan: semanal (Semilla), diario (Raiz/Ecosistema), cada 12h (addon Ecommerce)
- Las credenciales B2 se configuran desde Replanta Hub y se envian al plugin automaticamente

Disponible en: Todos (nivel de detalle segun plan)

---

## Cloudflare (`task-cloudflare`)

Integracion con la cuenta Cloudflare del sitio.

- Purgado de cache tras actualizaciones
- Estado del dominio (DNS, SSL)
- Estadisticas de trafico via API Cloudflare

Disponible en: Ecosistema (requiere API token Cloudflare)

---

## Reportes (`task-report`)

Generacion de informes periodicos para el cliente.

Incluye:
- Resumen de tareas ejecutadas
- Actualizaciones aplicadas
- Incidencias detectadas y resueltas
- Metricas de salud del sitio

Frecuencia: mensual (Semilla), semanal (Raiz y Ecosistema)

Disponible en: Todos

---

[Ver planes y precios](https://replanta.net/mantenimiento-wordpress/#planes) | [Volver al inicio](index.md)
