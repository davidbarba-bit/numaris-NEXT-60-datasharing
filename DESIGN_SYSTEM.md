# Numaris/NEXT - Design System & Style Library

Referencia completa de diseño para el equipo de desarrollo. Este documento refleja los estilos, componentes y patrones utilizados en la plataforma **Numaris Next** (frontend-router-level3).

---

## 1. Stack de la plataforma

```
Framework:     Next.js 13.4.17
UI Library:    Ant Design 5.20.6
Icons:         @ant-design/icons 5.2.5
State:         Jotai 2.14.0 + Immer
Forms:         Formik 2.4.3 + Yup 1.2.0
Dates:         Day.js 1.11.11
HTTP:          Axios 1.12.0
Queries:       @tanstack/react-query 4.32.6
Maps:          Google Maps (@googlemaps/react-wrapper)
Styles:        SCSS (Sass 1.65.1)
Testing:       Jest 29 + Testing Library + Cypress 14
Linting:       ESLint (Airbnb) + Prettier 3.2.5 + Stylelint
TypeScript:    5.1.6
Auth:          AWS Amplify 6.0.17
Monitoring:    Bugsnag + LogRocket
```

### Dependencias clave
| Paquete | Versión | Uso |
|---------|---------|-----|
| `antd` | 5.20.6 | Componentes UI |
| `@ant-design/icons` | 5.2.5 | Iconografía |
| `@ant-design/colors` | 7.2.0 | Paleta de colores |
| `jotai` | 2.14.0 | Estado global (atoms) |
| `jotai-immer` | 0.2.0 | Mutations inmutables |
| `formik` | 2.4.3 | Gestión de formularios |
| `yup` | 1.2.0 | Validación de esquemas |
| `dayjs` | 1.11.11 | Fechas y tiempos |
| `react-dnd` | 16.0.1 | Drag & drop |
| `react-table` | 7.8.0 | Tablas avanzadas |
| `rxjs` | 7.8.1 | Streams reactivos |
| `supercluster` | 8.0.1 | Clustering de mapas |

---

## 2. Variables CSS (Design Tokens)

```css
:root {
  /* ── Primary Colors ── */
  --primary: #1867FF;
  --primary-light: #d6e4ff;
  --primary-dark: #2f54eb;

  /* ── Text Colors ── */
  --text-primary: #3F3F3F;
  --text-secondary: #8c8c8c;
  --text-muted: rgba(0, 0, 0, 0.45);

  /* ── Background Colors ── */
  --bg-page: #f0f2f5;
  --bg-card: #ffffff;
  --bg-header: #FAFAFA;
  --bg-hover: #f5f5f5;

  /* ── Border Colors ── */
  --border-light: #f0f0f0;
  --border-default: #d9d9d9;

  /* ── Status Colors ── */
  --success: #52c41a;
  --success-bg: #f6ffed;
  --warning: #faad14;
  --warning-bg: #fffbe6;
  --error: #ff4d4f;
  --error-bg: #fff1f0;
  --inactive: #8c8c8c;
  --inactive-bg: #f5f5f5;

  /* ── Spacing / Radius ── */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;

  /* ── Typography ── */
  --font-family: "Source Sans 3", -apple-system, BlinkMacSystemFont,
                 "Segoe UI", Roboto, sans-serif;
  --font-size-sm: 13px;
  --font-size-base: 14px;
  --font-size-lg: 16px;
  --font-size-xl: 18px;
}
```

### Resumen rápido de colores

| Token | Valor | Uso |
|-------|-------|-----|
| `--primary` | `#1867FF` | Acciones principales, enlaces, hover, ink-bar |
| `--primary-dark` | `#2f54eb` | Botones primarios (background + border) |
| `--primary-light` | `#d6e4ff` | Fondo de tags seleccionados |
| `--text-primary` | `#3F3F3F` | Texto principal en toda la app |
| `--text-secondary` | `#8c8c8c` | Texto secundario, helpers |
| `--bg-page` | `#f0f2f5` | Fondo general de la app |
| `--bg-header` | `#FAFAFA` | Fondo de headers de tabla, sidebar |
| `--border-light` | `#f0f0f0` | Bordes sutiles, separadores |
| `--border-default` | `#d9d9d9` | Bordes de cards, inputs |
| `--success` | `#52c41a` | Activo, éxito |
| `--warning` | `#faad14` | Pendiente, advertencia |
| `--error` | `#ff4d4f` | Error, eliminar, peligro |
| `--inactive` | `#8c8c8c` | Inactivo, deshabilitado |

---

## 3. Tipografía

```
Fuente principal: Source Sans 3
Fallback:         -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif
Monospace:        'SF Mono', Monaco, monospace (para tokens/código)

Tamaños:
  sm:   13px  (texto secundario, helpers, tags)
  base: 14px  (texto normal, labels, items de menú)
  lg:   16px  (títulos de sidebar)
  xl:   18px  (títulos de página)

Pesos:
  400: Normal (texto corrido)
  500: Medium (enlaces, badges)
  600: Semibold (headers de tabla, títulos, items activos)
  700: Bold (disponible pero poco usado)

Anti-aliasing:
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
```

