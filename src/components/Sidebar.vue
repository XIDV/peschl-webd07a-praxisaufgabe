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
            },
            checkWindowWidth() {
                window.innerWidth < 880 ? this.sidebarVisible = false : this.sidebarVisible = true;
            }
        },
        created() {
            this.checkWindowWidth();
            window.addEventListener('resize', this.checkWindowWidth);
        }
    });
</script>

<template>
    <div id="sidebar" class="default" :class="{ hidden : !sidebarVisible }">
        <div id="hideBarButton" @click="toggleVisibility" title="Sidebar ein-/ausblenden">
            <img src="./../assets/chevron-left-solid.svg" alt="Sidbar visibility toggle icon">
        </div>
        <header>
            <h1>Do It!</h1>
            <p class="subtitle">Procrastinators unite! Tomorrw. Maybe.</p>
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
        background-color: var(--secondBgC);
    }
    
    .default {
        flex: 0 0 20rem;
        padding: 2rem;   
    }

    .default #hideBarButton {
        left: 18.5rem;
    }

    #sidebar,
    #sidebar * {
        transition: all 250ms ease-in-out;
    }

    .hidden {
        flex: 0 0 0;
        padding: 0;
    }
    .hidden #hideBarButton {
        left: -1.5rem;
    }
    .hidden img {
        transform: rotate(180deg);
    }
    .hidden *:not(img) {
        display: none;
    }

    h1,
    .subtitle,
    .cpr {
        display: block;
        margin: 0;
    }

    .cpr {
        font-size: .8rem;
        color: var(--black50);
    }
    h1 {
        font-size: clamp(3rem, 5vw, 6rem);
        font-weight: 100;
        text-align: center;
    }
    .subtitle {
        text-align: center;
        font-weight: 700;
        font-style: italic;
    }

    #hideBarButton {
        position: fixed;
        top: 50vh;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 3rem;
        height: 3rem;
        background-color: var(--secondBgC);
        border-radius: 50%;
        cursor: pointer;
        transform: translateY(-50%);
        transition: transform 250ms ease-in-out;
    }
    #hideBarButton img {
        width: 45%;
        pointer-events: none;
    }
    #hideBarButton:hover {
        transform: scale(110%) translateY(-50%);
    }

    #toolContainer {
        position: sticky;
        top: 20vh;
        height: 50vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #newListButton {
        width: 8rem;
        height: 8rem;
    }

    footer {
        position: sticky;
        top: 95vh;
        text-align: center;
    }
    
</style>