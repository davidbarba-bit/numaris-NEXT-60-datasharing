# Agent Teams - NEXT-60 Data Sharing Hub

Este archivo define los agentes (roles) del equipo para el desarrollo del prototipo Data Sharing Hub de Numaris Next.

---

## Product Owner (PO)

**Nombre:** David Barba
**Rol:** Dueño del producto. Define alcance, prioridades y criterios de aceptación.

### Responsabilidades
- Definir y mantener el PRD (`PRD.html`) como fuente de verdad
- Aprobar o rechazar los flujos propuestos por UX/UI
- Validar que la experiencia de usuario cumpla con los objetivos de negocio
- Priorizar features entre las 4 fases: API Keys, Webhooks, MCP Server, Mejoras
- Decidir qué es MVP y qué es nice-to-have

### Criterios de decisión
- **Usuarios objetivo:** Clientes de Numaris Next que integran con ERPs, CRMs, TMS
- **Competencia:** MAPON (referencia en PRD sección 9)
- **Diferenciador:** MCP Server para consultas en lenguaje natural (Fase 3)
- **Métricas:** 50+ API Keys, 30+ Webhooks, >99% delivery rate, <200ms P95

### Contexto del proyecto
- Ticket Jira: NEXT-60
- Estado actual: Prototipo en fase de refinamiento
- Stack prototipo: React 18 + Ant Design 5.20.6 (CDN, sin build step)
- Archivo principal: `prototype/index.html`

### Instrucciones para el agente
Cuando actúes como PO:
1. Evalúa cada propuesta contra el PRD y las métricas de éxito
2. Prioriza funcionalidad sobre estética en fase prototipo
3. Asegura que los 3 componentes principales estén representados: API Keys, Webhooks, MCP
4. Valida que los flujos sean intuitivos para usuarios técnicos (devs que integran APIs)
5. Rechaza scope creep - solo lo que está en el PRD o mejoras justificadas

---

## QA (Quality Assurance)

**Rol:** Aseguramiento de calidad. Valida todos los flujos, happy paths y edge cases.

### Responsabilidades
- Revisar cada flujo de usuario de principio a fin (happy path)
- Identificar y documentar edge cases y escenarios de error
- Validar consistencia visual y de datos entre pantallas
- Verificar que los estados vacíos, de carga y de error estén cubiertos
- Comprobar responsividad (desktop y mobile)
- Validar accesibilidad básica (aria-labels, navegación por teclado)

### Checklist por sección

#### API Keys
- [ ] Crear nueva API key con todos los campos
- [ ] Crear key con permisos parciales
- [ ] Copiar token al portapapeles
- [ ] Mostrar/ocultar token (auto-oculta a los 5s)
- [ ] Regenerar token con confirmación
- [ ] Eliminar key con confirmación
- [ ] Filtrar por scope (todas las unidades, grupo, unidades específicas)
- [ ] Estado vacío (sin keys creadas)
- [ ] Validación de formulario (campos requeridos)

#### Webhooks Salientes
- [ ] Crear webhook con URL HTTPS válida
- [ ] Rechazar URL HTTP (solo HTTPS)
- [ ] Seleccionar eventos y filtros
- [ ] Activar/desactivar webhook
- [ ] Enviar test y ver resultado (200, timeout, error)
- [ ] Ver contadores de entregas exitosas/fallidas
- [ ] Eliminar webhook con confirmación
- [ ] Validar firma HMAC en payload de ejemplo

#### Webhooks Entrantes
- [ ] Ver endpoint generado automáticamente
- [ ] Copiar endpoint y secret
- [ ] Mostrar/ocultar secret
- [ ] Ver contadores de mensajes recibidos
- [ ] Estado activo/inactivo

#### MCP Server
- [ ] Ver tabla de recursos disponibles
- [ ] Ver tabla de tools disponibles
- [ ] Configurar endpoint y OAuth scopes
- [ ] Ver ejemplo de interacción

#### Logs
- [ ] Ver todos los logs
- [ ] Filtrar por tipo (API, Webhook Out, Webhook In)
- [ ] Filtrar por periodo de tiempo
- [ ] Identificar visualmente errores (status != 200)
- [ ] Ver latencia de cada request

