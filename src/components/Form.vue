<script setup>
    import {reactive} from 'vue';
    import Alert from "./Alert.vue";

    const alert = reactive({
        type: '',
        message: ''
    });
    
    const state = reactive({
        name: '',
        patient: '',
        email: '',
        alta: '',
        symptoms: ''
    });
    
    const validate = () =>{
        if(Object.values(state).includes('')){  
            alert.message = 'Todo los compos son obligatorios';
            alert.type = "ERROR";
            return;
        }
    }
</script>

<template>
   <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>

        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y 
            <span class="text-indigo-600 font-bold">Adminístralos</span>
        </p>

        <Alert v-if="alert.message" :alert="alert"/>

        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validate">
            <div class="mb-5">
                <label for="pet" class="block text-gray-700 uppercase font-bold">
                    Nombre Mascota:
                </label>
                <input
                    type="text"
                    id="pet"
                    class="w-full border-2 p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Nombre de la mascota"
                   v-model="state.name"
                >
            </div>
            <div class="mb-5">
                <label for="owner" class="block text-gray-700 uppercase font-bold">
                    Nombre propietario:
                </label>
                <input
                    type="text"
                    id="owner"
                    class="w-full border-2 p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Nombre del propietario"
                    v-model="state.patient"
                >
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">
                    Email:
                </label>
                <input
                    type="email"
                    id="email"
                    class="w-full border-2 p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Email del propietario"
                    v-model="state.email"
                >
            </div>
            <div class="mb-5">
                <label for="date" class="block text-gray-700 uppercase font-bold">
                    Alta:
                </label>
                <input
                    type="date"
                    id="date"
                    class="w-full border-2 p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Fecha de alta"
                    v-model="state.alta"
                >
            </div>
            <div class="mb-5">
                <label for="symptoms" class="block text-gray-700 uppercase font-bold">
                    Síntomas:
                </label>
                <textarea
                    id="symptoms" 
                    class="w-full border-2 p-2 mt-2 placeholder-gray-400 rounded-md"
                    placeholder="Describe los síntomas"
                    v-model="state.symptoms"
                />
            </div>
            <input
                type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                value="Registrar paciente"
            >
        </form>
   </div>
</template>
