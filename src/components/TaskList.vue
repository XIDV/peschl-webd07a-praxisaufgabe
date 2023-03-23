//  TaskList.vue ::: Komponente definiert eine Aufgabenliste.

<script>

    //  Import der Komponenten 'TaskListItem' und 'DelBu'
    import TaskListItem from './TaskListItem.vue';
    import DelBu from './DelBu.vue';

    export default({
        name: 'TaskList',

        //  Registrierung der Komponenten
        components: {TaskListItem, DelBu},

        //  Registrierung der Emits
        emits: ['delTaskEvent', 'taskStatusToggleEvent'],

        //  Registrierung der Props
        props: {
            subTasksList: Array,
        },

        data() {
            return {
                listName: this.subTasksList[0].list,
            }
        },

        //  Definition der Computed-Properties        
        computed: {
            //  Liefere die Anzahl ausstehender Aufgaben der entspr. 'subTaskList'
            subTasksPending() {
                return this.subTasksList.filter(task => !task.done).length;
            },
        },
    });
</script>


<template>
    <div class="taskList">
        <header class="tlh">
            <h3>{{ listName }}</h3>
            <div class="pendingTasksInfo">
                <p v-if="subTasksPending > 0">{{ subTasksPending }}</p>
                <img v-else src="./../assets/check-circle.svg">
            </div>
            <DelBu title="Liste löschen" @click="$parent.$emit('delListEvent', this.listName);"/>
        </header>
        <div class="tasks">
            <TaskListItem v-for="task in this.subTasksList" :task="task" />
        </div>
    </div>
</template>


<style>
    .taskList {
        position: relative;
        width: clamp(10rem, 100%, 30rem);
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
        border: solid .175rem;
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