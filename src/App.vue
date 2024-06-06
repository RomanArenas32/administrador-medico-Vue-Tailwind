<script setup>
import Header from './components/Header.vue';
import { uid } from 'uid';
import Formulario from './components/Formulario.vue'
import { ref, reactive, watch, onMounted } from 'vue';
import Pacientes from './components/Pacientes.vue';

const turnos = ref([]);

const paciente = reactive({
  id: null,
  nombre: "",
  email: "",
  telefono: "",
  clase: "",
  fecha: "",
  sintomas: ""
})

watch(turnos, ()=>{
  guardarEnLocalStorage();
},{
  deep: true
})

const guardarEnLocalStorage = ()=>{
  localStorage.setItem('turnos', JSON.stringify(turnos.value))
}

onMounted(() => {
  const turnosStorage = localStorage.getItem('turnos');
  if(turnosStorage){
    turnos.value = JSON.parse(turnosStorage);
  }
})

const agendarTurno = () => {

  if(paciente.id){
    const {id} = paciente;
    const i = turnos.value.findIndex((pacienteState)=> pacienteState.id === id)
    turnos.value[i] = {...paciente}
  }
  else{
    turnos.value.push({ ...paciente, id: uid() })
  }
  paciente.nombre = "",
    paciente.email = "",
    paciente.telefono = "",
    paciente.clase = "",
    paciente.fecha = "",
    paciente.sintomas = ""
}

const actualizarTurno = (id) => {
  const turnoEditar = turnos.value.filter(turno => turno.id === id)[0]
  Object.assign(paciente, turnoEditar)
}

const eliminarTurno = (id) => {
  console.log("Eliminando", id)
  turnos.value = turnos.value.filter(turno => turno.id !== id)
}
</script>

<template>

  <Header />
  <div class="flex flex-col sm:flex-row w-full items-center p-6">
    <Formulario v-model:nombre="paciente.nombre" v-model:email="paciente.email" v-model:clase="paciente.clase"
      v-model:telefono="paciente.telefono" v-model:fecha="paciente.fecha" v-model:sintomas="paciente.sintomas"
      @agendar-turno="agendarTurno" />
    <div class="w-1/2  text-center">

      <h3 class="uppercase font-bold text-lg">Turnos agendados</h3>
      <div v-if="turnos.length > 0">
        <Pacientes v-for="turno in turnos" :turno="turno" @actualizar-turno="actualizarTurno" @eliminar-turno="eliminarTurno" :id="paciente.id"/>
      </div>
      <p v-else> Aun no hay citas agendadas </p>
    </div>


  </div>

</template>