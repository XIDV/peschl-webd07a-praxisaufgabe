<script>

    export default({
        name: 'Sidebar',
    });
</script>

<template>
    <div id="sidebar">
        <div id="hideBarButton">
            <img src="./../assets/chevron-left-solid.svg" alt="Sidbar visibility toggle icon">
        </div>
        <header>
            <h1>Do It!</h1>
            <p class="subtitle">Keep your Tasks insight!</p>
        </header>
        <div id="toolContainer">
            <button id="newListButton" title="Neue Liste erstellen">
                <img src="./../assets/plus-clipboard-add.svg" alt="Neue Liste-Icon">
            </button>
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

    #newListButton {
        width: 6rem;
        height: 6rem;
        background-color: var(--listBgC);
        border: none;
        cursor: pointer;
        transition: box-shadow 250ms ease-in-out;
    }
    #newListButton:hover {
        box-shadow: 0 0 0 .025rem white;
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
    }
    #hideBarButton img {
        width: 45%;
        pointer-events: none;
    }
    .cpr {
        font-size: .8rem;
        color: var(--black50);
    }
</style>