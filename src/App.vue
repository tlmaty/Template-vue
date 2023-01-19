<template>
    <HelloBarre content="50% de rabais le premier jour des soldes avec le code SOLDES50 !" background="#00395d" contentLink="Cliquez ici !" color="white" dateCount="18 January 2023" />
    <nav>
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link> |
        <router-link to="/divers">Divers</router-link> |
        <router-link to="/admin">Administration panel</router-link>
    </nav>
    <router-view />
</template>

<script>
    import HelloBarre from "./components/HelloBarre.vue";
    export default {
        name: 'AppVue',
        components: {
            HelloBarre
        }
    }
</script>

<style lang="scss">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }

    nav {
        padding: 30px;

        a {
            font-weight: bold;
            color: #2c3e50;

            &.router-link-exact-active {
                color: #42b983;
            }
        }
    }
</style>
