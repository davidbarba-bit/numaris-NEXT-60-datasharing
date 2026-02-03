# NEXT-60: Data Sharing Hub

Prototipo interactivo del módulo de Data Sharing para la plataforma Next de Numaris.

## 🚀 Ver el prototipo

### Opción 1: Replit (recomendado)
1. Importa este repo en [Replit](https://replit.com)
2. Click en **Run**
3. El prototipo se abre automáticamente

### Opción 2: Local
```bash
# Con Python
cd prototype
python3 -m http.server 8080
# Abre http://localhost:8080

# Con Node
npx serve prototype
```

## 📁 Estructura

```
├── README.md           # Este archivo
├── PRD.html            # Documento de Producto (PRD)
└── prototype/
    └── index.html      # Prototipo interactivo
```

## 🎨 Stack del prototipo

- **React 18** - UI Library
- **Ant Design 5.20.6** - Component library
- **Source Sans 3** - Tipografía Numaris

## 📋 Feature

**Data Sharing** permite a los clientes de Next compartir datos de su flota con sistemas externos:

- **API Keys** - Acceso programático a datos
- **Webhooks Salientes** - Push de eventos a sistemas externos
- **Webhooks Entrantes** - Recibir datos de ERPs/TMS
- **Conexiones** - Integraciones pre-configuradas (Slack, SAP, etc.)

---

*Generado para Numaris Next - 2026*
