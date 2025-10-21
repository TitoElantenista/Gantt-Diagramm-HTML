# 📊 Gantt Editor - Standalone HTML

## Descripción

**Gantt Editor** es una aplicación web completamente standalone (un solo archivo HTML) que permite crear, editar y visualizar diagramas de Gantt de manera interactiva, sin necesidad de Python ni servidor backend.

## ✨ Características

### 🎯 Gestión de Tareas
- **Crear tareas** y **meilensteins** con formulario visual
- **Editar** cualquier tarea haciendo clic sobre ella
- **Eliminar** tareas individualmente
- **Organizar** por grupos/fases
- **Fechas de inicio y fin**
- **Duración planificada** (opcional)
- **Tonnage** (opcional)
- **Texto personalizado** en barras

### 📈 Visualización
- **Diagrama Gantt interactivo** con Plotly
- **Zoom horizontal y vertical independiente**
- **Línea de "Hoy"** para referencia temporal
- **Slider de rango** para navegación temporal
- **Colores por grupo** automáticos
- **Tooltips informativos**

### 💾 Persistencia
- **Guardar configuración** como archivo JSON
- **Cargar configuración** desde JSON
- **Exportar/importar** proyectos completos

### 🎨 Interfaz
- **Diseño moderno** y responsive
- **Pestañas** para organizar: Tareas y Configuración
- **Lista de tareas** con preview
- **Estados vacíos** informativos
- **Validación de formularios**

## 🚀 Uso

### Método 1: Abrir directamente
```bash
# Navegar a la carpeta
cd gantt-editor

# Abrir en el navegador
xdg-open gantt-editor.html   # Linux
open gantt-editor.html        # macOS
start gantt-editor.html       # Windows
```

### Método 2: Servidor local (opcional)
```bash
# Python 3
python3 -m http.server 8000

# Luego abrir: http://localhost:8000/gantt-editor.html
```

## 📋 Workflow Típico

1. **Añadir Tareas**
   - Clic en "+ Aufgabe" o "★ Meilenstein"
   - Rellenar formulario (grupo, nombre, fechas)
   - Guardar

2. **Configurar Proyecto**
   - Ir a pestaña "Konfiguration"
   - Establecer título del proyecto
   - Seleccionar Bundesland por defecto
   - Configurar visualización

3. **Generar Diagrama**
   - Volver a pestaña "Aufgaben"
   - Clic en "🎨 Diagramm generieren"
   - El diagrama aparece en el área derecha

4. **Ajustar Visualización**
   - Usar controles de zoom H/V
   - Cambiar Bundesland en dropdown
   - Hacer scroll para navegar

5. **Guardar/Cargar**
   - "💾 JSON speichern" → descargar configuración
   - "📁 JSON laden" → cargar configuración previa

## 📁 Formato JSON

Ejemplo de archivo JSON exportado:

```json
{
  "title": "Mein Projekt",
  "defaultState": "BB",
  "showTextOnBars": true,
  "tasks": [
    {
      "type": "task",
      "group": "Phase 1",
      "name": "Planung",
      "start": "2025-11-01",
      "end": "2025-11-15",
      "duration": "10 AT",
      "tonnage": "500",
      "text": "Initialplanung"
    },
    {
      "type": "milestone",
      "group": "Phase 1",
      "name": "Kick-off",
      "start": "2025-11-01",
      "end": "2025-11-01",
      "duration": "",
      "tonnage": "",
      "text": ""
    }
  ]
}
```

## 🎨 Controles del Diagrama

### Zoom
- **H +/-**: Aumentar/reducir ancho horizontal (timeline)
- **V +/-**: Aumentar/reducir altura vertical (barras)
- **⟲**: Reset a 100%

### Navegación
- **Scroll horizontal**: Navegar cuando zoom H > 100%
- **Scroll vertical**: Ver más tareas
- **Range slider**: Ajustar ventana temporal

### Interacción Plotly
- **Hover**: Ver detalles de tarea
- **Click leyenda**: Mostrar/ocultar grupos
- **Doble click**: Reset zoom de Plotly
- **Box select**: Seleccionar área

## 🔧 Personalización

### Colores
Edita la función `generateColors()` en el JavaScript:
```javascript
const colors = [
  '#3b82f6',  // Azul
  '#10b981',  // Verde
  '#f59e0b',  // Amarillo
  // ... añadir más
];
```

### Altura de barras
Ajusta el cálculo en `generateChart()`:
```javascript
height: Math.max(500, tasks.length * 30)  // 30px por tarea
```

### Bundesländer
Los estados alemanes están hardcodeados. Para cambiar, edita los `<select>` en el HTML.

## 🆚 Diferencias con la versión Python

| Característica | Python | HTML Standalone |
|---|---|---|
| **Cálculo Arbeitstage** | ✅ Sí (holidays lib) | ❌ No |
| **Feiertage por Bundesland** | ✅ Sí | ❌ No |
| **Editor visual** | ❌ No | ✅ Sí |
| **Interfaz web** | ❌ CLI | ✅ GUI |
| **Dependencias** | 🐍 Python + libs | 🌐 Solo navegador |
| **Persistencia** | 📝 Python scripts | 💾 JSON files |
| **Portabilidad** | ⚙️ Necesita Python | 🚀 100% portable |

## ⚠️ Limitaciones

1. **No calcula Arbeitstage reales** (no tiene librería holidays)
   - Las fechas son calendario, no laborables
   - El campo "duration" es solo informativo

2. **No genera sombreado de fines de semana**
   - La versión Python sí lo hace

3. **No muestra festivos**
   - La versión Python marca los festivos del Bundesland

4. **Almacenamiento local**
   - No hay base de datos, solo archivos JSON

## 💡 Casos de Uso Ideales

✅ **Ideal para:**
- Planificación rápida sin instalaciones
- Presentaciones y demos
- Compartir con usuarios sin Python
- Edición visual de proyectos
- Prototipado rápido

❌ **No ideal para:**
- Cálculos precisos de días laborables
- Integración con sistemas de festivos
- Automatización con scripts
- Procesamiento de datos complejos

## 🔮 Futuras Mejoras

Ideas para extender el editor:

- [ ] Integrar API de festivos (holiday API)
- [ ] Dependencias entre tareas
- [ ] Recursos asignados
- [ ] Gantt de recursos
- [ ] Exportar a PDF/imagen
- [ ] Plantillas de proyectos
- [ ] Modo colaborativo (con backend)
- [ ] Cálculo de ruta crítica
- [ ] Integración con calendarios

## 📞 Soporte

Este es un proyecto standalone. Para la versión completa con cálculo de Arbeitstage, usa la versión Python principal del proyecto.

## 📄 Licencia

Mismo que el proyecto principal Gantt-Diagramm.
