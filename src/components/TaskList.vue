<script>
    import TaskListItem from './TaskListItem.vue';

    export default({
        name: 'TaskList',
        components: {TaskListItem},
        props: {
            subTasks: Array,
        }

        
    });
</script>



<template>
    <div class="taskList">
        <header>
            <h3>{{ this.subTasks[0].list }}</h3>
            <div class="pendingTasksInfo"></div>
            <button type="button" class="delTaskList">del</button>
        </header>
        <div class="tasks">
            <TaskListItem v-for="task in this.subTasks" :task="task" />
        </div>
    </div>
</template>



<style scoped>
    .taskList {
        flex: 1;
        background-color: var(--listBgC);
    }

    header {
        display: flex;
        justify-content: space-between;
    }
</style>