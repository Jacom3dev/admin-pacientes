<script setup>
  import { ref, reactive,onMounted,watch } from "vue";
  import {uid} from "uid";
  import Header from "./components/Header.vue";
  import Form from "./components/Form.vue";
  import Patient from "./components/Patient.vue";

  const state = reactive({
    id: null,
    patient: "",
    owner: "",
    email: "",
    date: "",
    symptoms: "",
  });

  const patients = ref([]);

  const create = () => {

    if (state.id) {
      const {id} = state;
      const index = patients.value.findIndex((p)=>p.id === id);
      patients.value[index] = {...state};
    }else {
      patients.value.push({ ...state,id: uid() });
    }

    
    Object.assign(state, {
      patient: "",
      owner: "",
      email: "",
      date: "",
      symptoms: "",
      id:null
    });
    
  };

  const update = (id)=>{
    const patientEdit = patients.value.find(p=>p.id === id);
    
    Object.assign(state,patientEdit);
  }

  const deletePatient = (id)=>{
    patients.value = patients.value.filter(p=>p.id !== id);
  }

  const setLocalStorage = ()=>{
    localStorage.setItem('patients',JSON.stringify(patients.value));
  }

  watch(patients,()=>{
    setLocalStorage();
  },{deep:true})

  onMounted(()=>{
    const getLocalStorage = localStorage.getItem("patients");
    if (getLocalStorage) {
      patients.value = JSON.parse(getLocalStorage);
    }
  })

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-2 md:flex">
      <Form
        v-model:patient="state.patient"
        v-model:owner="state.owner"
        v-model:email="state.email"
        v-model:date="state.date"
        v-model:symptoms="state.symptoms"
        @create="create"
        :id="state.id"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">
          Administra tus pacientes
        </h3>

        <div v-if="patients.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Patient
            v-for="patient in patients"
            :patient="patient" @update="update"
            @delete-patient="deletePatient"
          />
        </div>
        <p v-else class="mt-10 text-2xl">No hay pecientes</p>
      </div>
    </div>
  </div>
</template>
