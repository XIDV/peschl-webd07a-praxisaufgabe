//  App.vue ::: Root-Element der Anwendung

<script>
  
  //  Import der Komponenten 'Sidebar', 'Main' und 'CreateListButton'
  import Sidebar from './components/Sidebar.vue';
  import Main from './components/Main.vue';
  import CreateListButton from './components/CreateListButton.vue';

  export default({
    //  Registrierung der Komponenten
    components: {Sidebar, Main, CreateListButton},

    data() {
      return {
        newListName: '',
        newListNameTemp: '',
        // delListDialogVisible: false,
        listName: '',
        delListName: '',
        showInfo: false,
        changer: false,
        fileOperation: '',
      }
    },

    //  Definition der Methoden 
    methods: {
      //  Anzeige des Dialogs zum erstellen einer neuen Liste
      showCreateListDialog() {
        document.getElementById('createListDialog').showModal();
      },
      
      //  Schließen des Dialogs zum erstellen einer neuen Liste, Wert der Property 'showInfo' wird auf false gesetzt
      closeCreateListDialog() {
        document.getElementById('createListDialog').close();
        this.showInfo = false;
      },
      
      //  Property 'listName' erhält den Wert von Methodenparameter 'name', Anzeige des Dialogs zum löschen einer Aufgabenliste
      openDelDialog(name) {
        this.listName = name;
        document.querySelector('#delListDialog').showModal();
      },

      //  Schließen des Dialogs zum löschen einer Aufgabenliste
      closeDelDialog() {
        document.querySelector('#delListDialog').close();
      },

      //  Die Property 'delListName' erhält den Wert der Property 'listName', die Methode 'closeDelDialog()' wird aufgerufen
      triggerListDelete() {
        this.delListName  = this.listName;
        this.closeDelDialog();
      },

      //  Prüfen ob der übergebene String nicht leer ist und nicht nur aus Leerzeichen beseteht.
      validString(stringToValidate) {
        return stringToValidate !== '' && 
          !stringToValidate.split('', 1)
          .every(d => d === ' ');
      },
      
      //  Erstellen einer neuen Liste
      createNewList() {
        const listName = this.newListName;
        if(this.validString(listName)) {                    //  Aufruf d. Methode 'validString(String)'. Wenn 'true' ...
          this.newListNameTemp = listName;                  //  ... setze Wert von Property 'newListNameTemp' auf Wert von 'listName' ...
          this.closeCreateListDialog();                     //  ... rufe Methode 'closeCreateListDialog()' auf ...
          this.changer = !this.changer;                     //  ... invertiere den Wert von 'changer'.
        } else {                                            //  Wenn 'false' ...
          this.showInfo = true;                             //  ... setze den Wert von 'showInfo' auf 'true'.
        }
        this.newListName = '';                              //  Setze den Wert von 'newListName' zurück auf ''.
      },

      //  Setze den Wert von 'fileOperation' auf den Wert des Parameters 'operation'
      //  (Definiert welche Dateioperation [lesen oder schreiben] getriggert werden soll.)
      triggerFileOp(operation) {
        this.fileOperation = operation;
      },

      resetFileOperation() {
        this.fileOperation = '';
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

    <Sidebar 
      @showCreateListDialogEvent="showCreateListDialog"
      @triggerFileOpEvent="triggerFileOp"
      :changeTrigger="changer" />
    
    <!-- 
      - Beim Empfang eines 'resetNewListNameEvent' wird die Property 'newListName' auf '' gesetzt.
      - Beim Empfang eines 'resetDelListNameEvent' wief die Property 'delListName' auf '' gesetzt.
     -->
    <Main @delListEvent="openDelDialog" 
      @resetNewListNameEvent="newListNameTemp = ''"
      @resetDelListNameEvent="delListName = ''" 
      @fileOpCompleted="resetFileOperation" 
      :declaredFileOp="fileOperation" 
      :newName="newListNameTemp" 
      :delListName="delListName"/>
    
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
