<script setup>
    import { ref } from 'vue';

const showFormFlag = ref(false);
const newTest = ref({ name: "q0", id: 0, result: null , editing: false, saveEnabled: false});
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
</script>

<template>
<div>
    <div class="col-md-4"></div>
    <div class="col-md-4">
      <div class="card card-body">
        <button class="btn btn-sm btn-primary" @click="showForm">Añadir columna</button>
        <div class="form-wrapper" :class="{ hidden: !showFormFlag }">
            <div class="form-inline">
                <p>{{ newTest.name }}</p>
                <input class="form-control" type="text" v-model="newTest.result">
                <button class="btn btn-sm btn-info" @click="addTest">Add</button>
            </div>
        </div>
        <!-- Data Table -->
        <table class="table table-dark">
          <thead>
            <tr>
              <th scope="col">Estado</th>
              <th scope="col">Direccion</th>
              <th scope="col">Accion</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="test in tests" :key="test.id">
                <td>{{ test.name }}</td>
                <td v-if="!test.editing">{{ test.result }}</td>
                <div v-else>
                  <input class="result form-control" v-model="test.result" @keyup="enableSaveButton(test.id)" 
                    :data-testid="test.id" type="text"/>
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
      </div>
    </div>
    <div class="col-md-4"></div>
  </div>
</template>

<style scoped>
    .hidden{
        display:none;
    }

    .result{
    	max-width:80px; 
    }
</style>