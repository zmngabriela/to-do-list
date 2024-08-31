<script setup>
    const props = defineProps(['tasks']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="task in props.tasks" :key="task.title">
            <input @change="e => task.concluded = e.target.checked" :checked="task.concluded" :id="task.title" type="checkbox">
            <label :class="{ done: task.concluded }" class="ms-3" :for="task.title">
                {{ task.title }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>