<script setup>
    const props = defineProps(['addTask', 'tempTask', 'changeFilter', 'editTempTask']);
</script>

<template>
    <form @submit.prevent="props.addTask">
        <div class="row">
            <div class="col">
                <input :value="props.tempTask" required @change="props.editTempTask" type="text"
                    placeholder="Enter here the task description" class="form-control">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Add</button>
            </div>
            <div class="col-md-2">
                <select @change="props.changeFilter" class="form-control">
                    <option value="all">All</option>
                    <option value="pending">Pending</option>
                    <option value="concluded">Concluded</option>
                </select>
            </div>
        </div>
    </form>
</template>