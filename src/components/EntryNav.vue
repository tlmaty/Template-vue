<template>
    <div class="entrynav">
        <h3 class="name">Nom : {{ name }}</h3>
        <p class="level">Niveau : {{ level }}</p>
        <p class="parent">Parent : {{ parent }}</p>
        <p class="position">Position : {{ position }}</p>
        <p class="link">Lien : {{ link }}</p>
        <p class="children">Enfants : {{ children }}</p>
    </div>
</template>

<script>
    export default {
        name: 'EntryNav',
        props: [
            'id',
            'name',
            'position',
            'link',
            'children',
            'level',
            'parent'
        ]
    }
</script>

<style lang="scss">
    .entrynav {
        display: flex;
        align-items: center;
        gap: 20px;
    }
</style>