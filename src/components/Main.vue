//  Main.vue ::: Komponente definiert den pimären Anzeigebereich der Anwendung

<script>

    //  Import der node-Pakete 'lodash' und 'file-saver'
    import _ from 'lodash';
    import SaveAs from 'file-saver';

    //  Import der Komponenten 'TaskList' und 'Infobar'
    import TaskList from './TaskList.vue';
    import Infobar from './Infobar.vue';

    export default({
        name: 'Main',

        //  Registrierung der Komponenten
        components: {TaskList, Infobar},

        //  Registrierung der Emits
        emits: ['delListEvent', 'resetNewListNameEvent', 'resetDelListNameEvent', 'fileOpCompleted'],

        //  Registrierung der Props
        props: {
            newName: String,
            delListName: String,
            declaredFileOp: String,
        },
        
        //  Überwachung der Props ...
        watch: {
            newName(wert) {
                this.addListNames(wert);
            },
            delListName(list) {
                this.delList(list);
            },
            declaredFileOp(op) {
                if(op === 'import') {
                    this.importTaskData();
                } else if(op === 'export') {
                    this.expTaskData();
                    this.$emit('fileOpCompleted');
                }
            }
        },

        data() {
            return {
                date: new Date(),
                allLists: [],
                showInfo: false,
                newTaskData: {
                    list: '',
                    start: '',
                    end: '',
                    title: '',
                    done: false
                },
                inputDataOK: false,
                infoMessage: '',
                importData: '',
                tasks: [
                    { 
                        list: 'Erste Schritte',
                        start: '2023-03-30',
                        end: '2023-04-05',
                        title: 'Klick hier für Statusänderung der Aufgabe',
                        done: false
                    },
                    { 
                        list: 'Erste Schritte',
                        start: '2023-04-30',
                        end: '2023-05-05',
                        title: 'Status kann durck Klick wieder geändert werden',
                        done: true
                    },
                    { 
                        list: 'Erste Schritte',
                        start: '2023-04-10',
                        end: '2023-04-29',
                        title: 'Klick auf die Punkte ->',
                        done: false
                    },
                    { 
                        list: 'Erste Schritte',
                        start: '2023-04-15',
                        end: '2023-05-03',
                        title: 'Mülleimer löscht die Aufgabe',
                        done: false
                    },
                    { 
                        list: 'Mit Listen arbeiten',
                        start: '2023-07-16',
                        end: '2023-07-25',
                        title: 'Liste löschen mit Mülleimer im Listentitel',
                        done: false
                    },
                    { 
                        list: 'Mit Listen arbeiten',
                        start: '2023-07-17',
                        end: '2023-08-25',
                        title: 'Die Zahl zeigt die Anzahl der nicht erledigten Aufgaben',
                        done: false
                    },
                    { 
                        list: 'Mit Listen arbeiten',
                        start: '2023-07-17',
                        end: '2023-08-25',
                        title: 'Neue Listen können über die Schaltfl. in der Sidebar links angelegt werden',
                        done: false
                    },
                    { 
                        list: 'Das Interface',
                        start: '2023-07-19',
                        end: '2023-08-03',
                        title: 'Die Sidebar kann ein- und ausgeblendet werden',
                        done: false
                    },
                    { 
                        list: 'Das Interface',
                        start: '2023-06-07',
                        end: '2023-07-05',
                        title: 'Bei kleinen Bildschirmen ist sie standardmäßig ausgeblendet',
                        done: false
                    },
                    { 
                        list: 'Das Interface',
                        start: '2023-06-09',
                        end: '2023-07-02',
                        title: 'Die Statusleiste am oberen Bildschirmrand zeigt Datum, Uhrzeit und Anzahl nicht erledigter Aufgaben',
                        done: false
                    },
                    { 
                        list: 'Das Interface',
                        start: '2023-06-12',
                        end: '2023-07-01',
                        title: 'Darunter ist das Eingabeformular um neue Aufgaben zu erstellen. Validierung erfolgt bei der Eingabe',
                        done: false
                    },
                ],
            }
        },
        
        //  Definition der Methoden
        methods: {
            //  Setze die Property 'date' auf das aktuelle Datum u. Uhrzeit
            setDate() {
                this.date = new Date();
            },

            //  Füge der Property 'allLists' einen neuen Eintrag hinzu
            addListNames(newList) {
                this.allLists = this.lists;                             //  Schreibe den Inhalt d. C-Property 'liste' in 'allLists'
                if(newList && !_.includes(this.allLists, newList)) {    //  Prüfe ob der Methode ein Parameter übergeben wurde und, wenn das der Fall ist, ob sich in 'allLists' nicht bereits ein entsprechender Eintrag befindet. Wenn 'true' ...
                    this.allLists.push(newList);                        //  Füge 'allLists' den Wert von 'newList' hinzu
                }
                this.$emit('resetNewListNameEvent');                    //  Feuer einen 'resetNewListNameEvent' (s. App.vue)
            },

            //  Füge der Property 'tasks' eine weiteres Objekt hinzu
            addNewTask() {
                this.tasks.push({
                    list: this.newTaskData.list,
                    start: this.newTaskData.start,
                    end: this.newTaskData.end,
                    title: this.newTaskData.title,
                    done: this.newTaskData.done
                });
                this.addListNames();
                this.saveTasksToLocalStorage();
                this.clearNewTaskForm();
                this.inputDataOK = false;
            },

            //  Validiere aller Nutzereingaben
            validateValues() {
                Promise.all(
                    [
                        this.validateString(this.newTaskData.list),                             //  validiere Auswahl d. Liste
                        this.validateString(this.newTaskData.title),                            //  validiere Aufgabentitel
                        this.validateDateLogic(this.newTaskData.start, this.newTaskData.end)    //  validiere Logik von Start- u. Enddatum.
                    ]).then(
                    res => {
                        this.inputDataOK = true;            //  Alle eingegebenen Daten sind OK
                        this.showInfo = false;
                        this.infoMessage = '';
                    },
                    rej => {
                        this.inputDataOK = false;           //  Eine o. mehrere Eingaben sind fehlerhaft
                        this.showInfo = true;
                        this.infoMessage = rej;
                    }
                );
            },

            //  Validiere einen String
            validateString(str) {
                return new Promise((res, rej) => {
                    if(this.$parent.validString(str)) {
                        res(true);
                    } else {
                        rej('Bitte Aufgabenname und Liste prüfen.');
                    }
                });
            },

            // Validiere ob ein Enddatum vergeben wurde und ob Start- und Enddatum logisch kohärent sind
            validateDateLogic(start, end) {
                return new Promise((res, rej) => {
                    if(start === null || start < end) {
                        res(true);
                    } else {
                        rej('Das Fälligkeitsdatum ist erforderlich. Das Startdatum muss vor dem Fälligkeitsdatum liegen.');
                    }
                });
            },

            //  Setze die input- und das select-Element zurück
            clearNewTaskForm() {
                this.newTaskData.list = '';
                this.newTaskData.start = '';
                this.newTaskData.end = '';
                this.newTaskData.title = '';
            },

            //  Lösche die mittels 'task' spezifizierte Aufgabe aus 'tasks'
            delTask(task) {
                this.tasks.splice(this.tasks.indexOf(task), 1);
                this.addListNames();
                this.saveTasksToLocalStorage();
            },

            //  Lösche eine ganze Liste indem alle durch 'list' spezifizierten Aufgaben aus 'tasks' entfernt werden
            delList(list) {
                this.tasks = _.remove(this.tasks, function(t) {
                    return t.list !== list;
                });
                this.addListNames();
                this.saveTasksToLocalStorage();
                this.$emit('resetDelListNameEvent');            // Feuer einen 'resetDelListNameEvent' (s. App.vue)
            },

            //  Verändere den Status der durch 'task' spezifizierten Aufgabe
            toggleTaskStatus(task) {
                this.tasks[this.tasks.indexOf(task)].done = !this.tasks[this.tasks.indexOf(task)].done;
                this.saveTasksToLocalStorage();
            },

            //  Prüfe ob im localStorage des Browsers ein Element 'savedTasks' existiert und gebe es zurück
            checkForLokalTasksData() {
                return localStorage.getItem('savedTasks');
            },

            //  Speicher den Inhalt von 'tasks' unter der Bezeichnung 'savedTasks' im localStorage des Browsers
            saveTasksToLocalStorage() {
                localStorage.setItem('savedTasks', JSON.stringify(this.tasks));
            },

            //  Öffne einen 'Datei öffnen'-Dialog
            importTaskData() {
                document.querySelector('#fileSelect').click();
                this.$emit('fileOpCompleted');
            },

            //  Importiere Aufgaben aus Datei
            handleImportData(e) {
                const file = e.target.files[0];
                const fileReader = new FileReader();
                if(file.type.match('application.json')) {
                    fileReader.addEventListener('load', event => {
                        if(confirm('Bestehende Aufgaben werden durch den Import Überschrieben. Dieser Vorgang kann nicht wiederrufen werden!')) {
                            this.tasks = JSON.parse(fileReader.result);
                            this.saveTasksToLocalStorage();
                        }
                    });
                    fileReader.readAsText(file);
                } else {
                    alert('Dateityp ist nicht zulässig. JSON erforderlich.');
                }
                e.target.value = '';
            },

            //  Speicher die Aufgaben in einer Datei
            expTaskData() {
                let dataExport = new Blob([this.checkForLokalTasksData()], { type: 'text/plain;charset=utf-8' });
                SaveAs.saveAs(dataExport, `DoIt-backup.json`);
            },
        },
        
        //  Ausführen beim rendern der Komponente
        created() {
            setInterval(this.setDate, 1000);                        //  Rufe jede Sekunde die Methode 'setDate()' auf
            let localTasks = this.checkForLokalTasksData();
            if(localTasks !== null) {
                this.tasks = JSON.parse(localTasks) 
            }
            this.addListNames();
        },

        //  Definition der Computed-Properties
        computed: {
            //  Generiere eine Liste aller Listennamen
            lists() {
                return _.uniq(this.tasks.map(task => task.list));
            },

            //  Generiere Listen anhand der Listenzugehörigkeit der spezifischen Aufgaben
            subLists() {
                let subLists = [];
                this.lists.forEach((list) => {
                    subLists.push(this.tasks.filter(task => task.list === list));
                });
                return subLists;
            },

            //  Generiere eine Liste der ausstehenden Aufgaben
            pendingList() {
                return this.tasks.filter(task => !task.done);
            },

            //  Generiere eine Liste der erledigten Aufgaben
            doneList() {
                return this.tasks.filter(task => task.done);
            },

            //  Gebe das aktuelle Datum als custom-String zurück
            currentDate() {
                return `${ this.date.toLocaleString('default', { weekday: 'long' }) },
                ${ this.date.getUTCDate() }.
                ${ this.date.getMonth() + 1}.
                ${ this.date.getFullYear() }`;
                
            },

            //  Gebe die Uhrzeit als custom-String zurück
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
        <div>
            <input type="file" name="fileSelect" id="fileSelect" style="display: none" @change="handleImportData">
        </div>

        <header>
            <div id="dateContainer">{{ currentDate }}</div>
            <div id="numOfPendingTasks"><p>{{ pendingList.length }}</p></div>
            <div id="timeContainer">{{ currentTime }}</div>
        </header>

        <form action="" id="createNewTaskForm" @change="validateValues">
            <div class="few">
                <label for="taskName">Neue Aufgabe erstellen *</label>
                <input type="text" id="taskName" placeholder="z. B. Geschenk besorgen" v-model="newTaskData.title">
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
                <label for="listSelect">Liste wählen *</label>
                <select name="listSelect" id="listSelect" v-model="newTaskData.list">
                    <option v-for="list in allLists" :value='list'>{{ list }}</option>
                </select>
            </div>
            <button type="button" id="createNewTaskButton" 
            @click="addNewTask" 
            :class="{'active' : inputDataOK}">
                <img src="./../assets/calendar-plus-regular.svg" alt="Create new task icon">
            </button>
            <div class="warn" v-if="showInfo" style="width: 100%; text-align: center;">{{ infoMessage }}</div>
        </form>
            
        <div id="contentWrapper">
            <main>
                <h2>Ihre Listen</h2>
                <div id="listsContainer">
                    <TaskList v-for="list in subLists" :subTasksList="list" :key="list[0].list" 
                    @delTaskEvent="delTask" 
                    @taskStatusToggleEvent="toggleTaskStatus" />
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
        gap: .25rem;
        font-size: clamp(1.4rem, 3vw, 4.5rem);
        font-weight: 100;
        padding: .5rem 0;
        border-bottom: solid thin white;
    }

    #contentWrapper {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
    }

    main {
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
        font-size: clamp(1.2rem, 3vw, 2.5rem);
        width: clamp(3rem, 5vw, 5rem);
        height: clamp(3rem, 5vw, 5rem);
        display: inherit;
        justify-content: center;
        align-items: center;
        text-align: center;
        border: solid .175rem;
        border-radius: 50%;
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
        background-color: var(--black50);
        border: none;
        margin: 1rem;
        cursor: pointer;
        pointer-events: none;
    }

    .active {
        background-color: var(--listBgC);
        pointer-events: all;
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
        align-items: flex-start;
        flex-wrap: wrap;
        gap: 1rem
    }
</style>