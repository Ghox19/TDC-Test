<script setup>
    import { ref } from 'vue';

    const { tableDataIn } = defineProps(["tableDataIn"])

</script>

<template>
<div>
    <div class="col-md-4"></div>
    <div class="col-md-4">
      <div class="d-inline">
        <!-- Data Table -->
        <table class="table table-dark">
          <thead>
            <tr>
              <th scope="col">Inicio</th>
              <th scope="col">Estado</th>
              <th scope="col">Simbolo 1</th>
              <th scope="col">Simbolo 2</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="test in tableDataIn" :key="test.id">
                <td>
                  <input id="poto" type="checkbox" v-model="test.inicio" disabled>
                </td>
                <td>{{ test.name }}</td>
                <td>{{ test.result1 }}</td>	
                <td>{{ test.result2 }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>
    .hidden{
        display:none;
    }

    .d-inline p,
    .d-inline input,
    .d-inline button {
        display: inline; /* Alinear elementos en línea */
        margin-right: 20px; /* Añadir un margen derecho para separar los elementos */
    }

    .d-inline input {
      width: 20px;
    }

    .table{
      z-index: 10;
    }
</style>