---

## 4. Componentes de Layout

### 4.1 ModuleSidebar

Barra lateral fija de navegación con grupos colapsables.

```
Ancho:          250px
Background:     #fafafa
Borde derecho:  1px solid #f0f0f0
Posición:       fixed, left: 0, top: 64px (debajo del header)
Padding top:    24px

Título:
  Padding:      0 24px 12px
  Font-weight:  600
  Font-size:    16px
  Color:        #333

Items:
  Padding:      10px 16px
  Margin-bottom: 4px
  Border-radius: 6px
  Font-size:    14px
  Color normal: rgba(0, 0, 0, .85)
  Color activo: #262626
  BG activo:    #f5f5f5
  Weight activo: 600
  Hover class:  .sidebar-item-hover → background: #f5f5f5

Grupos:
  Weight:       600
  Icono expand: PlusOutlined (12px, #262626)
  Icono collapse: MinusOutlined (12px, #262626)
  Children padding-left: 8px
  Hover class:  .sidebar-group-header → background: #f0f0f0
```

### 4.2 ModulePageHeader

Header sticky de página con título, búsqueda y acción principal.

```
Background:     #fff
Padding:        16px 24px
Border-bottom:  1px solid #f0f0f0
Position:       sticky, top: 0, z-index: 99
Display:        flex, space-between, align-center
Margin:         -24px (left, right, top) para full-width

Título:
  Level:        h4 (Title level={4})
  Font-weight:  600
  Font-size:    18px
  Margin:       0

Botón back:
  Icono:        ArrowLeftOutlined
  Clase:        module-icon-button
  Border-radius: 8px

Botón primario:
  Border-radius: 4px
  Height:       32px
  Padding:      0 16px
  Font-weight:  500
  Background:   #2f54eb
  Border-color: #2f54eb
```

### 4.3 ModulePanel

Contenedor blanco para contenido.

```
Background:     #fff
Border-radius:  8px
Border:         1px solid #f0f0f0
Padding:        24px (default)
Height:         100%
Overflow:       hidden
Display:        flex, column
```

### 4.4 ModuleFormPage

Layout completo para formularios con header fijo y área scrollable.

```
Header:
  Background:   #fff
  Padding:      16px 24px
  Border-bottom: 1px solid #f0f0f0
  Botón cancelar: default
  Botón guardar: primary (#2f54eb)

Content:
  Flex:         1
  Padding:      24px
  Background:   #fff
  Overflow-y:   auto
  Max-width:    98%
  Margin:       0 auto

Container (si no noContainer):
  Background:   #fff
  Border-radius: 8px
  Border:       1px solid #f0f0f0
  Padding:      24px
  Box-shadow:   0 1px 2px rgba(0,0,0,0.03)
```

---

## 5. Componentes de Configuración

### 5.1 ConfigCard

```
Bordered:       true
Border-radius:  12px
Border-color:   #d9d9d9
Box-shadow:     0 1px 2px rgba(0,0,0,0.03)
Margin-bottom:  24px
```

### 5.2 ConfigSection

```
Margin-bottom:  24px
```

### 5.3 FormLabel

```
Display:        block
Font-weight:    bold (Text strong)
Margin-bottom:  8px
Required:       * en #ff4d4f, margin-right: 4px
```

### 5.4 FormHelperText

```
Type:           secondary
Font-size:      13px
Display:        block
Margin-top:     4px
```

### 5.5 StatusBadge

```
Display:        inline-block
Padding:        2px 8px
Border-radius:  10px
Font-size:      12px
Font-weight:    500

Variantes:
  active:   bg: #f6ffed  color: #52c41a  label: "Activo"
  pending:  bg: #fffbe6  color: #faad14  label: "Pendiente"
  inactive: bg: #f5f5f5  color: #8c8c8c  label: "Inactivo"
  error:    bg: #fff1f0  color: #ff4d4f  label: "Error"
```

---

## 6. Estilos de Tabla (.module-table)

### Header

```css
Background:     #FAFAFA
Color:          #3F3F3F
Font-weight:    600
Font-size:      14px
Border-bottom:  1px solid #f0f0f0
Padding:        12px 16px
White-space:    nowrap
```

### Sort

```
Icono inactivo: #bfbfbf
Icono activo:   #1867FF
Sin pseudo-elementos ::before/::after
Sin separadores de columna (::before transparent)
```

### Filter

```
Icono inactivo: #bfbfbf
Icono activo:   #1867FF
```

### Body

```
Padding:        12px 16px
Font-size:      13px
Border-bottom:  1px solid #f0f0f0
Color:          #3F3F3F
Hover BG:       #fafafa
```

### Pagination

```
Margin:         16px 0
Justify:        center
```

