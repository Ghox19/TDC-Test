<script setup>
    import { ref } from 'vue';

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
              <th scope="col">Direccion</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="test in tests" :key="test.id">
                <td>
                  <input type="checkbox" class="toggle-btn" v-model="test.inicio"/>
                </td>
                <td>{{ test.name }}</td>
                <td>{{ test.result }}</td>
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