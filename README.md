# ASOCHIVAS Colombia — Plataforma digital

Plataforma institucional de ASOCHIVAS Colombia: un portal público y directorio neutral de asociados, con herramientas privadas para asociados y administración. El proyecto busca facilitar que las personas conozcan operadores y les soliciten cotizaciones directamente, manteniendo la privacidad, la trazabilidad y la autonomía comercial de cada asociado.

> **Estado:** proyecto en construcción. Las funcionalidades descritas en este README expresan el alcance definido; no implican que ya estén implementadas. La definición de producto y la arquitectura son propuestas para revisión. Los datos institucionales, legales y de asociados solo se publicarán con fuentes y autorizaciones validadas.

## Alcance del producto

La plataforma se organiza en tres espacios:

- **Portal público:** información institucional, directorio con búsqueda y filtros, perfiles y experiencias publicados, noticias, capacitaciones, información de afiliación, contacto y PQR.
- **Portal privado del asociado:** administración de su perfil, vehículos, experiencias, fotografías y documentos; consulta de vigencias y solicitudes de cotización recibidas; respuestas e información institucional autorizada.
- **Panel administrativo:** gestión de usuarios y asociados, revisión y publicación de perfiles y contenidos, documentos, solicitudes, capacitaciones, PQR, auditoría y configuración según permisos.

### Primera entrega (MVP)

El MVP contempla el portal público y directorio; perfiles sujetos a revisión; solicitudes de cotización dirigidas por el visitante a uno o varios asociados (máximo configurable de tres); autenticación y permisos; portal del asociado; administración; gestión documental; contenidos institucionales; notificaciones y auditoría.

Las funcionalidades ampliadas —por ejemplo analítica avanzada, mapas, integraciones adicionales y automatizaciones— podrán incorporarse en fases posteriores sin bloquear la primera entrega.

### Neutralidad y privacidad

ASOCHIVAS funciona como directorio y canal de contacto. No es marketplace ni intermediario comercial. La plataforma no fija tarifas, compara precios, distribuye clientes, reserva servicios, cobra comisiones ni procesa pagos por servicios turísticos.

Cada asociado solo podrá ver la copia de una solicitud que le fue enviada; no conocerá los demás destinatarios ni las respuestas de competidores. El solicitante deberá autorizar el tratamiento de sus datos y su envío a los operadores elegidos. La afiliación o revisión interna no equivale a certificación, habilitación estatal ni garantía del servicio.

## Arquitectura y tecnología

La propuesta técnica es un **monolito modular**: una aplicación desplegable organizada por dominios, sin microservicios en el MVP. Las capas separan presentación, aplicación, reglas de dominio e infraestructura. Los módulos previstos incluyen identidad y permisos, asociados, directorio, flota, experiencias, cotizaciones, documentos, afiliaciones, formación, contenidos, PQR, incidentes, notificaciones y auditoría.

| Área | Base definida |
| --- | --- |
| Aplicación | Next.js 16, React y TypeScript |
| Runtime inicial | Node.js 24 en Hostinger Business |
| Interfaz | Tailwind CSS y sistema de diseño propio |
| Datos | MySQL/MariaDB con InnoDB y migraciones versionadas |
| Archivos privados | Almacenamiento externo compatible con S3 |
| Repositorio y despliegue inicial | GitHub y Hostinger Business |

Las versiones estables y parches deben verificarse antes de instalar o desplegar. ORM, autenticación, proveedores de almacenamiento y correo, pruebas y CI/CD siguen sujetos a decisión técnica. El diseño debe respetar las limitaciones del hosting inicial: sin workers permanentes ni WebSockets entrantes; tareas programadas mediante cron/outbox o servicios externos.

## Organización del código

La estructura evolucionará conforme se implementen los módulos. La arquitectura de referencia propone:

```text
src/
  app/          Rutas públicas, privadas, administración y API
  modules/      Dominios y reglas de negocio
  components/   Componentes reutilizables
  lib/          Adaptadores de infraestructura y utilidades
  styles/       Estilos globales
docs/           Definición de producto, arquitectura y decisiones técnicas
tests/          Pruebas unitarias, integración y E2E
```

Las reglas de negocio viven en sus módulos y no dependen de la interfaz. Un módulo no consulta directamente tablas privadas de otro. La autorización se valida en el servidor para cada operación; los documentos privados no se alojan en `public/`.

## Trabajo en equipo y Pull Requests

Dos integrantes podrán trabajar en paralelo, cada uno en su propio entorno de Codex. Para evitar pisar cambios, cada tarea debe partir de la rama base acordada y trabajarse en una rama propia. Al comenzar el desarrollo se definirá el esquema de ramas del equipo (por ejemplo `feature/<tema>`); las issues se crearán más adelante y no hacen parte de esta etapa.

1. Actualiza la rama base y crea una rama para tu cambio.
2. Mantén el cambio enfocado y evita trabajar sobre la misma rama que tu compañero.
3. Antes del PR, revisa el diff y ejecuta las validaciones disponibles para el cambio.
4. Abre un Pull Request hacia la rama acordada, describe qué cambió y cómo se verificó.
5. El compañero revisa el código; se corrigen observaciones antes de integrar. Los cambios destinados a producción siempre pasan por PR y revisión.
6. Integra únicamente después de aprobación y validaciones acordadas. No se editan archivos directamente en producción.

El flujo objetivo contempla entornos local, desarrollo, staging y producción, con configuración, bases de datos y secretos separados. La automatización CI/CD y la protección de ramas se configurarán en una etapa posterior.

## Desarrollo local

Requisitos actuales del proyecto: Node.js 24 y npm.

```bash
npm install
npm run dev
```

Comandos disponibles:

```bash
npm run lint
npm run build
npm start
```

No agregues secretos al repositorio. Las variables de entorno y su archivo de ejemplo se documentarán cuando se incorporen integraciones que las requieran.

## Seguridad, calidad y operación

La implementación deberá aplicar mínimo privilegio, sesiones seguras, validación en servidor, aislamiento de datos por asociado, almacenamiento privado, consentimiento y auditoría de operaciones sensibles. Los perfiles y contenidos institucionales requieren revisión antes de publicarse; la información jurídica debe provenir de una fuente validada.

La estrategia de aceptación prevista incluye pruebas de reglas críticas, APIs y permisos, aislamiento entre asociados, flujos de cotización y documentos, accesibilidad (objetivo WCAG 2.2 AA), rendimiento, seguridad, SEO y restauración de respaldos. No se considera listo para producción hasta verificar permisos, privacidad, contenido autorizado, monitoreo y recuperación.

## Documentación del proyecto

Los documentos de referencia para el alcance y diseño son la **Definición del producto**, la **Arquitectura de software** y el **Pliego Maestro de desarrollo**. La arquitectura prevé documentar decisiones, requisitos, modelo de datos, permisos y despliegue en `docs/` a medida que se revisen y aprueben.


