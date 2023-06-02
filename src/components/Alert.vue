<script setup>
    import {computed} from "vue";

   const props = defineProps({
    alert: {
        type: Object,
        required: true
    }
   })

   const isError = computed(()=>{
        return props.alert.type === "ERROR" ?'bg-green-500': 'bg-red-800';
   })
</script>


<template>
    <div 
        :class="isError"
        class="text-white text-center p-3 uppercase font-bold mb-3 rounded-md"
    >
        <p>{{ alert.message }}</p>
    </div>
</template>

