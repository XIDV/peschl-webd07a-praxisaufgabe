<script>
  import Sidebar from './components/Sidebar.vue';
  import Main from './components/Main.vue';

  export default({
    components: {Sidebar, Main},
    data() {
      return {
        tasks: null
      }
    },
    methods: {
      showCreateListDialog() {
        document.getElementById('createListDialog').showModal();
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
        <button id="createList" type="button"><img src="./assets/plus-clipboard-add.svg" alt="Neue Liste-Icon"></button>
      </form>
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

  #primeContainer {
    display: flex;
  }
</style>
