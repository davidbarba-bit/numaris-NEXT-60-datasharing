# CLAUDE.md - Instrucciones del proyecto NEXT-60

## Proyecto
**NEXT-60: Data Sharing Hub** - Prototipo interactivo para Numaris Next.
Permite a clientes compartir datos de flota con sistemas externos via API Keys, Webhooks y MCP Server.

## Estructura
```
├── CLAUDE.md              # Este archivo (instrucciones para Claude)
├── AGENTS.md              # Definición de roles del equipo (PO, QA, UX/UI, Frontend, Backend)
├── DESIGN_SYSTEM.md       # Design System completo: tokens, componentes, patrones CSS
├── PRD.html               # Documento de requisitos del producto (fuente de verdad)
├── README.md              # Descripción general del proyecto
└── prototype/
    └── index.html         # Prototipo interactivo (self-contained, single-file)
```

## Stack del prototipo
- React 18 (UMD via CDN - NO JSX, usar React.createElement)
- Ant Design 5.20.6 (UMD via CDN)
- @ant-design/icons 5.2.6 (UMD via CDN)
- Day.js 1.11.11 (UMD via CDN)
- Tipografía: Source Sans 3
- Sin build step - el HTML funciona directamente en browser

## Reglas de desarrollo
1. **Single-file:** Todo el código va en `prototype/index.html`
2. **Sin JSX:** Usar `e(Component, props, children)` donde `var e = React.createElement`
3. **Sin dependencias nuevas:** Solo las CDN ya declaradas en el HTML
4. **Sin build step:** No Node.js, no npm, no webpack. Abrir en browser y listo
5. **Idioma UI:** Español (labels, mensajes, placeholders)
6. **Idioma código:** Inglés (variables, funciones, comentarios técnicos)

## Agent Teams
Ver `AGENTS.md` para la definición completa de roles. Resumen:
- **PO:** Define alcance y aprueba flujos. Referencia: `PRD.html`
- **QA:** Valida flujos, happy paths y edge cases
- **UX/UI:** Diseña pantallas siguiendo Ant Design + Design System Numaris
- **Frontend:** Implementa en React.createElement sin build step
- **Backend:** Revisa factibilidad de API contracts y arquitectura

## Workflow
```
PO → UX/UI → PO aprueba → Frontend implementa → Backend revisa → QA valida → PO aprueba
```

## Convenciones Git
- Branch principal de desarrollo: `claude/setup-agent-teams-mode-2qJGd`
- Commits en español descriptivo
- Prefijo de commits: `NEXT-60:`
