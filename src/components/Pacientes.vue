<script setup>

const emit = defineEmits(['actualizar-turno', 'eliminar-turno'])
defineProps({
    turno: {
        type: Object,
        required: true
    }
})
</script>

<template>
    <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
        <p class="font-bold mb-3 text-gray-700 uppercase">ID:
            <span class="font-normal normal-case">
                {{ turno.id }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Nombre:
            <span class="font-normal normal-case">
                {{ turno.nombre }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Fecha:
            <span class="font-normal normal-case">
                {{ turno.fecha }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Email:
            <span class="font-normal normal-case">
                {{ turno.email }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Año de Nacimiento:
            <span class="font-normal normal-case">
                {{ turno.clase }}
            </span>
        </p>
        <p class="font-bold mb-3 text-gray-700 uppercase">Síntomas:
            <span class="font-normal normal-case">
                {{ turno.sintomas }}
            </span>
        </p>
        <div class="grid md:grid-cols-2 gap-5 mt-10 ">
            <button type="button"
                class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg" @click="$emit('actualizar-turno', turno.id)">Editar</button>
            <button type="button"
                class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg" @click="$emit('eliminar-turno', turno.id)">Eliminar</button>
        </div>
    </div>
</template>