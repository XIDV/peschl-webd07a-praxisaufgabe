<script>
    import _ from 'lodash';
    import TaskList from './TaskList.vue';

    export default({
        name: 'Main',
        components: {TaskList},
        props: {
            newName: String,
        },
        data() {
            return {
                date: new Date(),
                allLists: [],
                newTaskData: {
                    list: '',
                    start: '',
                    end: '',
                    title: '',
                    done: false
                },
                tasks: [
                    { 
                        list: 'Demoliste',
                        start: '2023-03-30',
                        end: '2023-04-05',
                        title: 'Geschenk besorgen',
                        done: false
                    },
                    { 
                        list: 'Demoliste',
                        start: '2023-04-10',
                        end: '2023-04-29',
                        title: 'Vortrag vorbereiten',
                        done: false
                    },
                    { 
                        list: 'Demoliste2',
                        start: '2023-04-15',
                        end: '2023-05-03',
                        title: 'Einladungen versenden',
                        done: true
                    },
                    { 
                        list: 'Demoliste',
                        start: '2023-07-16',
                        end: '2023-07-25',
                        title: 'Reise buchen',
                        done: false
                    }
                ],
            }
        },
        
        watch: {
            newName(wert) {
                this.addListNames(wert);
            },
        },
        
        methods: {
            setDate() {
                this.date = new Date();
            },
            addListNames(newList) {
                this.allLists = this.lists;
                if(newList && !_.includes(this.allLists, newList)) {
                    this.allLists.push(newList);
                }
            }
        },
        
        created() {
            setInterval(this.setDate, 1000);
            this.addListNames();
        },
        
        computed: {
            lists() {
                return _.uniq(this.tasks.map(task => task.list));
            },
            subLists() {
                let subLists = [];
                this.lists.forEach((list) => {
                    subLists.push(this.tasks.filter(task => task.list === list));
                });
                return subLists;
            },
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
            <div class="few">
                <label for="taskName">Neue Aufgabe erstellen *</label>
                <input type="text" id="taskName" placeholder="z. B. Geschenk besorgen" required v-model="newTaskData.title">
            </div>
            <div class="few">
                <label for="startDate">Startdatum wählen</label>
                <input type="date" name="startDate" id="startDate" v-model="newTaskData.start">
            </div>
            <div class="few">
                <label for="endDate">Fällig am *</label>
                <input type="date" name="endDate" id="endDate" v-model="newTaskData.end">
            </div>
            <div class="few">
                <label for="listSelect">Liste wählen</label>
                <select name="listSelect" id="listSelect" v-model="newTaskData.list">
                    <!-- Todo: options dynamisch ezeugen lassen -->
                    <option v-for="list in allLists" value="list">{{ list }}</option>
                </select>
            </div>
            <button type="button" id="createNewTaskButton"><img src="./../assets/calendar-plus-regular.svg" alt="Create new task icon"></button>
        </form>

        <main>
            <h2>Ihre Listen</h2>
            <div id="listsContainer">
                <!-- Hier werden alle Listen angezeigt -->
                <TaskList v-for="list in subLists" :subTasks="list" />

            </div>
        </main>

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
        font-size: clamp(1.4rem, 3vw, 4.5rem);
        font-weight: 100;
        padding: .5rem 0;
        border-bottom: solid thin white;
    }

    h2 {
        font-size: 2.5rem;
    }

    #createNewTaskForm {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin-top: .5rem;
    }

    label {
        margin: 1rem 0 .5rem 0;
    }

    .few,
    input,
    select {
        width: 100%;
    }

    input,
    select {
        font-size: 1.2rem;
        color: white;
        background-color: var(--secondBgC);
        padding: .5rem;
        border: none;
    }

    button {
        width: 3rem;
        height: 3rem;
        align-self: center;
        background-color: var(--listBgC);
        border: none;
        margin: 1rem;
        cursor: pointer;
    }
    button img {
        width: 90%;
        pointer-events: none;
    }
    button:hover {
        box-shadow: 0 0 0 .025rem white;
    }

    @media screen and (min-width: 50em) {
        #createNewTaskForm {
            flex-direction: row;
            align-items: flex-end;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .few {
            flex: 1 0 10rem;
        }
        button {
            align-self: flex-end;
            margin: 0;
        }
    }

    #listsContainer {
        display: flex;
        gap: 1rem
    }
</style>