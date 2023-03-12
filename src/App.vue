<script>
  
  import Sidebar from './components/Sidebar.vue';
  import Main from './components/Main.vue';
  import CreateListButton from './components/CreateListButton.vue';

  export default({
    components: {Sidebar, Main, CreateListButton},
    data() {
      return {
        newListName: '',
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
        // Todo::: bessere Validierung der Eingabe !
        if(listName !== '') {                       

          // Todo::: Neue Liste Erstellen in Main triggern ...
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
