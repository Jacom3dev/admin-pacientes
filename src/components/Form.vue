<script setup>
    import {reactive} from 'vue';
    import Alert from "./Alert.vue";

    const alert = reactive({
        type: '',
        message: ''
    });
    
    const props = defineProps({
        id: {
            type: String
        },
        patient: {
            type: String, required: true
        },
        email: {
            type: String, required: true
        },
        owner: {
            type: String, required: true
        },
        date: {
            type: String, required: true
        },
        symptoms: {
            type: String, required: true
        }
    });
    const emits = defineEmits(['update:patient','update:email','update:owner','update:date','update:symptoms','create']);
    
    const validate = () =>{
        if(Object.values(props).includes('')){  
            alert.message = 'Todo los compos son obligatorios';
            alert.type = "ERROR";
            return;
        }

        emits('create');

        alert.message = props.id?"Paciente editado": "Paciente registrado correctamente";
        alert.type = "SUCCESS";

        setTimeout(()=>{
            Object.assign(alert,
            {
                type: '',
                message: ''
            }); 
        },3000)
    }
</script>

<template>
   <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>


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
                    :value="patient"
                    @input="$emit('update:patient',$event.target.value)"
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
                    :value="owner"
                    @input="$emit('update:owner',$event.target.value)"
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
                    :value="email"
                    @input="$emit('update:email',$event.target.value)"
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
                    :value="date"
                    @input="$emit('update:date',$event.target.value)"
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
                    :value="symptoms"
                    @input="$emit('update:symptoms',$event.target.value)"
                />
            </div>
            <input
                type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                :value="id?'Actulizar':'Registrar paciente'"
            >
        </form>
   </div>
</template>
