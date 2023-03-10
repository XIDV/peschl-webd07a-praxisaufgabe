<script>
  import Sidebar from './components/Sidebar.vue';
  import Main from './components/Main.vue';
  import CreateListButton from './components/CreateListButton.vue';

  export default({
    components: {Sidebar, Main, CreateListButton},
    data() {
      return {
        tasks: null,
      }
    },
    methods: {
      showCreateListDialog() {
        document.getElementById('createListDialog').showModal();
      },
      closeCreateListDialog() {
        document.getElementById('createListDialog').close();
      }
    }
  })
</script>

<template>
  <div id="primeContainer">
    
    <dialog id="createListDialog">
      <form action="">
        <div class="few">
          <label for="listName">Name der neuen Liste</label>
          <input type="text" id="listName" placeholder="z.B. Studium" required>
        </div>
        <CreateListButton />
      </form>
      <footer>
        <a id="cancelCreation" href="#" @click.prevent="closeCreateListDialog">Abbrechen</a>
      </footer>
    </dialog>

    <Sidebar @showCreateListDialogEvent="showCreateListDialog" />
    <Main />

  </div>
  
</template>

<style scoped>
  #createListDialog {
    width: 30rem;
    color: white;
    background-color: var(--secondBgC);
    padding: 3rem;
    border: none;
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
  #createList {
    width: 6rem;
    height: 6rem;
    background-color: var(--listBgC);
    border: none;
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

  #primeContainer {
    display: flex;
  }
</style>
