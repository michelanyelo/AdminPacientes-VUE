<script setup>
import { reactive, defineProps, defineEmits } from 'vue';
import AlertaComp from './AlertaComp.vue';

const alerta = reactive({
    tipo: '',
    mensaje: ''
})

const props = defineProps({
    nombre: { type: String, required: true },
    propietario: { type: String, required: true },
    email: { type: String, required: true },
    alta: { type: String, required: true },
    sintomas: { type: String, required: true },
});

const emit = defineEmits([
    "update:nombre",
    "update:propietario",
    "update:email",
    "update:alta",
    "update:sintomas",
    "guardar-paciente"
]);

const validar = () => {
    if (Object.values(props).some(value => value === '')) {
        alerta.tipo = 'error'
        alerta.mensaje = 'Todos los campos son obligatorios'
        return
    }

    emit('guardar-paciente')
}


</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>

        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-600 font-bold">Adminístralos</span>
        </p>

        <AlertaComp v-if="alerta.mensaje" :alerta="alerta" />

        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">Nombre Mascota</label>
                <input type="text" id="mascota" placeholder="Nombre de la mascota"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" :value="props.nombre"
                    @input="emit('update:nombre', $event.target.value)">
            </div>
            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">Nombre Propietario</label>
                <input type="text" id="propietario" placeholder="Nombre del Propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" :value="props.propietario"
                    @input="emit('update:propietario', $event.target.value)">
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">Correo Propietario</label>
                <input type="email" id="email" placeholder="Correo del Propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" :value="props.email"
                    @input="emit('update:email', $event.target.value)">
            </div>
            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">Alta Mascota</label>
                <input type="date" id="alta" class="border-2 w-full p-2 mt-2 rounded-md text-gray-400"
                    :value="props.alta" @input="emit('update:alta', $event.target.value)">
            </div>
            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">Síntomas</label>
                <textarea id="sintomas" placeholder="Describe los síntomas"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40" :value="props.sintomas"
                    @input="emit('update:sintomas', $event.target.value)"></textarea>
            </div>
            <input type="submit" value="Registrar Paciente"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors">
        </form>
    </div>
</template>

<style scoped></style>
