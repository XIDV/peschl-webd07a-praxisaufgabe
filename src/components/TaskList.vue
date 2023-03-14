<script>
    import TaskListItem from './TaskListItem.vue';
    import DelBu from './DelBu.vue';

    export default({
        name: 'TaskList',
        components: {TaskListItem, DelBu},
        props: {
            subTasks: Array,
        },
        methods: {
            triggerTaskDel(task) {
                this.$emit('delTaskEvent', task);
            },
            triggerListDel() {
                this.$emit('delListEvent', this.subTasks[0].list);
                this.closeDelListDialog();
            },
            triggerToggleStatus(task) {
                this.$emit('taskStatusToggleEvent', task);
            },
            operateDelListDialog() {
                document.querySelector('#confirmDelListDialog').showModal();

            },
            closeDelListDialog() {
                document.querySelector('#confirmDelListDialog').close();
            }
        }

        
    });
</script>



<template>
    <div class="taskList">
        <dialog id="confirmDelListDialog">
            <header>
                <h3>Achtung!!!</h3>
            </header>
            <div>
                <p>Das Löschen der gesamten Liste kann <strong>nicht</strong> rückgängig gemacht werden!</p>
                <p>Es werden alle enthaltenen Aufgaben ebenfalls gelöscht!</p>
                <p>Wollen Sie die Liste <strong>"{{ this.subTasks[0].list }}"</strong> löschen?</p>
            </div>
            <div>
                <button @click="closeDelListDialog" id="cancelDel" type="button">Abbrechen!</button>
                <button @click="triggerListDel" id="deletNow" type="button">Jetzt löschen!</button>
            </div>
        </dialog>
        <header class="tlh">
            <h3>{{ this.subTasks[0].list }}</h3>
            <div class="pendingTasksInfo"><p>{{ subTasks.length }}</p></div>
            <DelBu title="Liste löschen" @click="operateDelListDialog"/>
        </header>
        <div class="tasks">
            <TaskListItem v-for="task in this.subTasks" :task="task" @delTaskEvent="triggerTaskDel" @taskStatusToggleEvent="triggerToggleStatus"/>
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
        border: solid .25rem;
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

    #confirmDelListDialog {
        color: white;
        background-color: var(--secondBgC);
    }
    #confirmDelListDialog::backdrop {
        backdrop-filter: blur(.5rem);
    }
    #confirmDelListDialog div:last-of-type {
        display: flex;
        justify-content: space-evenly;
    }
    #confirmDelListDialog h3,
    #confirmDelListDialog p:last-of-type {
        text-align: center;
    }
    
    #confirmDelListDialog button {
        width: 8rem;
        color: white;
        font-weight: bold;
    }
    #cancelDel {
        background-color: var(--black50);
    }
    #deletNow {
        background-color: var(--warnColor);
    }
</style>