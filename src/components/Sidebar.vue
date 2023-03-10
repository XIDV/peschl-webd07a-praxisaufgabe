<script>
    import CreateListButton from './CreateListButton.vue';

    export default({
        name: 'Sidebar',
        components: {CreateListButton},
        data() {
            return {
                sidebarVisible: true,
            }
        },
        methods: {
            toggleVisibility() {
                this.sidebarVisible = !this.sidebarVisible;
            },
            showCreateListDialog() {
                this.$emit('showCreateListDialogEvent');
            }
        }
    });
</script>

<template>
    <div id="sidebar" :class="{ hidden : !sidebarVisible }">
        <div id="hideBarButton" @click="toggleVisibility" title="Sidebar ein-/ausblenden">
            <img src="./../assets/chevron-left-solid.svg" alt="Sidbar visibility toggle icon">
        </div>
        <header>
            <h1>Do It!</h1>
            <p class="subtitle">Keep your Tasks insight!</p>
        </header>
        <div id="toolContainer">
            <CreateListButton @click="showCreateListDialog" />
        </div>
        <footer>
            <p class="cpr">&copy; Sebastian Peschl (2023)</p>
        </footer>
    </div>
</template>

<style scoped>
    #sidebar {
        position: relative;
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        background-color: var(--secondBgC);
        padding: 2rem;
    }

    #sidebar,
    #sidebar img {
        transition: transform 250ms ease-in-out;
    }

    .hidden {
        transform: translateX(-100%);
    }
    .hidden img {
        transform: rotate(180deg);
    }

    h1,
    .subtitle,
    .cpr {
        display: block;
        margin: 0;
    }
    h1 {
        font-size: 6rem;
        font-weight: 100;
    }
    .subtitle {
        font-weight: 700;
        font-style: italic;
    }

    #hideBarButton {
        position: absolute;
        right: -1.5rem;
        top: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 3rem;
        height: 3rem;
        background-color: var(--secondBgC);
        border-radius: 50%;
        cursor: pointer;
        transition: transform 250ms ease-in-out;
    }
    #hideBarButton img {
        width: 45%;
        pointer-events: none;
    }
    #hideBarButton:hover {
        transform: scale(110%);
    }
    .cpr {
        font-size: .8rem;
        color: var(--black50);
    }
</style>