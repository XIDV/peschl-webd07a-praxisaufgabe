<script>
    import _ from 'lodash';
    import TaskList from './TaskList.vue';
    import Infobar from './Infobar.vue';

    export default({
        name: 'Main',
        components: {TaskList, Infobar},
        props: {
            newName: String,
            delListName: String,
        },
        emits: ['delListEvent'],
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
            delListName(list) {
                this.delList(list);
            }
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
            },
            addNewTask() {
                const temp = {
                    list: this.newTaskData.list,
                    start: this.newTaskData.start,
                    end: this.newTaskData.end,
                    title: this.newTaskData.title,
                    done: this.newTaskData.done
                }
                this.tasks.push(temp);
                this.addListNames();
                this.clearNewTaskForm();
                this.saveTasksToLocalStorage();
            },
            clearNewTaskForm() {
                this.newTaskData.list = '';
                this.newTaskData.start = '';
                this.newTaskData.end = '';
                this.newTaskData.title = '';
            },
            delTask(task) {
                this.tasks.splice(this.tasks.indexOf(task), 1);
                this.addListNames();
                this.saveTasksToLocalStorage();
            },

            delList(list) {
                this.tasks = _.remove(this.tasks, function(t) {
                    return t.list !== list;
                });
                this.addListNames();
                this.saveTasksToLocalStorage();
            },



            toggleTaskStatus(task) {
                this.tasks[this.tasks.indexOf(task)].done = !this.tasks[this.tasks.indexOf(task)].done;
                this.saveTasksToLocalStorage();
            },
            checkForLokalTasksData() {
                return localStorage.getItem('savedTasks');
            },
            saveTasksToLocalStorage() {
                localStorage.setItem('savedTasks', JSON.stringify(this.tasks));
            }
        },
        
        created() {
            setInterval(this.setDate, 1000);
            let localTasks = this.checkForLokalTasksData();
            if(localTasks !== null) {
                this.tasks = JSON.parse(localTasks) 
            }
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
            pendingList() {
                return this.tasks.filter(task => !task.done);
            },
            doneList() {
                return this.tasks.filter(task => task.done);
            },
            currentDate() {
                return `${ this.date.toLocaleString('default', { weekday: 'long' }) },
                ${ this.date.getUTCDate() }.
                ${ this.date.getMonth() + 1}.
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
                // return `${time.hours}:${time.minutes}:${time.seconds}`;
                return `${time.hours}:${time.minutes}`;
            },
            
        },
    });
</script>

<template>
    <div id="mainWrapper">
        <header>
            <div id="dateContainer">{{ currentDate }}</div>
            <div id="numOfPendingTasks"><p>{{ pendingList.length }}</p></div>
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
                        <option v-for="list in allLists" :value='list'>{{ list }}</option>
                    </select>
                </div>
                <button type="button" id="createNewTaskButton" @click="addNewTask"><img src="./../assets/calendar-plus-regular.svg" alt="Create new task icon"></button>
            </form>
            
        <div id="contentWrapper">
            <main>
                <h2>Ihre Listen</h2>
                <div id="listsContainer">
                    <TaskList v-for="list in subLists" :subTasksList="list" :key="list[0].list" @delTaskEvent="delTask" @taskStatusToggleEvent="toggleTaskStatus" />
                </div>
            </main>
            <aside>
                <Infobar @delTaskEvent="delTask" :doneAndPending="{done: doneList, pending: pendingList}"/>
            </aside>

        </div>
    </div>
</template>

<style scoped>
    #mainWrapper {
        flex: 1;
        padding: 0 2rem;
    }

    header {
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: clamp(1.4rem, 3vw, 4.5rem);
        font-weight: 100;
        padding: .5rem 0;
        border-bottom: solid thin white;
    }

    #contentWrapper {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
    }

    main {
        min-width: 30rem;
        flex: 1;
    }

    aside {
        width: 100%;
        border-top: solid thin;
        margin-top: 2rem;
    }

    h2 {
        font-size: 2.5rem;
    }

    #numOfPendingTasks {
        font-size: clamp(1.2rem, 4vw, 4.5rem);
        width: clamp(3rem, 5vw, 5rem);
        height: clamp(3rem, 5vw, 5rem);
        display: inherit;
        justify-content: center;
        align-items: center;
        text-align: center;
        border: solid .25rem;
        border-radius: 50%;
    }

    #createNewTaskForm {
        /* max-width: 80rem; */
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
    
    @media screen and (min-width: 64em) {
        #createNewTaskForm {
            flex-direction: row;
            justify-content: center;
            align-items: flex-end;
            flex-wrap: wrap;
            gap: 1rem;
        }
    
        .few {
            flex: 0 1 15rem;
        }
        button {
            align-self: flex-end;
            margin: 0;
        }
        aside {
            width: 20rem;
            padding-left: 2rem;
            border-top: none;
            border-left: solid thin;
            margin: 2 0 0 0;
        }
    }
    #listsContainer {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        gap: 1rem
    }
</style>