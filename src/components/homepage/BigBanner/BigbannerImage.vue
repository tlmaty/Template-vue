<template>
    <img :src="this.$props.bbimgsrc" :alt="this.$props.bbimgalt" :width="this.$props.bbimgwidth" :height="this.$props.bbimgheight">
</template>

<script>
    export default {
        name: 'BigBannerImage',
        props: [
            'bbimgsrc',
            'bbimgalt',
            'bbimgwidth',
            'bbimgheight'
        ]
    }
</script>