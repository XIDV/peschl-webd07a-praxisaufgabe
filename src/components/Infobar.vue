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
        }

    });
</script>



<template>
    <div id="infobar">
        <div id="pendingList">
            <header>
                <h2>Ausstehend</h2>
            </header>
            <ul>
                <li v-for="pTask in pending">{{ pTask.title }}</li>
            </ul>
        </div>
    
    
        <div id="doneList">
            <header>
                <h2>Erledigt</h2>
            </header>
            <ul>
                <li v-for="dTask in done">{{ dTask.title }}</li>
            </ul>
        </div>
    </div>

</template>



<style scoped>
    h2 {
        font-size: 1rem;
        font-weight: 900;
        border-bottom: solid thin;
        margin-top: 2rem;
    }
    ul {
        list-style: none;
        padding: 0;
    }
    li {
        line-height: 2rem;
    }
    #doneList li {
        color: var(--black50);
    }
</style>