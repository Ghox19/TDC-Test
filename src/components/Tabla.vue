<script setup>
    import { ref } from 'vue';

const showFormFlag = ref(false);
const newTest = ref({ name: "q0", id: 0, result: null , editing: false, saveEnabled: false, inicio: false});
const testsClean = ref([]);
const tests = ref([]);

const showForm = () => {
  showFormFlag.value = true;
};

const addTest = () => {
  if (!newTest.value.result) {
    alert('Direccion no ingresada');
  } else {
    tests.value.push({ ...newTest.value });
    newTest.value.id = newTest.value.id + 1
    newTest.value.name = "q" + newTest.value.id;
    newTest.value.result = null;
    showFormFlag.value = false;
  }
};

const startEditing = (testid) => {
  tests.value[testid].editing = true;
};

const enableSaveButton = (testid) => {
  const item = tests.value.find((i) => i.id === testid);
  if (item) {
    item.saveEnabled = true;
  }
};

const saveResult = (testid) => {
  const item = tests.value[testid];
  item.editing = false;
  item.saveEnabled = false;
};

const deleteTest = (id) => {
  tests.value = tests.value.filter((test) => test.id !== id);
  newTest.value.id = newTest.value.id - 1
  newTest.value.name = "q" + newTest.value.id
};

const cleanData = (data) => {
  const { name, id, result, inicio } = data;
  return { name, id, result, inicio };
};

const verCleanData = () => {
  testsClean.value = tests.value.map(cleanData);
  console.log(testsClean.value)
};

const props = defineProps({
  testsClean: Array,
});
</script>

<template>
<div>
    <div class="col-md-4"></div>
    <div class="col-md-4">
      <div class="d-inline">
        <div class="d-flex align-items-center">
          <button class="btn btn-sm btn-primary" @click="showForm">Añadir columna</button>
          <div class="form-wrapper" :class="{ hidden: !showFormFlag }">
              <div class="d-flex align-items-center custom-bg">
                  <p>{{ newTest.name }}</p>
                  <input class="form-control col-7" type="text" v-model="newTest.result" @keyup.enter="addTest">
                  <button class="btn btn-sm btn-info" @click="addTest">Add</button>
              </div>
          </div>
        </div>
        <!-- Data Table -->
        <table class="table table-dark">
          <thead>
            <tr>
              <th scope="col">Inicio</th>
              <th scope="col">Estado</th>
              <th scope="col">Direccion</th>
              <th scope="col">Accion</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="test in tests" :key="test.id">
                <td>
                  <input type="checkbox" class="toggle-btn" v-model="test.inicio"/>
                </td>
                <td>{{ test.name }}</td>
                <td v-if="!test.editing">{{ test.result }}</td>
                <div v-else>
                  <input class="result form-control" style="width: 68px;" v-model="test.result" @keyup="enableSaveButton(test.id)" @keyup.enter="saveResult(test.id)" type="text"/>
                  <button :id="'save-' + test.id" @click="saveResult(test.id)" :disabled="!test.saveEnabled">Save</button>
                </div>
                <td> 
                   <button class="btn btn-sm btn-info" @click="startEditing(test.id)" :data-testid="test.id">Edit</button>
                   <div v-if="test.id === newTest.id - 1">
                      <button class="btn btn-sm btn-danger" @click="deleteTest(test.id)">Delete</button>
                   </div>
                </td>
            </tr>
          </tbody>
        </table>
        <button @click="verCleanData">Enviar</button>
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