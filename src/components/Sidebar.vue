<script>
    import CreateListButton from './CreateListButton.vue';

    export default({
        name: 'Sidebar',
        components: {CreateListButton},
        props: {
            changeTrigger: Boolean,
        },
        data() {
            return {
                sidebarVisible: true,
            }
        },
        emits: ['triggerFileOpEvent', 'showCreateListDialogEvent'],
        methods: {
            toggleVisibility() {
                this.sidebarVisible = !this.sidebarVisible;
            },
            checkWindowWidth() {
                window.innerWidth < 880 ? this.sidebarVisible = false : this.sidebarVisible = true;
            },
        },
        created() {
            this.checkWindowWidth();
            window.addEventListener('resize', this.checkWindowWidth);
        },
        watch: {
            changeTrigger() {
                this.checkWindowWidth();
            },
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
            <CreateListButton @click="$emit('showCreateListDialogEvent')" />
            <div>
                <button type="button" id="importTasks" title="Aufgaben importieren" @click="$emit('triggerFileOpEvent', 'import')"><img src="./../assets/import-arrow-down.svg" alt="Import-Icon"></button>
                <button type="button" id="exportTasks" title="Aufgaben exportieren" @click="$emit('triggerFileOpEvent', 'export')"><img src="./../assets/floppy-disk.svg" alt="Save-Icon"></button>
            </div>

        </div>
        <footer>
            <p class="cpr">&copy; Sebastian Peschl (2023)</p>
        </footer>
    </div>
</template>

<style scoped>
    #sidebar {
        position: fixed;
        top: 0;
        min-height: 100vh;
        background-color: var(--secondBgC);
        z-index: 2;
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
        transition: transform 250ms ease-in-out;
        z-index: 3;
    }
    .default #hideBarButton {
        right: .5rem;
        border: solid .125rem;
        transform: translate(50%, -50%);
    }
    .hidden #hideBarButton {
        left: 0;
        border: none;
        transform: translate(-50%, -50%);
    }
    #hideBarButton img {
        width: 45%;
        pointer-events: none;
    }
    .default #hideBarButton:hover {
        transform: scale(110%) translate(50%, -50%);
    }

    .hidden #hideBarButton:hover {
        transform: scale(110%) translate(-50%, -50%);
    }

    @media  screen and (min-width: 32em) {
        #sidebar {
            position: relative;
        }
        #hideBarButton {
            position: absolute;
        }
        .default #hideBarButton{
            border: none;
        }
    }
    
    .default {
        flex: 0 0 20rem;
        padding: 2rem;   
    }

    #sidebar,
    #sidebar * {
        transition: all 250ms ease-in-out;
    }

    .hidden {
        flex: 0 0 0;
        padding: 0;
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

    #toolContainer {
        position: sticky;
        top: 20vh;
        height: 50vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 1rem;
    }

    #toolContainer div {
        display: inherit;
        flex-direction: row;
        justify-content: space-around;
    }

    #importTasks,
    #exportTasks {
        width: 4rem;
        height: 4rem;
        background-color: transparent;
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