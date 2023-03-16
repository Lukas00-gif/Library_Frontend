<template>
    <div>
        <div id="nav">
            <router-link to="/">Home</router-link> |
            <router-link to="/add_livros">Adicionar Livros</router-link>
        </div>
    </div>
</template>

<script>
    export default {
        name: "NavBar"
    }
</script>

<style scoped>
#nav { 
        background: #000000;
        border-bottom: 4px solid #0f0e0e;
        padding: 12px 40px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }

    #nav a {
        color: #cb5729;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }

    #nav a:hover {
        color: #FFF;
    }
</style>