//  CreateListButton.vue ::: Komponente definiert eine Schaltfläche

<script>

    export default({
        name: 'CreateListButton',
    })
</script>


<template>
    <button id="newListButton" title="Neue Liste erstellen" @click="showCreateListDialog">
        <img src="./../assets/plus-clipboard-add.svg" alt="Neue Liste-Icon">
    </button>
</template>


<style scoped>
    #newListButton {
        min-width: 3rem;
        background-color: var(--listBgC);
        border: none;
        cursor: pointer;
        transition: box-shadow 250ms ease-in-out;
    }
    #newListButton:hover {
        box-shadow: 0 0 0 .025rem white;
    }
</style>