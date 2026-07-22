<script setup>
// 🔨 [A · Req 6] Reciban por props (con validación) lo que el padre calcula:
//    total (Number), cantidad (Number),
//    porCategoria (Array de { nombre, emoji, monto, porcentaje }).
</script>

<template>
  <!-- 🔨 [A] Muestren: un título, el total grande, la cantidad de gastos,
       y una barra por categoría (v-for sobre porCategoria) donde el ancho sea
       :style="{ width: cat.porcentaje + '%' }".
       Clases disponibles: .total-big, .barra-row, .lbl, .barra, .fill -->
</template>

<style scoped>
</style>