<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    studentsData: {
        type: Array,
        required: true
    }
});
</script>

<template>
    <div class="table-wrapper">
        <h2>Listado de Estudiantes</h2>

        <div v-if="props.studentsData.length > 0" class="table-container">
            <table>
                <thead>
                    <tr>
                        <th>Nombre</th>
                        <th>Apellidos</th>
                        <th>CI</th>
                        <th>Nuevo Ingreso</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(student, index) in props.studentsData" :key="index">
                        <td>{{ student.name }}</td>
                        <td>{{ student.lastname }}</td>
                        <td>{{ student.ci }}</td>
                        <td>{{ student.newI ? 'Sí' : 'No' }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <p v-else class="no-data-message">
            Aún no hay estudiantes registrados.
        </p>
    </div>
</template>

<style scoped>
.table-wrapper {
    margin-top: 2rem;
    width: 80%;
    max-width: 800px;
    text-align: center;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}
th {
    background-color: #f2f2f2;
}
.no-data-message {
    color: #888;
    margin-top: 1rem;
}
</style>