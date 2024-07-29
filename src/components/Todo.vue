<script setup>
    const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <!-- <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()" :key="tarefa.titulo"> -->
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefa.titulo">
            <!-- pra fazer checkbox selecionar quando a finalizada for true: -->
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <!-- pra fazer a classe done ser valida somente quando a tarefa e finalizada for true **o === true e opcional  -->
            <label :class="{ done: tarefa.finalizada === true }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <!-- <p v-else class="mt-5 ms-5">Voce nao tem tarefas pendentes</p> -->
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>