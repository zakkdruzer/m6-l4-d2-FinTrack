<script setup>
// 🔨 [B · Req 3] Reciban el gasto por prop, con validación (type Object, required).
// 🔨 [B · Req 5] Declaren los eventos 'eliminar' y 'ajustar' (defineEmits).
//               El hijo NO borra ni cambia el monto: SOLO emite (con el id).

// Mapa de emojis por categoría (dato acordado, úsenlo):
const emojis = { Comida:'🍔', Transporte:'🚗', 'Súper':'🛒', Ocio:'🎬', Otros:'📦' }
</script>

<template>
  <!-- 🔨 [B] Una fila con: emoji de la categoría (emojis[gasto.categoria]),
       descripción, monto formateado, y botones  −  +  ✕  que emitan
       ajustar(id,-500) / ajustar(id,500) / eliminar(id).
       Clases disponibles: .gasto-item, .emoji, .desc, .monto, .mini, .mini.del -->
</template>

<style scoped>
</style>