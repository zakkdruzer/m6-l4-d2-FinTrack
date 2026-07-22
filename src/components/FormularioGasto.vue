<script setup>
// 🔨 [A · Req 1] Reciban 'categorias' por prop (para el <select>).
// 🔨 [A · Req 2] Declaren el evento 'agregar' (defineEmits).
// 🔨 [A · Req 1] Estado del formulario con v-model (Lección 3): descripción, monto, categoría.
// 🔨 [A · Req 2] Al enviar: validen, emitan 'agregar' con { descripcion, monto, categoria }
//               y limpien. El hijo NO agrega a ninguna lista: solo avisa al padre.
</script>

<template>
  <!-- 🔨 [A] Un <form @submit.prevent> (Día 1) con: input de descripción,
       input numérico de monto, un <select> de categoría (v-for sobre categorias)
       y el botón Agregar. Clases disponibles: .fin-form, .btn -->
</template>

<style scoped>
</style>