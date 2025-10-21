# 🎯 Comparación: Versión Python vs HTML Editor

## 📁 Estructura del Proyecto

```
Gantt-Diagramm/
├── gantt/                    # 🐍 Versión Python (original)
│   ├── __init__.py
│   ├── models.py
│   ├── work_calendar.py      # Cálculo Arbeitstage + Festivos
│   ├── data_prep.py
│   ├── figure_builder.py
│   ├── html_exporter.py
│   ├── project_config.py     # Configuración hardcoded
│   └── example_project.py
├── vorlage.py                # CLI principal
└── gantt-editor/             # 🌐 Versión HTML Standalone (nueva)
    ├── gantt-editor.html     # TODO-EN-UNO: Editor + Viewer
    ├── ejemplo-batteriepark.json
    └── README.md
```

## 🔄 Casos de Uso

### Usa la **Versión Python** cuando:
✅ Necesitas **cálculos precisos de Arbeitstage**  
✅ Debes considerar **festivos por Bundesland** (holidays)  
✅ Quieres **automatizar** generación de múltiples diagramas  
✅ Tienes datos en **archivos Python/scripts**  
✅ Necesitas **integración con otros sistemas Python**  
✅ Quieres **sombreado de fines de semana**  
✅ Trabajas con **grandes volúmenes de datos**  

### Usa la **Versión HTML** cuando:
✅ Necesitas **editar visualmente** el proyecto  
✅ Quieres **compartir con usuarios no técnicos**  
✅ No tienes Python instalado (solo navegador)  
✅ Necesitas **portabilidad total** (un solo archivo)  
✅ Quieres **edición rápida** sin código  
✅ Prefieres **interfaz gráfica** sobre CLI  
✅ Necesitas **presentar en vivo** y ajustar sobre la marcha  

## 📊 Comparativa Detallada

| Aspecto | Python | HTML Editor |
|---------|--------|-------------|
| **Instalación** | 🐍 Python + venv + deps | 🌐 Solo navegador |
| **Portabilidad** | ⚙️ Necesita entorno | ✈️ 100% portable |
| **Interfaz** | 💻 CLI (terminal) | 🎨 GUI (visual) |
| **Edición** | ✏️ Código Python | 🖱️ Formularios web |
| **Arbeitstage** | ✅ Cálculo real | ❌ Solo informativo |
| **Festivos** | ✅ Por Bundesland | ❌ No incluido |
| **Fines de semana** | ✅ Sombreado | ❌ Sin sombreado |
| **Almacenamiento** | 📝 .py files | 💾 .json files |
| **Automatización** | ✅ Scripts/CI/CD | ❌ Manual |
| **Curva aprendizaje** | 📚 Media (Python) | 🎈 Baja (intuitive) |
| **Colaboración** | 📂 Git | 💾 Compartir JSON |
| **Visualización** | 📈 Plotly + HTML | 📈 Plotly en vivo |
| **Zoom H/V** | ✅ Sí | ✅ Sí |
| **Exportar** | 📄 HTML | 💾 JSON |

## 🔀 Workflow Híbrido (Recomendado)

### Escenario: Proyecto Real

**1. Planificación inicial (HTML)**
```
→ Abrir gantt-editor.html
→ Crear estructura de tareas visualmente
→ Ajustar fechas, grupos, duraciones
→ Guardar como proyecto-draft.json
```

**2. Cálculos precisos (Python)**
```bash
# Convertir JSON a Python config
# (opcional: crear script de conversión)
python vorlage.py --state BB --output gantt-final.html
```

**3. Presentación/Ajustes (HTML)**
```
→ Cargar proyecto-draft.json en editor
→ Hacer ajustes en vivo durante reunión
→ Guardar versión actualizada
```

**4. Producción final (Python)**
```bash
# Generar con cálculos reales de Arbeitstage
python vorlage.py --state BB
```

## 🛠️ Conversión entre Formatos

### JSON (HTML) → Python Config

Ejemplo de script de conversión:

