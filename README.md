# 📅 HR Planner 2026

Herramienta de gestión de ausencias para equipos. Un solo archivo HTML — sin instalación, sin dependencias, sin backend. Ábrelo en el browser y listo.

![HR Planner Screenshot](https://img.shields.io/badge/status-activo-00e6c7?style=flat-square) ![HTML](https://img.shields.io/badge/stack-HTML%20%2B%20JS-FFB800?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-30363d?style=flat-square)

---

## ¿Qué hace?

Permite registrar y visualizar ausencias de un equipo en un **Gantt mensual interactivo**, reemplazando hojas de cálculo con fórmulas frágiles por una app ligera que funciona desde el browser.

### Funcionalidades

- **Gantt mensual** con navegación por mes, tooltip por celda, y detección de simultáneos
- **Formulario de registro** con 11 tipos de ausencia ordenados por frecuencia
- **Tabla de registros** con filtros por estado y tipo, y opción de eliminar
- **Gestión de equipo** — agrega o elimina colaboradores dinámicamente
- **Límite de simultáneos** configurable — alerta visual en rojo cuando se supera
- **Persistencia local** — los datos viven en `localStorage`, sobreviven cierres del browser
- **Sin instalación** — un solo `.html`, funciona offline

---

## Tipos de ausencia soportados

| # | Tipo |
|---|------|
| 1 | Vacaciones |
| 2 | Incapacidad |
| 3 | Calamidad doméstica |
| 4 | Cita médica |
| 5 | Día compensatorio |
| 6 | Permiso no remunerado |
| 7 | Duelo |
| 8 | Capacitación externa |
| 9 | Licencia maternidad/paternidad |
| 10 | Licencia matrimonio |
| 11 | Ausencia injustificada |

---

## Cómo usar

1. Descarga `hr_planner_2026.html`
2. Ábrelo en Chrome, Edge o Firefox
3. Ve a **Equipo** → configura tus colaboradores y el límite de simultáneos
4. Ve a **+ Ausencia** → registra eventos
5. Ve a **Gantt** → visualiza el mes actual y navega entre meses

> Los datos se guardan automáticamente en el `localStorage` del browser. No se envía nada a ningún servidor.

---

## Stack

- HTML5 + CSS3 + Vanilla JS
- Fuentes: DM Sans + DM Mono (Google Fonts)
- Sin frameworks, sin npm, sin build process

---

## Próximos pasos (roadmap)

- [ ] Exportar registros a CSV / Excel
- [ ] Vista anual consolidada
- [ ] Filtro por colaborador en el Gantt
- [ ] Soporte para festivos nacionales (Colombia)
- [ ] Modo multi-usuario con backend ligero

---

## Autor

**Rodrigo Infante** — [@RodrigoInfante48](https://github.com/RodrigoInfante48)  
Daily Duty Institute · Bogotá, Colombia

---

## Licencia

MIT — úsalo, modifícalo, distribúyelo libremente.
