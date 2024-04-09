<script setup>
  defineProps({
    valeur : Number,
    unite: String,
})
</script>

<template>
  <p>{{ unite }}</p>
  <!-- <input type="number" v-model="valeur"> <br> -->
</template>

<style scoped>

</style>