```python
import json
from datetime import datetime

# Cargar JSON del editor
with open('gantt-editor/proyecto.json') as f:
    data = json.load(f)

# Convertir a formato Python
tasks = []
for task in data['tasks']:
    if task['type'] == 'task':
        tasks.append({
            'group': task['group'],
            'task': task['name'],
            'start': task['start'],
            'end': task['end'],
            'duration': task.get('duration', ''),
            'tonnage': int(task['tonnage']) if task.get('tonnage') else None,
            'text': task.get('text', '')
        })

# Escribir a project_config.py
# (código para generar RAW_TASKS)
```

### Python Config → JSON (HTML)

```python
from gantt.project_config import RAW_TASKS, PROJECT_TITLE, DEFAULT_STATE
import json

# Convertir a formato JSON del editor
editor_format = {
    'title': PROJECT_TITLE,
    'defaultState': DEFAULT_STATE,
    'showTextOnBars': True,
    'tasks': []
}

for task in RAW_TASKS:
    editor_format['tasks'].append({
        'type': 'milestone' if task.get('is_milestone') else 'task',
        'group': task['group'],
        'name': task['task'],
        'start': task['start'],
        'end': task['end'],
        'duration': task.get('duration', ''),
        'tonnage': str(task.get('tonnage', '')),
        'text': task.get('text', '')
    })

# Guardar JSON
with open('gantt-editor/proyecto.json', 'w') as f:
    json.dump(editor_format, f, indent=2)
```

## 🎯 Mejores Prácticas

### Para Equipos

1. **Diseñador/PM** → Usa HTML Editor para crear estructura
2. **Ingeniero** → Valida fechas y cálculos con versión Python
3. **Cliente** → Ve HTML Editor para feedback visual
4. **Producción** → Usa Python para reportes finales

### Para Individual

- **Prototipado rápido**: HTML Editor
- **Análisis de viabilidad**: Python (Arbeitstage reales)
- **Presentaciones**: HTML Editor (ajustes en vivo)
- **Documentación final**: Python (precisión)

## 🚀 Próximos Pasos

### Posibles Mejoras al HTML Editor

1. **Integrar API de festivos**
   ```javascript
   // Usar API pública de festivos alemanes
   fetch('https://feiertage-api.de/api/?jahr=2025&nur_land=BB')
   ```

2. **Importar desde Python**
   ```html
   <input type="file" accept=".py"> <!-- Parser de Python -->
   ```

3. **Cálculo aproximado de Arbeitstage**
   ```javascript
   // Sin festivos, pero con fines de semana
   function calculateWorkDays(start, end) {
     let days = 0;
     let current = new Date(start);
     while (current <= end) {
       if (current.getDay() !== 0 && current.getDay() !== 6) {
         days++;
       }
       current.setDate(current.getDate() + 1);
     }
     return days;
   }
   ```

4. **Dependencias entre tareas**
   ```json
   {
     "task": "Montage",
     "depends_on": ["Fundamente", "Verkabelung"]
   }
   ```

### Scripts de Conversión Automática

Crear en `gantt-editor/`:

- `json_to_python.py` - Convierte JSON → project_config.py
- `python_to_json.py` - Convierte project_config.py → JSON
- `validate.py` - Valida fechas y dependencias

## 💡 Tips de Uso

### HTML Editor

```
Atajos útiles:
- Click en tarea → Editar
- + Aufgabe → Nueva tarea rápida
- Ctrl+S en modal → Guardar (si implementas)
- Generar después de cada cambio → Ver resultado inmediato
```

### Python CLI

```bash
# Ver ayuda completa
python vorlage.py --help

# Diferentes estados
python vorlage.py --state BY  # Bayern
python vorlage.py --state BE  # Berlin

# Sin abrir navegador
python vorlage.py --no-open

# Salida personalizada
python vorlage.py --output mi-proyecto.html
```

## 📝 Notas Finales

- **HTML Editor** es ideal para **planificación y colaboración**
- **Python** es ideal para **producción y precisión**
- Ambas versiones son **complementarias**, no excluyentes
- El formato JSON facilita **intercambio entre versiones**

---

**Recomendación**: Usa ambas herramientas según la fase del proyecto. Empieza con el editor visual para diseño rápido, y finaliza con Python para cálculos precisos.