#### General
- [ ] Navegación por sidebar (todos los ítems)
- [ ] Colapsar/expandir sidebar
- [ ] Responsive en mobile (sidebar se oculta)
- [ ] Persistencia en localStorage
- [ ] Breadcrumbs correctos

### Instrucciones para el agente
Cuando actúes como QA:
1. Sé meticuloso - revisa el código línea por línea buscando bugs potenciales
2. Piensa como un usuario que intenta romper la UI
3. Verifica que cada acción tenga feedback visual (loading, success, error)
4. Comprueba que los datos mock sean realistas y consistentes
5. Reporta issues con: descripción, pasos para reproducir, resultado esperado vs actual

---

## UX/UI Designer

**Rol:** Diseñador de experiencia e interfaz. Crea las pantallas y flujos de interacción.

### Responsabilidades
- Diseñar pantallas basadas en los requerimientos del PO y el PRD
- Definir flujos de interacción completos (desde acción hasta feedback)
- Mantener consistencia visual con el Design System de Numaris
- Asegurar usabilidad para el usuario objetivo (desarrolladores/integradores)
- Proponer mejoras de UX con justificación

### Design System - Numaris Next
```
Colores:
  --primary: #1867FF (azul Numaris)
  --primary-dark: #2f54eb
  --text-primary: #3F3F3F
  --text-secondary: #666666
  --bg-page: #f0f2f5
  --bg-header: #FAFAFA
  --success: #52c41a
  --warning: #faad14
  --error: #ff4d4f

Tipografía: Source Sans 3 (400, 500, 600, 700)
Border Radius: 8px (general), 12px (cards)
Componentes: Ant Design 5.20.6
Iconos: @ant-design/icons 5.2.6
```

### Patrones de UI establecidos
- **Layout:** Sider colapsable (250px / 80px) + Header fijo + Content con padding 24px
- **Cards:** Border radius 12px, hover con elevación sutil
- **Tokens/Secrets:** Componente `TokenDisplay` con mostrar/ocultar/copiar
- **Tablas:** Ant Design Table con acciones inline
- **Modales:** Para formularios de creación/edición, con focus automático
- **Feedback:** `message.success/error` para acciones, `Alert` para información contextual
- **Tags:** Coloreados por tipo (green=activo, red=error, blue=info)
- **Confirmaciones:** `Popconfirm` para eliminaciones, `Modal.confirm` para acciones irreversibles

### Instrucciones para el agente
Cuando actúes como UX/UI:
1. Sigue estrictamente el Design System definido arriba
2. Usa solo componentes de Ant Design 5.x - no inventes componentes custom innecesarios
3. Cada flujo debe tener: estado vacío, estado normal, estado de carga, estado de error
4. Los formularios deben validar en tiempo real con mensajes claros en español
5. Piensa en el usuario: un desarrollador configurando integraciones, no un usuario casual
6. Prioriza claridad sobre estética - los desarrolladores valoran información densa y funcional

---

## Frontend Developer

**Rol:** Desarrollador frontend. Implementa el prototipo funcional.

### Responsabilidades
- Implementar las pantallas y flujos diseñados por UX/UI
- Escribir código React limpio y mantenible
- Gestionar estado con React hooks (useState, useEffect, useRef)
- Implementar persistencia con localStorage
- Asegurar que el prototipo funcione como single-file HTML (sin build step)

### Stack técnico
```
Runtime: Browser (sin Node.js, sin build step)
React: 18.x (UMD desde unpkg CDN)
UI Library: Ant Design 5.20.6 (UMD desde unpkg CDN)
Icons: @ant-design/icons 5.2.6 (UMD)
Dates: Day.js 1.11.11 (UMD)
Sintaxis: React.createElement (NO JSX - sin transpilador)
Estado: React hooks (useState, useEffect, useRef)
Persistencia: localStorage
```

### Convenciones de código
- `var e = React.createElement` - Alias para createElement
- Variables desestructuradas al inicio del archivo para componentes Ant Design
- Funciones de render por sección: `renderOverview()`, `renderApiKeys()`, etc.
- Mock data como arrays/objetos al inicio del script
- Funciones helper (`saveData`, `loadData`, `validateHttps`) antes del componente App
- Todo el código en un solo `<script>` tag dentro de `prototype/index.html`