### Links en tabla

```
Color:          #1867FF
Font-weight:    500
Hover:          underline
```

### Empty State

```
BG placeholder: #f5f7fa
Cell border:    none
Padding cell:   0
Empty margin:   48px 0
```

---

## 7. Botón de Icono (.module-icon-button)

```css
Border-radius:  8px
Width:          32px
Height:         32px
Padding:        0
Display:        flex, center
Border-color:   #d9d9d9
Background:     #fff
Transition:     all 0.2s

Hover:
  Border-color: #1867FF
  Color:        #1867FF

Icono:
  Font-size:    14px
  SVG centered
```

---

## 8. Tabs (.module-tabs)

```css
Nav margin-bottom: 0
Border-bottom:     #f0f0f0

Tab:
  Padding:      12px 0
  Margin-right: 32px
  Font-size:    14px
  Color:        #3F3F3F
  Hover color:  #1867FF

Tab activo:
  Color:        #1867FF
  Font-weight:  600
  Text-shadow:  none

Ink bar:
  Background:   #1867FF
  Height:       2px
```

---

## 9. Permission Tags

```css
.permission-tag:
  Transition:   all 0.2s
  Color hereda a span, div, svg

Hover normal:
  Border-color: #1867FF
  Color:        #1867FF

Hover checked:
  Background:   #d6e4ff (primary-light)

Hover delete:
  Border-color: #ff4d4f
  Color:        #ff4d4f

Hover delete+checked:
  Background:   #fff1f0 (error-bg)
```

---

## 10. Overrides globales de Ant Design

### Botones
```
.module-page .ant-btn:         border-radius: 8px
.ant-btn-primary:              color: #ffffff (forzado)
.ant-btn span:                 color: inherit
```

### Cards
```
.module-page .ant-card:        border-radius: 12px, border-color: #d9d9d9
```

### Layout
```
.ant-layout:                   background: #f0f2f5
```

### Menú
```
Selected/Hover items:          color: #1867FF (forzado a todo: a, span)
```

### Transfer
```
.ant-transfer-operation:       hidden (display: none, width: 0)
.ant-transfer:                 display: flex, gap: 24px
.ant-transfer-list:            flex: 1
```

### Dropdown (danger items)
```
Hover:                         color: white (texto + icono)
```

---

## 11. Patrones de código

### Ant Design ConfigProvider theme

```javascript
// Para el prototipo (sin JSX)
var theme = {
  token: {
    colorPrimary: '#1867FF',
    colorText: '#3F3F3F',
    colorTextSecondary: '#666666',
    fontFamily: '"Source Sans 3", sans-serif',
    borderRadius: 8
  }
};
```

### Código monospace (tokens, secrets)

```css
code {
  background: #FAFAFA;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 12px;
  border: 1px solid #f0f0f0;
  font-family: 'SF Mono', Monaco, monospace;
}

.masked-token {
  font-family: 'SF Mono', Monaco, monospace;
  letter-spacing: 2px;
}
```

### Code blocks (dark theme)

```css
.code-block {
  background: #1e1e1e;
  color: #d4d4d4;
  padding: 16px;
  border-radius: 8px;
  font-family: 'SF Mono', Monaco, monospace;
  font-size: 13px;
  overflow-x: auto;
}
```

---

## 12. Responsive

```css
/* Mobile breakpoint */
@media (max-width: 768px) {
  .ant-layout-sider {
    width: 0 !important;
    position: absolute;
    z-index: 1000;
  }
  .ant-layout {
    margin-left: 0 !important;
  }
}
```

---

## 13. Resumen visual rápido

```
┌─────────────────────────────────────────────────────────┐
│  Header: #fff, 64px, border-bottom #f0f0f0             │
├──────────┬──────────────────────────────────────────────┤
│ Sidebar  │  Content: #f0f2f5 padding 24px              │
│ #fafafa  │                                              │
│ 250px    │  ┌─ ModulePageHeader ──────────────────┐    │
│ fixed    │  │ Title (18px 600)    [Search] [+Btn] │    │
│          │  └─────────────────────────────────────┘    │
│ Items:   │                                              │
│  14px    │  ┌─ ModulePanel ───────────────────────┐    │
│  hover   │  │ #fff, radius 8px, border #f0f0f0   │    │
│  #f5f5f5 │  │                                     │    │
│          │  │  ┌─ Table (.module-table) ────────┐ │    │
│ Active:  │  │  │ Header: #FAFAFA 14px 600       │ │    │
│  #f5f5f5 │  │  │ Body: 13px, hover #fafafa      │ │    │
│  600     │  │  │ Pagination: center              │ │    │
│  #262626 │  │  └────────────────────────────────┘ │    │
│          │  └─────────────────────────────────────┘    │
└──────────┴──────────────────────────────────────────────┘
```

---

*Fuente: Style Library de frontend-router-level3 (Numaris/NEXT)*
*Última actualización: 2026-02-09*
