# CLAUDE.md — HR Planner 2026

Contexto para Claude Code. Lee esto antes de tocar cualquier archivo.

---

## Qué es este proyecto

App de gestión de ausencias de RRHH para un equipo de ~15 personas. Un solo archivo HTML standalone (`hr_planner_2026.html`) sin dependencias externas excepto Google Fonts. Todo el estado vive en `localStorage`.

**Owner:** Rodrigo Infante — Daily Duty Institute  
**Stack:** HTML5 + CSS3 + Vanilla JS (ES6+)  
**Paleta de marca DDI:** Teal `#00e6c7`, Gold `#FFB800`, Dark Navy `#0d1117`

---

## Arquitectura del archivo

```
hr_planner_2026.html
├── <style>           → CSS variables + todos los estilos
├── Topbar            → navegación entre las 4 vistas
├── #view-gantt       → Gantt mensual interactivo
├── #view-registro    → tabla de todos los registros con filtros
├── #view-nuevo       → formulario de nueva ausencia
├── #view-config      → gestión de colaboradores y configuración
└── <script>
    ├── getData/saveData         → lectura/escritura localStorage
    ├── getCollabs/saveCollabs   → gestión de colaboradores
    ├── getLimite/saveLimite     → límite de simultáneos
    ├── workdays(start, end)     → calcula días hábiles L-V
    ├── showView(v)              → switch entre vistas
    ├── guardarRegistro()        → valida y persiste nueva ausencia
    ├── renderGantt()            → construye la tabla Gantt completa
    ├── renderRegistros()        → tabla de registros con filtros
    └── renderConfig()           → gestión de equipo
```

---

## localStorage keys

| Key | Contenido |
|-----|-----------|
| `hrplanner_registros` | Array de objetos `{id, colaborador, tipo, inicio, fin, estado, aprobador, notas, dias}` |
| `hrplanner_collabs` | Array de strings con nombres de colaboradores |
| `hrplanner_limite` | Integer — máximo de personas off simultáneamente |

**Formato de fechas:** siempre `YYYY-MM-DD` (string ISO). Comparaciones de rango son string-safe.

---

## Estructura de un registro

```js
{
  id: 1234567890,          // Date.now() — único
  colaborador: "Ana García",
  tipo: "Vacaciones",
  inicio: "2026-06-15",   // YYYY-MM-DD
  fin: "2026-06-19",
  estado: "Aprobado",     // "Aprobado" | "Pendiente" | "Rechazado"
  aprobador: "Karen",
  notas: "—",
  dias: 5                  // días hábiles calculados con workdays()
}
```

---

## Tipos de ausencia (ordenados por frecuencia)

```
Vacaciones, Incapacidad, Calamidad doméstica, Cita médica,
Día compensatorio, Permiso no remunerado, Duelo,
Capacitación externa, Licencia maternidad/paternidad,
Licencia matrimonio, Ausencia injustificada
```

---

## Lógica del Gantt

- `renderGantt()` construye una `<table>` HTML dinámica
- **Columna sticky izquierda:** nombre del colaborador
- **Columnas de días:** 1 por cada día del mes en curso
- **Weekends (sáb/dom):** columnas vacías con fondo ligeramente diferente
- **Celda con evento:** bloque coloreado según estado + tooltip al hover
- **Fila "Simultáneos":** cuenta ausencias activas por día (estado ≠ Rechazado)
- **Fila "Límite":** muestra ● rojo si el conteo supera `getLimite()`
- El mes actual se inicializa con `new Date()` y se navega con `changeMonth(±1)`

---

## CSS variables principales

```css
--teal: #00e6c7        /* acento principal */
--gold: #FFB800        /* acento secundario */
--navy: #0d1117        /* fondo base */
--navy2: #161b22       /* superficies */
--navy3: #21262d       /* hover states */
--navy4: #30363d       /* bordes */
--text: #e6edf3        /* texto principal */
--text2: #8b949e       /* texto secundario */
--red: #f85149         /* error / rechazado */
--green: #3fb950       /* success / aprobado */
--amber: #d29922       /* warning / pendiente */
```

---

## Convenciones de código

- **Funciones:** camelCase, verbos en español (`guardarRegistro`, `renderGantt`)
- **IDs de HTML:** kebab-case con prefijo de vista (`f-colaborador`, `view-gantt`)
- **Sin clases JS externas** — todo vanilla, sin jQuery, sin frameworks
- **Sin comentarios en el código** — el código debe ser autoexplicativo
- **Tutear siempre** en textos de UI — nunca "usted"

---

## Qué NO hacer

- No agregar dependencias npm o bundlers — debe seguir siendo un solo HTML
- No cambiar la paleta de colores sin consultar (es marca DDI)
- No usar `alert()` — ya existe el sistema de `toast(msg, error)`
- No romper la compatibilidad con Chrome/Edge/Firefox actuales
- No usar frameworks CSS (Bootstrap, Tailwind) — CSS custom properties propio

---

## Tareas pendientes conocidas (para Claude Code)

- [ ] Exportar registros a CSV
- [ ] Filtro por colaborador en el Gantt
- [ ] Vista anual (12 meses en una sola pantalla, resumen)
- [ ] Soporte festivos Colombia (hardcoded o configurable)
- [ ] Editar un registro existente (actualmente solo se puede borrar)
- [ ] Validación de solapamiento: alertar si el mismo colaborador ya tiene ausencia en esas fechas
- [ ] Contador de días hábiles disponibles por colaborador (según política de vacaciones)
