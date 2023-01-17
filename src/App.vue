<template>
    <HelloBarre content="50% de rabais le premier jour des soldes avec le code SOLDES50 !" background="#00395d" contentLink="Cliquez ici !" color="white" />
    <slot :hour="hour" :min="min" :sec="sec"></slot>
    <nav>
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link> |
        <router-link to="/divers">Divers</router-link>
    </nav>
    <router-view />
</template>

<script>
    import HelloBarre from "./components/HelloBarre.vue";
    export default {
        name: 'AppVue',
        components: {
            HelloBarre
        },
        props: {
            endDate: {
                type: Date,
                default() {
                    return new Date;
                }
            },
            negative: {
                type: Boolean,
                default: false
            }
        },
        data() {
            return {
                now: new Date(),
                timer: null
            }
        },
        computed() {
            function hour() {
                let h = Math.trunc((this.endDate - this.now) / 1000 / 3600);
                return h > 9 ? h : '0' + h;
            }
            function min() {
                let m = Math.trunc((this.endDate - this.now) / 1000 / 60) % 60;
                return m > 9 ? m : '0' + m;
            }
            function sec() {
                let s = Math.trunc((this.endDate - this.now) / 1000) % 60
                return s > 9 ? s : '0' + s;
            }
        },
        watch: {
            endDate: {
                immediate: true,
                handler(newVal) {
                    if (this.timer) {
                        clearInterval(this.timer)
                    }
                    this.timer = setInterval(() => {
                        this.now = new Date()
                        if (this.negative)
                            return
                        if (this.now > newVal) {
                            this.now = newVal
                            this.$emit('endTime')
                            clearInterval(this.timer)
                        }
                    }, 1000)
                }
            }
        },
        beforeUnmount() {
            clearInterval(this.timer)
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
