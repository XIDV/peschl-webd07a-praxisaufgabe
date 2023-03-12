<script>
    
    export default({
        name: 'TaskListItem',
        props: {
            task: Object,
        }
    });
</script>


<template>
    <button class="tli">
        <div>{{ this.task.title }}</div>
    </button>
</template>



<style scoped>
    button {
        display: block;
        width: 100%;
    }
</style>