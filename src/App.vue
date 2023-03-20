<script>
  
  import Sidebar from './components/Sidebar.vue';
  import Main from './components/Main.vue';
  import CreateListButton from './components/CreateListButton.vue';

  export default({
    components: {Sidebar, Main, CreateListButton},
    data() {
      return {
        newListName: '',
        newListNameTemp: '',
        delListDialogVisible: false,
        listName: '',
        delListName: '',
        showInfo: false,
        changer: false,
        fileOperation: '',
      }
    },
    methods: {
      showCreateListDialog() {
        document.getElementById('createListDialog').showModal();
      },
      closeCreateListDialog() {
        document.getElementById('createListDialog').close();
        this.showInfo = false;
      },

      openDelDialog(name) {
        this.listName = name;
        document.querySelector('#delListDialog').showModal();
      },
      closeDelDialog() {
        document.querySelector('#delListDialog').close();
      },
      triggerListDelete() {
        this.delListName  = this.listName;
        this.closeDelDialog();
      },
      validString(stringToValidate) {
        return stringToValidate !== '' && 
          !stringToValidate.split('', 1)
          .every(d => d === ' ');
      },
      
      createNewList() {
        const listName = this.newListName;
        if(this.validString(listName)) {
          this.newListNameTemp = listName;
          this.closeCreateListDialog();
          this.changer = !this.changer;
        } else {
          this.showInfo = true;
        }
        this.newListName = '';
      },
  
      triggerFileOp(operation) {
        this.fileOperation = operation;
        // this.fileOperation = '';
      }
    }
  })
</script>



<template>
  <div id="primeContainer">

    <dialog id="delListDialog">
      <header>
        <h3>Liste Löschen?</h3>
      </header>
      <div>
        <p>Wollen Sie die Liste <strong>"{{ listName }}"</strong> mit allen darin enthaltenen Aufgaben löschen?"</p>
        <p><strong>Dieser Vorgang kann nicht wiederrufen werden!</strong></p>
      </div>
      <div>
        <button type="button" id="cancelDelete" @click="closeDelDialog">Abbrechen!</button>
        <button type="button" id="confirmDelete" @click="triggerListDelete">Liste jetzt löschen!</button>
      </div>
    </dialog>
    
    <dialog id="createListDialog">
      <form action="">
        <div class="few">
          <label for="listName">Name der neuen Liste</label>
          <input v-model="newListName" type="text" id="listName" placeholder="z.B. Studium">
          <div v-if="showInfo" class="warn">Bitte geben Sie einen Namen für die neue Liste ein.</div>
        </div>

        <CreateListButton @click.prevent="createNewList" />
      
      </form>
      <footer>
        <a id="cancelCreation" href="#" @click.prevent="closeCreateListDialog">Abbrechen</a>
      </footer>
    </dialog>

    
    <Sidebar @showCreateListDialogEvent="showCreateListDialog" :changeTrigger="changer" @triggerFileOpEvent="triggerFileOp" />
    <Main :newName="newListNameTemp" :delListName="delListName" @delListEvent="openDelDialog" @resetNewListNameEvent="newListNameTemp = ''" @resetDelListNameEvent="delListName = ''" :declaredFileOp="fileOperation" />
    
  </div>
  
</template>



<style>
  #primeContainer {
    position: relative;
    display: flex;
  }

  dialog {
    width: clamp(20rem, 90vw, 30rem);
    color: white;
    background-color: var(--secondBgC);
    padding: 3rem;
    border: solid thin white;
  }

  dialog form {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: .5rem;
  }

  dialog::backdrop {
    backdrop-filter: blur(.5rem);
  }

  #delListDialog div:last-of-type {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
  }

  #delListDialog button {
    font-size: 1.2rem;
    font-weight: 900;
    width: 20rem;
    height: 4rem;
    padding: .5rem;
  }

  #cancelDelete {
    background-color: var(--black50);
  }

  #confirmDelete {
    background-color: var(--warnColor);
  }

  dialog header {
    text-align: center;
  }

  dialog div:last-of-type {
    display: flex;
    justify-content: space-evenly;
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

  dialog #newListButton {
    width: 20%;
    height: 20%;
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

  .warn {
    font-size: 1rem;
    font-weight: 900;
    color: var(--warnColor);
  }
</style>
