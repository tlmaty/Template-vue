<template>
    <header>
        <h1>Menu</h1>
        <ul>
            <li><a href="/">Entrée 1</a></li>
            <li><a href="/">Entrée 2</a></li>
            <li><a href="/">Entrée 3</a></li>
        </ul>
    </header>
</template>

<script>
export default {
    name: 'MenuNav'
}
</script>

<style scoped lang="scss">
ul {
    display: flex;
    justify-content: space-around;
    padding: 0;
    li {
        list-style: none;
        padding: 0;
        a {
            text-decoration: none;
        }
    }
}
</style>