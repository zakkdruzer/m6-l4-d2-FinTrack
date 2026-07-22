# FinTrack – Control de Gastos en Equipo

Aplicación de control de gastos construida con Vue 3 y Vite, siguiendo el patrón **“datos bajan por props, avisos suben por eventos”**.  
Permite registrar gastos, verlos en una lista editable, filtrarlos por categoría y visualizar un resumen con totales y porcentajes, persistiendo los datos en `localStorage`.

## Características

- Registro de gastos con descripción, monto y categoría.
- Lista de gastos con emoji según categoría.
- Edición rápida del monto (−500 / +500) y eliminación de gastos.
- Filtro por categoría (Todas, Comida, Transporte, Súper, Ocio, Otros).
- Panel de resumen con:
  - Total gastado.
  - Cantidad de gastos.
  - Desglose por categoría con barras y porcentaje.
- Persistencia de datos en `localStorage` para mantener los gastos al recargar.
- Arquitectura basada en componentes y comunicación padre–hijo mediante props y eventos.

## Stack técnico

- Vue 3 (Composition API con `<script setup>`).
- Vite como bundler y servidor de desarrollo.
- CSS plano incluido en `src/style.css` para el layout y estilos de la app.
- `localStorage` para persistencia de gastos.
- Configuración lista para despliegue estático con Vite y visualización en GitHub Pages.

## Estructura de componentes

- `App.vue`  
  - Componente padre y dueño del estado.
  - Mantiene el array de `gastos`, el `filtroActivo` y calcula:
    - `total`
    - `cantidad`
    - `porCategoria`
    - `gastosVisibles`
  - Conecta los eventos de los hijos con los métodos:
    - `agregarGasto`
    - `eliminarGasto`
    - `ajustarMonto`
    - `cambiarFiltro`

- `components/FormularioGasto.vue`  
  - Formulario para agregar nuevos gastos.
  - Recibe `categorias` por prop.
  - Usa `v-model` para descripción, monto y categoría.
  - Emite el evento `agregar` con `{ descripcion, monto, categoria }`.

- `components/ItemGasto.vue`  
  - Representa una fila de gasto.
  - Recibe `gasto` por prop (`{ id, descripcion, monto, categoria }`).
  - Muestra emoji, descripción y monto formateado.
  - Emite:
    - `eliminar` con el `id`.
    - `ajustar` con `(id, delta)` para −500 / +500.

- `components/FiltroCategoria.vue`  
  - Renderiza los “chips” de categoría.
  - Recibe `categorias` (array de nombres) y `activa` (categoría seleccionada) por props.
  - Emite `filtrar` con la categoría elegida.
  - Marca visualmente el chip activo.

- `components/PanelResumen.vue`  
  - Muestra el panel de resumen.
  - Recibe por props:
    - `total`
    - `cantidad`
    - `porCategoria` (array de `{ nombre, emoji, monto, porcentaje }`).
  - Renderiza el total y las barras por categoría usando el porcentaje.

## Flujo de datos

- Los datos viven en `App.vue`:
  - El array `gastos` se inicializa leyendo desde `localStorage`.
  - Un `watch` sobre `gastos` guarda el estado cada vez que cambia.
- Los componentes hijos reciben la información necesaria por **props**:
  - `FormularioGasto` recibe las categorías disponibles.
  - `ItemGasto` recibe cada gasto.
  - `FiltroCategoria` recibe la lista de nombres de categoría y la categoría activa.
  - `PanelResumen` recibe totales y desglose por categoría.
- Los cambios del usuario se comunican al padre por **eventos**:
  - `FormularioGasto` emite `agregar`.
  - `ItemGasto` emite `eliminar` y `ajustar`.
  - `FiltroCategoria` emite `filtrar`.
- El padre actualiza su estado y los `computed` recalculan la vista.

## Instalación y ejecución

```bash
# Instalar dependencias
npm install

# Servidor de desarrollo
npm run dev

# Build para producción
npm run build

# Vista previa del build
npm run preview
```

## Deploy

El proyecto está preparado para despliegue como sitio estático con Vite y publicación en una rama `gh-pages`.  
Tras configurar el valor `base` en `vite.config` y los scripts de deploy en `package.json`, la app se puede visualizar en GitHub Pages ejecutando:

```bash
npm run deploy
```

## Aprendizajes clave

- Uso de `defineProps` y `defineEmits` en `<script setup>` para componentes reutilizables.
- Patrón de comunicación: **props down, events up**.
- Uso de `ref`, `computed` y `watch` para gestionar estado y efectos secundarios.
- Cálculos de totales y porcentajes con `computed` a partir de un array de gastos.
- Persistencia de estado en `localStorage` manteniendo la reactividad de Vue.
- Configuración básica de despliegue de apps Vite + Vue en GitHub Pages.

## Puedes ver el resultado en:

https://zakkdruzer.github.io/m6-l4-d2-FinTrack/
