<script>
    export default({
        name: 'Main',
        data() {
            return {
                date: new Date(),
            }
        },
        methods: {
            setDate() {
                this.date = new Date();
            }
        },
        created() {
                setInterval(this.setDate, 1000);
        },
        computed: {
            currentDate() {
                return `${ this.date.toLocaleString('default', { weekday: 'long' }) },
                ${ this.date.getUTCDate() }.
                ${ this.date.getMonth() }.
                ${ this.date.getFullYear() }`;
                
            },
            currentTime() {
                const time = {
                    hours: this.date.getHours(),
                    minutes: this.date.getMinutes(),
                    seconds: this.date.getSeconds()
                    
                }
                for(let element in time) {
                    if(time[element] < 10) {
                        time[element] = `0${time[element]}`;
                    }
                }
                return `${time.hours}:${time.minutes}:${time.seconds}`;
            },
            
        },
    });
</script>

<template>
    <div id="mainWrapper">
        <header>
            <div id="dateContainer">{{ currentDate }}</div>
            <div id="timeContainer">{{ currentTime }}</div>
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
        flex: 1;
        padding: 0 2rem;
    }

    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 2.5rem;
        font-weight: 100;
        padding: .5rem 0;
        border-bottom: solid thin white;
    }

    h2 {
        font-size: 2.5rem;
    }
</style>