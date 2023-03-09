<script>
  import Sidebar from './components/Sidebar.vue';
  import Main from './components/Main.vue';

  export default({
    components: {Sidebar, Main},
    data() {
      return {
        tasks: null
      }
    }
  })
</script>

<template>
  <div id="primeContainer">
    <Sidebar />
    <Main />
  </div>
  
</template>

<style scoped>
  #primeContainer {
    display: flex;
  }
</style>
