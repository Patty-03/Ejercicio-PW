<script setup>
import { ref } from 'vue';
import Form from './components/Form.vue';
import Table from './components/Table.vue';
import Footer from './components/Footer.vue';

const students = ref([]);

function addStudent(newStudent) {
    if (newStudent) {
        students.value.push(newStudent);
    }
}
</script>

<template>
    <main class="container">
        <Form @add-student="addStudent"></Form>
        <Table :students-data="students"></Table>
    </main>
    <Footer></Footer>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-around;
    padding: 2rem;
}
</style>