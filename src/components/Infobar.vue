<script>

    export default({
        name: 'Infobar',
        props: {
            doneAndPending: Object,
        },
        data() {
            return {
                done: this.doneAndPending.done,
                pending: this.doneAndPending.pending,
            }
        },
        watch: {
            doneAndPending() {
                this.done = this.doneAndPending.done;
                this.pending = this.doneAndPending.pending;
            }
        },
        methods: {
            triggerDelTask(i) {
                this.$emit('delTaskEvent', this.done[i]);
            }
        },
        
    });
</script>



<template>
    <div id="infobar">
        <div id="pendingList">
            <header>
                <h2>Ausstehend</h2>
                <div>Fällig</div>
            </header>
            <ul>
                <li v-for="pTask in pending">
                    <div>{{ pTask.title }}</div>
                    <div>{{ new Date(pTask.end).toLocaleDateString() }}</div>
                </li>
            </ul>
        </div>
    
    
        <div id="doneList">
            <header>
                <h2>Erledigt</h2>
            </header>
            <ul>
                <li v-for="dTask in done">
                    <div>{{ dTask.title }}</div>
                    <button @click="triggerDelTask(done.indexOf(dTask))" type="button"><img src="./../assets/trash.svg" alt="Delet icon"></button>
                </li>
            </ul>
        </div>
    </div>

</template>



<style scoped>
    header {
        border-bottom: solid thin;
        margin-top: 2rem;
    }
    header:first-of-type {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    h2,
    header div {
        font-size: 1rem;
        font-weight: 900;
    }
    ul {
        list-style: none;
        padding: 0;
    }
    li {
        line-height: 2rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: .75rem;
    }
    #doneList li {
        color: var(--black50);
    }
    button {
        background-color: transparent;
        border: none;
    }
    button img {
        width: 1.25rem;
    }
</style>