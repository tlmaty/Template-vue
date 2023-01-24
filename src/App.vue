<template>
    <div class="hellobarres">
        <HelloBarre
            v-for="barreactive in barresactivesArr"
            :key="barreactive.id" 
            :content="barreactive.content"
            :background="barreactive.background"
            :contentLink="barreactive.contentLink"
            :color="barreactive.color"
            :dateCount="barreactive.dateCount"
        ></HelloBarre>
    </div>
    <button id="next" @click="barrerotation()">Suivante</button>
    <nav>
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link> |
        <router-link to="/divers">Divers</router-link> |
        <router-link to="/admin">Administration panel</router-link> |
        <router-link to="/nav">Administration navigation</router-link> | 
        <router-link to="/hp">Administration homepage MATY</router-link>
    </nav>
    <router-view />
</template>

<script>
    import HelloBarre from "./components/HelloBarre.vue";
    import json from './assets/label.json'
    export default {
        name: 'AppVue',
        components: {
            HelloBarre
        },
        data() {
            return {
                barres : json,
                'barresactivesArr': [],
            }
        },
        mounted() {
            for (let i = 0; i < this.barres.length; i++) {
                if (this.barres[i].isActive) {
                    this.barresactivesArr.push(this.barres[i])
                }
            }
        },
        updated() {
            var barres = document.querySelectorAll('.hellobarres .hellobarre')

            // Ajout du timer à toutes les barres
            let i = 0;
            barres.forEach(() => {
                this.datetimer(i);
                i++
            })

            // Rotation des barres
            if (barres.length > 1) {
                var tslY = 0
                for (let i = 0; i < barres.length; i++) {
                    if (i < barres.length -1) {
                        // console.log(i)
                        // console.log(barres[i].getBoundingClientRect().height)
                        // tslY = tslY + barres[i].getBoundingClientRect().height
                        tslY = document.querySelector('.hellobarres').getBoundingClientRect().height
                        tslY -= barres[barres.length-1].getBoundingClientRect().height
                    }
                }
                document.querySelector('.hellobarres').style.transform = (`translateY(-${tslY}px)`);
                console.log(tslY)
                this.barrerotation()
            }
        },  
        methods: {
            datetimer(nb) {
                var countDownDate = new Date(this.barresactivesArr[nb].dateCount).getTime();
                if (!isNaN(countDownDate)) {
                    var x = setInterval(function() {
                        var now = new Date().getTime();
                        var distance = countDownDate - now;

                        var barres = document.querySelectorAll('.hellobarres .hellobarre .demo')

                        var days = Math.floor(distance / (1000 * 60 * 60 * 24));
                        days == '0' ? days = '' : days = days + 'j '
                        var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)) + 'h ';
                        var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60)) + 'm ';
                        var seconds = Math.floor((distance % (1000 * 60)) / 1000) + 's';

                        barres[nb].innerHTML = days + hours + minutes + seconds;

                        if (distance < 0) {
                            barres[nb].innerHTML = '';
                            clearInterval(x)
                        }
                    }, 1000);
                }
            },
            barrerotation() {
                console.log('abab')
                var barres = document.querySelectorAll('.hellobarres .hellobarre')
                document.querySelector('.hellobarre').parentNode.insertBefore(barres[barres.length - 1], barres[0])
            }
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
