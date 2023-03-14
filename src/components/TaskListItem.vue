<script>
    import DelBu from './DelBu.vue';
    import ExpandBu from './ExpandBu.vue';

    export default({
        name: 'TaskListItem',
        components: {DelBu, ExpandBu},
        props: {
            task: Object,
        },
        
        data() {
            return {
                detailsHidden: true,
            }
        },

        methods: {
            toggleDetails() {
                this.detailsHidden = !this.detailsHidden;
            },
            triggerTaskDel() {
                this.$emit('delTaskEvent', this.task);
            },
            triggerToggleStatus() {
                this.$emit('taskStatusToggleEvent', this.task);
            }
        },
        computed: {
            formatedDates() {
                return {
                    start: new Date(this.task.start).toLocaleDateString(),
                    end: new Date(this.task.end).toLocaleDateString(),
                }
            }
        }
    });
</script>


<template>
    <div class="tli" :class="{'taskDone' : this.task.done}">
        <header>
            <div class="taskTitle" @click="triggerToggleStatus" title="Status ändern">{{ this.task.title }}</div>
            <div class="btnWrapper">
                <ExpandBu title="Details anzeigen" @click="toggleDetails" />
                <DelBu title="Aufgabe löschen" @click="triggerTaskDel"/>
            </div>
        </header>
        <div class="taskDetails" :class="{'hidden' : detailsHidden}">
            <div>
                <div class="detHead">Startdatum</div>
                <div>{{ formatedDates.start }}</div>
            </div>
            <div>
                <div class="detHead">Fällig am</div>
                <div>{{ formatedDates.end }}</div>
            </div>

        </div>
    </div>
</template>



<style scoped>
    .tli {
        padding: 1rem;
        border: solid thin;
        margin: .5rem;
        overflow: hidden;
    }
    .taskDone {
        background-color: var(--black50);
    }
    .taskDone .taskTitle {
        text-decoration: line-through;
    }
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0 0 .5rem 0;
    }
    .taskTitle {
        cursor: pointer;
        transition: all 250ms ease-in-out;
    }
    .taskTitle:hover {
        text-decoration: underline;
        transform: scale(110%);
    }
    .btnWrapper {
        display: inherit;
        gap: 1rem
    }
    .taskDetails {
        display: flex;
    }
    .taskDetails div {
        flex: 1;
    }
    .detHead {
        font-size: .8rem;
    }
    .hidden {
       display: none;        
    }
</style>