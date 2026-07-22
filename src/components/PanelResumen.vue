<script setup>
const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
  cantidad: {
    type: Number,
    required: true,
  },
  porCategoria: {
    type: Array,
    required: true,
    // Array de { nombre, emoji, monto, porcentaje }
  },
})
</script>

<template>
  <div>
    <h2>Resumen</h2>
    <p>Total gastado</p>
    <p class="total-big">
      ${{ props.total.toLocaleString('es-CL') }}
    </p>
    <p>
      {{ props.cantidad }} gasto<span v-if="props.cantidad !== 1">s</span>
    </p>

    <hr />

    <div v-for="cat in props.porCategoria" :key="cat.nombre" class="barra-row">
      <div class="lbl">
        <span>{{ cat.emoji }} {{ cat.nombre }}</span>
        <span>
          ${{ cat.monto.toLocaleString('es-CL') }}
          · {{ cat.porcentaje }}%
        </span>
      </div>
      <div class="barra">
        <div
          class="fill"
          :style="{ width: cat.porcentaje + '%' }"
        ></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>