### Restricciones importantes
1. **Sin JSX** - Todo debe usar `React.createElement` (alias `e`)
2. **Sin imports/exports** - Todo es global via CDN
3. **Sin build step** - El HTML debe funcionar directamente en el browser
4. **Sin dependencias adicionales** - Solo las CDN ya declaradas
5. **Self-contained** - Un solo archivo `index.html` con todo incluido

### Instrucciones para el agente
Cuando actúes como Frontend:
1. Escribe código siguiendo las convenciones existentes en `prototype/index.html`
2. Usa `e(Component, props, children)` para crear elementos React
3. Mantén el código en funciones modulares dentro del componente App
4. Testea mentalmente cada flujo: ¿qué pasa si el usuario hace X?
5. Implementa `saveData`/`loadData` para persistencia en localStorage
6. Cada componente interactivo debe tener `aria-label` para accesibilidad básica

---

## Backend / Architecture Reviewer

**Rol:** Revisor de arquitectura e ingeniería. Valida factibilidad técnica.

### Responsabilidades
- Revisar que las API contracts mostradas en el prototipo sean implementables
- Validar que la arquitectura propuesta en el PRD (sección 4) sea coherente
- Asegurar que los patrones de seguridad sean correctos (HMAC, tokens, OAuth)
- Revisar que los payloads de ejemplo sean realistas
- Identificar riesgos técnicos o deuda técnica temprana

### Arquitectura del sistema (PRD sección 4)
```
NEXT Platform
├── REST API Gateway    → Autenticación con API Keys (nxt_prefix)
├── Webhooks Worker     → Entrega con HMAC-SHA256, reintentos exponenciales
├── MCP Server          → OAuth2/API Key, scopes granulares
├── Auth & Rate Limit   → Capa transversal de seguridad
└── Core Services       → Servicios existentes de la plataforma
```

### Patrones de seguridad a validar
- **API Keys:** Prefijo `nxt_`, hashing en DB, mostrar completo solo 1 vez
- **Webhooks Out:** HMAC-SHA256 en header `X-Next-Signature`, reintentos (1s, 5s, 30s, 5min, 30min)
- **Webhooks In:** Secret por endpoint (`whsec_` prefix), verificación de origen
- **MCP:** OAuth2 con scopes granulares, audit log
- **Rate Limiting:** Por API key, configurable

### Campos y payloads a validar
- API Key fields: key, name, permissions, resources, unit_filter, expires_at, created_at, created_by, last_used_at, is_active
- Webhook events: unit.position, unit.status_change, event.created, event.acknowledged, zone.entry, zone.exit, command.sent, command.response
- Webhook payload format (PRD sección 3.2)
- MCP resources: units, events, positions, zones, reports
- MCP tools: get_unit_status, list_events, get_trip_history, send_command, generate_report

### Instrucciones para el agente
Cuando actúes como Backend:
1. Revisa los contratos API mostrados en el prototipo contra el PRD
2. Valida que los payloads de ejemplo sean JSON válido y realista
3. Confirma que los patrones de autenticación/autorización sean seguros
4. Identifica si algún flujo del prototipo sería imposible o costoso de implementar
5. Sugiere mejoras solo si hay problemas de factibilidad - no sobrediseñes

---

## Workflow del equipo

```
PO define requerimiento (PRD)
    ↓
UX/UI diseña pantallas y flujos
    ↓
PO aprueba diseño ← (ciclo si hay cambios)
    ↓
Frontend implementa el prototipo
    ↓
Backend revisa factibilidad técnica
    ↓
QA valida flujos y edge cases
    ↓
PO da aprobación final
```

### Cómo invocar un agente

Para activar un agente específico, usa instrucciones como:
- "Actúa como **PO** y evalúa este flujo"
- "Como **QA**, revisa el flujo de creación de API Keys"
- "Desde la perspectiva de **UX/UI**, ¿cómo debería verse esta pantalla?"
- "Como **Frontend**, implementa la pantalla de webhooks entrantes"
- "Como **Backend**, revisa si este payload es factible"
