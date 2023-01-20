<template>
    <a :href="this.$props.bblinkhref">{{ bblinktext }}</a>
</template>

<script>
    export default {
        name: 'BigBannerLink',
        props: [
            'bblinkhref',
            'bblinktext'
        ]
    }
</script>