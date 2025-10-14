<script setup>
    import {ref} from 'vue'

    const name = ref('')
    const lastname = ref('')
    const ci = ref('')
    const newI = ref(false)

    const students = ref([])

    function addToList(){
        students.value.push({
            name, 
            lastname,
            ci,
            newI
        })
    }

</script>

<template>
    <form>
        <label for="name">Nombre</label>
        <input type="text" name="name" id="name">

        <label for="name">Nombre</label>
        <input type="text" name="name" id="name">

        <label for="name">Nombre</label>
        <input type="text" name="name" id="name">

        <label for="name">Nombre</label>
        <input type="text" name="name" id="name">

        <button @click="addToList">Agregar Estudiante</button>
    </form>

</template>