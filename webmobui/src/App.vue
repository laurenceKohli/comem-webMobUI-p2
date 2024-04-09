<script setup>
  import { computed, defineModel } from 'vue';
  import AppScience from './components/AppScience.vue';

  const tempSI = defineModel()
  tempSI.value = 12;

  function round(valeur){
    return Math.round(valeur*100) / 100
  }

  //besoin de cela sinon on tourne en rond quand on appel set pour une autre car Kelvin changerait donc get appelé
  const tempKelvin = computed({
    get: () => {
      return round(tempSI.value) ;
    },
    set: (value) => {
      tempSI.value = (value);
    }
  });

  // const tempCels = computed(() => {
  //   return (tempKelvin.value - 273.15).toFixed(2) ;
  // }); //affiche uniquement si Kelvin change => pas possible modif Celsius
  //toFixed retourn un String !!

  const tempCels = computed({
    get: () => {
    return round(tempSI.value - 273.15) ;
    },
    set: (value) => {
      tempSI.value = (value + 273.15);
    }
  });

  const tempFahr = computed({
    get: () => {
      return round((tempSI.value - 273.15)* 9/5 + 32) ;
    },
    set: (value) => {
      tempSI.value = ((value - 32) * 5/9 + 273.15) 
    }
  });

  console.log(tempCels.value)
</script>

<template>
  <AppScience :valeur ="tempKelvin" unite ="Kelvin"/> <br>
  <input type="number" v-model="tempKelvin">
  <input type="number" v-model="tempCels">
  <input type="number" v-model="tempFahr">
  <div v-if="tempKelvin < 0">
    <p>La température est négative</p>
  </div>
</template>

<style scoped>

</style>
