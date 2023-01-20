<template>
    <a :href="this.$props.bbentryhref">{{ bbentrytext }}</a>
</template>

<script>
    export default {
        name: 'BigBannerEntry',
        props: [
            'bbentryhref',
            'bbentrytext'
        ]
    }
</script>