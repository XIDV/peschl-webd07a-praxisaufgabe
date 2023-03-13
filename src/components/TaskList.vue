<script>
    import TaskListItem from './TaskListItem.vue';
    import DelBu from './DelBu.vue';
import { trigger } from '@vue/reactivity';

    export default({
        name: 'TaskList',
        components: {TaskListItem, DelBu},
        props: {
            subTasks: Array,
        },
        methods: {
            triggerTaskDel(task) {
                this.$emit('delTaskEvent', task);
            }
        }

        
    });
</script>



<template>
    <div class="taskList">
        <header class="tlh">
            <h3>{{ this.subTasks[0].list }}</h3>
            <div class="pendingTasksInfo"><p>{{ subTasks.length }}</p></div>
            <DelBu title="Liste löschen"/>
        </header>
        <div class="tasks">
            <TaskListItem v-for="task in this.subTasks" :task="task" @delTaskEvent="triggerTaskDel"/>
        </div>
    </div>
</template>



<style >
    .taskList {
        flex: 0 1 30rem;
        background-color: var(--listBgC);
    }

    .tlh {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 1.5rem;
    }

    .pendingTasksInfo {
        width: 3rem;
        height: 3rem;
        display: inherit;
        justify-content: center;
        align-items: center;
        text-align: center;
        border: solid thin;
        border-radius: 50%;
    }
    button {
        width: 2rem;
        height: 2rem;
        display: block;
        border: none;
        cursor: pointer;
        transition: transform 250ms ease-in-out; 
    }
    button:hover {
        transform: scale(110%);
    }
</style>