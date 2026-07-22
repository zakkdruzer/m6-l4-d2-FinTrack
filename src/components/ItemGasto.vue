<script setup>
import { computed } from 'vue'

const props = defineProps({
  gasto: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['eliminar', 'ajustar'])

const emojis = { Comida: '🍔', Transporte: '🚗', 'Súper': '🛒', Ocio: '🎬', Otros: '📦' }

const emojiCategoria = computed(() => emojis[props.gasto.categoria] || '📦')

const formatearMonto = (m) => {
  return '$' + m.toLocaleString('es-CL')
}

const eliminar = () => {
  emit('eliminar', props.gasto.id)
}

const ajustarMenos = () => {
  emit('ajustar', props.gasto.id, -500)
}

const ajustarMas = () => {
  emit('ajustar', props.gasto.id, 500)
}
</script>

<template>
  <div class="gasto-item">
    <span class="emoji">{{ emojiCategoria }}</span>
    <span class="desc">{{ gasto.descripcion }}</span>
    <span class="monto">{{ formatearMonto(gasto.monto) }}</span>

    <button class="mini" type="button" @click="ajustarMenos">
      −
    </button>
    <button class="mini" type="button" @click="ajustarMas">
      +
    </button>
    <button class="mini del" type="button" @click="eliminar">
      ✕
    </button>
  </div>
</template>

<style scoped>
</style>