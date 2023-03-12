<script>
  import _ from 'lodash';
  import Sidebar from './components/Sidebar.vue';
  import Main from './components/Main.vue';
  import CreateListButton from './components/CreateListButton.vue';

  export default({
    components: {Sidebar, Main, CreateListButton},
    data() {
      return {
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
            list: 'Demoliste',
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
        newListName: '',
      }
    },
    computed: {
      lists() {
        return _.uniq(this.tasks.map(task => task.list));
      }
    },
    methods: {
      showCreateListDialog() {
        document.getElementById('createListDialog').showModal();
      },
      closeCreateListDialog() {
        document.getElementById('createListDialog').close();
      },
      createNewList() {
        const listName = this.newListName;
        if(listName !== '') {                                             // bessere Validierung der Eingabe implementieren!
          console.log('Erstelle neue Liste: ' + listName);
          this.closeCreateListDialog();
        }
        this.newListName = '';
      },
  
    }
  })
</script>

<template>
  <div id="primeContainer">
    <dialog id="createListDialog">
      <form action="">
        <div class="few">
          <label for="listName">Name der neuen Liste</label>
          <input v-model="newListName" type="text" id="listName" placeholder="z.B. Studium">
        </div>
        <CreateListButton @click="createNewList" />
      </form>
      <footer>
        <a id="cancelCreation" href="#" @click.prevent="closeCreateListDialog">Abbrechen</a>
      </footer>
    </dialog>

    <Sidebar @showCreateListDialogEvent="showCreateListDialog" />

    <Main />

  </div>
  
</template>

<style>
  #primeContainer {
    display: flex;
  }

  #createListDialog {
    width: 30rem;
    color: white;
    background-color: var(--secondBgC);
    padding: 3rem;
    border: solid thin white;
  }
  form {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    justify-content: space-between;
  }
  .few {
    display: inherit;
    flex-direction: column;
  }

  label {
    font-size: .8rem;
    margin: 0 0 1rem 0;
  }
  #listName {
    font-size: 1.2rem;
    color: white;
    background-color: var(--firstBgC);
    padding: .5rem;
    border: none;
  }
  #listName:focus {
    outline: none;
  }

  #cancelCreation:link,
  #cancelCreation:visited {
    font-size: 1rem;
    color: var(--black50);
    text-decoration: none;
  }
  #cancelCreation:hover {
    text-decoration: underline;
  }
</style>
