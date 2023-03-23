//  TaskListItem.vue ::: Komponente definiert ein einzelnes Aufgabenelement

<script>

    //  Import der Komponenten 'DelBu' und 'ExpandBu'
    import DelBu from './DelBu.vue';
    import ExpandBu from './ExpandBu.vue';

    export default({
        name: 'TaskListItem',

        //  Registrierung der Komponenten
        components: {DelBu, ExpandBu},

        //  Registrierung der Props
        props: {
            task: Object,
        },
        
        data() {
            return {
                detailsHidden: true,
            }
        },

        //  Definition der Methoden
        methods: {
            //  Invertiere den Wert von 'detailsHidden'
            toggleDetails() {
                this.detailsHidden = !this.detailsHidden;
            },
        },

        //  Definition der Computed-Properties
        computed: {
            //  Wandle Stat- und Enddatum f. die Anzeige in das Format dd.mm.yyyy um
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
            <div class="taskTitle" title="Status ändern" 
            @click="$parent.$emit('taskStatusToggleEvent', this.task)">
                {{ this.task.title }}
            </div>
            <div class="btnWrapper">
                <ExpandBu title="Details anzeigen" @click="toggleDetails" />
                <DelBu title="Aufgabe löschen" @click="$parent.$emit('delTaskEvent', this.task)"/>
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
        padding: 0 1rem;
        border: solid thin;
        margin: .5rem;
        overflow: hidden;
    }
    .taskDone {
        background-color: var(--black50);
    }
    .taskDone .taskTitle,
    .taskDone .taskTitle:hover {
        text-decoration: line-through;
    }
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0 0 .5rem 0;
    }
    .taskTitle {
        flex: 1;
        padding: 1rem 0;
        cursor: pointer;
        transition: all 250ms ease-in-out;
    }
    .taskTitle:hover {
        text-decoration: underline;
        transform: scale(105%);
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