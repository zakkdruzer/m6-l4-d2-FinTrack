<script setup>
const props = defineProps({
  categorias: {
    type: Array,
    required: true,
  },
  activa: {
    type: String,
    required: true,
  },
})

const emit = defineEmits(['filtrar'])

const seleccionar = (categoria) => {
  emit('filtrar', categoria)
}
</script>

<template>
  <div class="filtro">
    <button
      class="chip"
      :class="{ activa: activa === 'Todas' }"
      type="button"
      @click="seleccionar('Todas')"
    >
      Todas
    </button>

    <button
      v-for="cat in categorias"
      :key="cat"
      class="chip"
      :class="{ activa: activa === cat }"
      type="button"
      @click="seleccionar(cat)"
    >
      {{ cat }}
    </button>
  </div>
</template>