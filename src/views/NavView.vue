<template>
    <h1>Page de gestion de la navigation</h1>
    <EntryNav
        name="Soldes"
        niveau="1"
        parent=""
        position="1"
        link="www.maty.com"
        children=""
        level="1"
    />
</template>

<script>
    import EntryNav from '../components/EntryNav.vue'
    export default {
        name: 'NavView',
        components: {
            EntryNav,
        }
    }
</script>