<script setup>
import { computed } from 'vue';

const props = defineProps({
    alerta: {
        type: Object,
        required: true
    }
})

const isError = computed(()=>{
    return props.alerta.error
})

</script>

<template>
    <div 
    :class="[isError ? 'bg-red-600' : 'bg-green-600']"
    class="font-bold uppercase text-center p-3 rounded-md text-white mt-2">
        {{ alerta.mensaje }}
    </div>
</template>