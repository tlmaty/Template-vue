<template>
    <img :src="this.$props.bbbgimgsrc" :alt="this.$props.bbbgimgalt">
</template>

<script>
    export default {
        name: 'BigBannerBackground',
        props: [
            'bbbgimgsrc',
            'bbbgimgalt'
        ]
    }
</script>