<script setup>
import { ref, computed } from 'vue'
import FormularioGasto from './components/FormularioGasto.vue'
import ItemGasto from './components/ItemGasto.vue'
import FiltroCategoria from './components/FiltroCategoria.vue'
import PanelResumen from './components/PanelResumen.vue'

// Categorías acordadas
const CATEGORIAS = [
  { nombre: 'Comida',     emoji: '🍔' },
  { nombre: 'Transporte', emoji: '🚗' },
  { nombre: 'Súper',      emoji: '🛒' },
  { nombre: 'Ocio',       emoji: '🎬' },
  { nombre: 'Otros',      emoji: '📦' },
]

// Estado del padre
const gastos = ref([])
const filtroActivo = ref('Todas')
let ultimoId = 0

const agregarGasto = (datos) => {
  // datos viene como { descripcion, monto, categoria }
  ultimoId++
  gastos.value.push({
    id: ultimoId,
    descripcion: datos.descripcion,
    monto: datos.monto,
    categoria: datos.categoria,
  })
}

const eliminarGasto = (id) => {
  gastos.value = gastos.value.filter(g => g.id !== id)
}

const ajustarMonto = (id, delta) => {
  const gasto = gastos.value.find(g => g.id === id)
  if (!gasto) return
  const nuevoMonto = gasto.monto + delta
  gasto.monto = nuevoMonto < 0 ? 0 : nuevoMonto
}

const cambiarFiltro = (categoria) => {
  filtroActivo.value = categoria
}

const gastosVisibles = computed(() => {
  if (filtroActivo.value === 'Todas') return gastos.value
  return gastos.value.filter(g => g.categoria === filtroActivo.value)
})

const total = computed(() =>
  gastos.value.reduce((s, g) => s + g.monto, 0)
)

const porCategoria = computed(() => {
  return CATEGORIAS.map(cat => {
    const montoCat = gastos.value
      .filter(g => g.categoria === cat.nombre)
      .reduce((s, g) => s + g.monto, 0)

    const porcentaje = total.value === 0
      ? 0
      : Math.round((montoCat / total.value) * 100)

    return {
      nombre: cat.nombre,
      emoji: cat.emoji,
      monto: montoCat,
      porcentaje,
    }
  })
})

const cantidad = computed(() => gastos.value.length)
</script>

<template>
  <h1>💸 FinTrack</h1>
  <div class="finapp">
    <!-- IZQUIERDA -->
    <div class="card">
      <h2>Nuevo gasto</h2>
      <FormularioGasto
        :categorias="CATEGORIAS"
        @agregar="agregarGasto"
      />

      <FiltroCategoria
        :categorias="CATEGORIAS.map(c => c.nombre)"
        :activa="filtroActivo"
        @filtrar="cambiarFiltro"
      />

      <div>
        <template v-if="gastosVisibles.length">
          <ItemGasto
            v-for="g in gastosVisibles"
            :key="g.id"
            :gasto="g"
            @eliminar="eliminarGasto"
            @ajustar="ajustarMonto"
          />
        </template>
        <p v-else class="vacio">Sin gastos aún</p>
      </div>
    </div>

    <!-- DERECHA -->
    <div class="card">
      <PanelResumen
        :total="total"
        :cantidad="cantidad"
        :por-categoria="porCategoria"
      />
    </div>
  </div>
</template>