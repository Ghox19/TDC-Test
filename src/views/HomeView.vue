<script setup>
import { ref } from 'vue';
import Tabla from '../components/Tabla.vue'
import TablaClean from '../components/TablaClean.vue'

const pepe = ref(null);
const ver = false;

const elpepe = (prop) => {
  pepe.value = prop;
  }
</script>

<template>
  <div>
    <Tabla @table-data="n => elpepe(n)"/>
  </div>
  <div>
    <TablaClean :tableDataIn= "pepe"/>
  </div>
</template>

<style scoped>
</style>