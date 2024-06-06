<script setup>
import { reactive, computed } from 'vue';
import Alerta from './Alerta.vue';


const alerta = reactive({
    error: false,
    mensaje: ""
})

const emit = defineEmits(['update:nombre', 'update:email', 'update:telefono', 'update:clase', 'update:fecha', 'update:sintomas', 'agendar-turno'])

const props = defineProps({
    id: {
        type: [String, null], //puede ser string o null
        required: true
    },
    nombre: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true
    },
    telefono: {
        type: Number,
        required: true
    },
    clase: {
        type: Number,
        required: true
    },
    fecha: {
        type: Date,
        required: true
    },
    sintomas: {
        type: String,
        required: true
    }
})


const validarTurno = () => {
    if (Object.values(props).includes("")) {
        alerta.error = true,
            alerta.mensaje = "Por favor, llene todos los campos"
        setTimeout(() => {
            alerta.mensaje = ""
        }, 2000);
        return
    }
    emit('agendar-turno');
    alerta.error = false,
        alerta.mensaje = "Turno agendado correctamente"
}


const editando = computed(() => {
    return props.id
})


</script>

<template>
    <div class="w-1/2 items-center text-center">
        <div class="w-full max-w-[450px] bg-white rounded-lg p-6 shadow-2xl">
            <h2 class="text-2xl font-bold text-gray-800 mb-4">Agendar turno</h2>
            <form class="flex flex-col" @submit.prevent="validarTurno">
                <input type="text" id="nombre" :value="nombre"
                    class="bg-gray-100 text-gray-800 border-0 rounded-md p-2 mb-4 focus:bg-gray-200 focus:outline-none focus:ring-1 focus:ring-blue-500 transition ease-in-out duration-150"
                    placeholder="Nombre completo" @input="$emit('update:nombre', $event.target.value)" />
                <input type="email" :value="email"
                    class="bg-gray-100 text-gray-800 border-0 rounded-md p-2 mb-4 focus:bg-gray-200 focus:outline-none focus:ring-1 focus:ring-blue-500 transition ease-in-out duration-150"
                    placeholder="Email" @input="$emit('update:email', $event.target.value)" />
                <input type="number" :value="telefono"
                    class="bg-gray-100 text-gray-800 border-0 rounded-md p-2 mb-4 focus:bg-gray-200 focus:outline-none focus:ring-1 focus:ring-blue-500 transition ease-in-out duration-150"
                    placeholder="Telefono" @input="$emit('update:telefono', parseInt($event.target.value))" />

                <input type="number" :value="clase"
                    class="bg-gray-100 text-gray-800 border-0 rounded-md p-2 mb-4 focus:bg-gray-200 focus:outline-none focus:ring-1 focus:ring-blue-500 transition ease-in-out duration-150"
                    placeholder="Año de nacimiento" @input="$emit('update:clase', parseInt($event.target.value))" />
                <input type="date" :value="fecha"
                    class="bg-gray-100 text-gray-800 border-0 rounded-md p-2 mb-4 focus:bg-gray-200 focus:outline-none focus:ring-1 focus:ring-blue-500 transition ease-in-out duration-150"
                    placeholder="fecha de agenda" @input="$emit('update:fecha', $event.target.value)" />
                <textarea name="message" :value="sintomas"
                    class="bg-gray-100 text-gray-800 border-0 rounded-md p-2 mb-4 focus:bg-gray-200 focus:outline-none focus:ring-1 focus:ring-blue-500 transition ease-in-out duration-150"
                    placeholder="Sintomas" @input="$emit('update:sintomas', $event.target.value)"></textarea>
                <input type="submit" :value="[editando ? 'Guardar cambios' : 'Agendar Turno']"
                    class="bg-gradient-to-r from-indigo-500 to-blue-500 text-white font-bold py-2 px-4 rounded-md mt-4 hover:bg-indigo-600 hover:to-blue-600 transition ease-in-out duration-150" />
                <Alerta v-if="alerta.mensaje" :alerta="alerta" />
            </form>
        </div>
    </div>
</template>
