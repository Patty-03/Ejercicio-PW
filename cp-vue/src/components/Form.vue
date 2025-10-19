<script setup>
import { ref, computed, defineEmits } from 'vue';

const emit = defineEmits(['add-student']);

const name = ref('');
const lastname = ref('');
const ci = ref('');
const newI = ref(false);

const nameRegex = /^[a-zA-ZáéíóúÁÉÍÓÚñÑ\s]+$/;
const ciRegex = /^\d+$/; 

const validations = computed(() => {
    return {
        name: name.value.trim() !== '' && nameRegex.test(name.value.trim()),
        lastname: lastname.value.trim() !== '' && nameRegex.test(lastname.value.trim()),
        ci: ci.value.trim() !== '' && ciRegex.test(ci.value.trim())
    };
});

const isFormValid = computed(() => {
    return Object.values(validations.value).every(isValid => isValid);
});

function addToList() {
    if (isFormValid.value) {
        const newStudent = {
            name: name.value,
            lastname: lastname.value,
            ci: ci.value,
            newI: newI.value
        };
        
        emit('add-student', newStudent); 

        name.value = '';
        lastname.value = '';
        ci.value = '';
        newI.value = false;
        alert('Estudiante agregado correctamente');
    } else {
        alert('Existen campos inválidos');
    }
}
</script>

<template>
    <div class="form-wrapper">
        <h2>Agregar Estudiante</h2>
        <form @submit.prevent="addToList">
            <label for="name">Nombre</label>
            <input type="text" name="name" id="name" v-model="name"
                :class="{ 'is-invalid': name.length > 0 && !validations.name, 'is-valid': validations.name }">
            <p v-if="name.length > 0 && !validations.name" class="error-message">Este campo es obligatorio y solo debe contener letras</p>
            
            <label for="lastname">Apellidos</label>
            <input type="text" name="lastname" id="lastname" v-model="lastname"
                :class="{ 'is-invalid': lastname.length > 0 && !validations.lastname, 'is-valid': validations.lastname }">
            <p v-if="lastname.length > 0 && !validations.lastname" class="error-message">Este campo es obligatorio y solo debe contener letras</p>

            <label for="ci">CI</label>
            <input type="text" name="ci" id="ci" v-model="ci"
                :class="{ 'is-invalid': ci.length > 0 && !validations.ci, 'is-valid': validations.ci }">
            <p v-if="ci.length > 0 && !validations.ci" class="error-message">Este campo es obligatorio y solo debe contener números.</p>

            <label for="newI">Nuevo Ingreso<input type="checkbox" name="newI" id="newI" v-model="newI"></label>

            <button :disabled="!isFormValid" type="submit">Agregar Estudiante</button>
        </form>
    </div>
</template>

<style scoped>
.form-wrapper {
    width: 80%;
    max-width: 400px;
    margin-bottom: 2rem;
}
form {
    display: flex;
    flex-direction: column;
}
input {
    margin-bottom: 0.5rem;
    padding: 8px;
    border: 1px solid #ccc;
    transition: border-color 0.3s;
}
button {
    max-width: fit-content;
    padding: 10px 15px;
    border: none;
    margin-top: 1rem;
}
button:disabled { background-color: #e0e0e0; color: #a0a0a0; cursor: not-allowed; }
button:enabled { background-color: #4CAF50; color: white; cursor: pointer; }
.is-valid { border-color: #4CAF50; box-shadow: 0 0 5px rgba(76, 175, 80, 0.5); }
.is-invalid { border-color: #f44336; }
.error-message { color: #f44336; font-size: 0.85rem; margin-top: 0; margin-bottom: 1rem; }
</style>