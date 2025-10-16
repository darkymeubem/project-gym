
<script setup>
    const props = defineProps({
        modelValue: Number
    })

    const emit = defineEmits(['update:modelValue'])

    function goHome() {
        emit('update:modelValue', 1) //update value in parents
    }
</script>

<template>
    <header>
        <div class="head-screen">
                <h1 style="color: slateblue;opacity: 60%;">Gym Planner</h1>
                <button @click="goHome">
                    <i class="fa-solid fa-home"></i>
                </button>
        </div>
    </header>
    <main>
        <slot/>
    </main>
    <footer>
        <small>Criado por Felipe Pedroza</small>
        <a href="https://www.github.com/darkymeubem" target="_blank">
            <img src="https://avatars.githubusercontent.com/u/73255212?v=4" alt="pfp">
            <div>
                <p>darkymeubem</p>
                <i class="fa-brands fa-github"></i>
            </div>
        </a>
    </footer>
</template>

<style scoped>
    .head-screen{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }

    header,footer,main{
        padding: 1rem;
        width: 100%;
        max-width: 700px;
        margin: 0 auto;
    }
    main{
        flex: 1;
    }

    footer{
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        align-items: center;
        padding: 2rem 0;
        padding-bottom: 3rem;
    }
    footer a{
        display: flex;
        color: #000;
        align-items: center;
        gap: 0.5rem;
        padding: 0.4rem;
        padding-right:0.5rem;
        background: var(--background-muted);
        border-radius: 4rem;
        border: 1px solid transparent;
        transition-duration: 200ms;
        text-decoration: none;
    }
    footer a div {
        display: flex;
        gap: 0.5rem;
        align-items:center;
        opacity: 90%;
    }

    footer a:hover{
        border-color: var(--color-link);
    }

    footer a img{
        max-width: 30px;
        aspect-ratio: 1 / 1;
        border: 100%;
    }
</style>
