<script>

    export default({
        name: 'Main',
        data() {
            return {
                date: new Date(),
            }
        },
        
    });
</script>

<template>
    <div id="mainWrapper">
        <header>
            <div id="dateContainer">{{ date.toDateString().toLocaleString() }}</div>
            <div id="timeContainer">{{ date.getHours() }}:{{ date.getMinutes() }}</div>
        </header>

        <form action="" id="createNewTaskForm">
            <!-- Formularelemente erstellen -->
        </form>

        <div id="listsContainer">
            <h2>Ihre Listen</h2>
            <!-- Hier werden alle Listen angezeigt -->
        </div>

        <aside>
            <!-- Anzeige aller laufenden und erledigten Aufgaben -->
        </aside>
    </div>
</template>

<style scoped>
    #mainWrapper {
        /* Bereich passt sich nicht an wenn Sidbar ausgeblendet wird ... */
        padding: 0 2rem;
    }

    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 2.5rem;
        font-weight: 100;
        border-bottom: solid thin white;
    }

    h2 {
        font-size: 2.5rem;
    }
</style>