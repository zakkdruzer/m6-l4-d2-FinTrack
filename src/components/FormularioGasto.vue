<script setup>
const props = defineProps({
  categorias: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['agregar'])

const descripcion = ref('')
const monto = ref(0)
const categoria = ref(props.categorias[0] ?? 'Comida')

const enviar = () => {
  if (!descripcion.value || !categoria.value || monto.value <= 0) return

  emit('agregar', {
    descripcion: descripcion.value,
    monto: Number(monto.value),
    categoria: categoria.value,
  })

  descripcion.value = ''
  monto.value = 0
  categoria.value = props.categorias[0] ?? 'Comida'
}
</script>

<template>
  <form class="fin-form" @submit.prevent="enviar">
    <input
      type="text"
      v-model="descripcion"
      placeholder="Descripción"
    />
    <input
      type="number"
      v-model.number="monto"
      min="0"
      placeholder="$0"
    />
    <select v-model="categoria">
      <option
        v-for="cat in props.categorias"
        :key="cat"
        :value="cat"
      >
        {{ cat }}
      </option>
    </select>
    <button class="btn" type="submit">
      +
    </button>
  </form>
</template>