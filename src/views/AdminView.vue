<script>
import HelloBarre from "../components/HelloBarre.vue";
import json from '../assets/label.json'
export default {
    name: 'AdminView',
    components: { 
        HelloBarre 
    },
    data() {
        return {
            // barres: [
            //     { 
            //         id: 0, 
            //         title: 'Soldes',
            //         content: '50% de rabais le premier jour des soldes avec le code SOLDES50 !', 
            //         background: '#00395d',
            //         contentLink: 'Cliquez ici !',
            //         color: 'white',
            //         dateCount: '18 january 2023 23:59',
            //     },
            //     { 
            //         id: 1, 
            //         title: 'Livraison gratuite',
            //         content: 'Profitez de la livraison gratuite jusqu\'au 31 janvier', 
            //         background: '#FF352F',
            //         contentLink: 'J\'en profite !',
            //         color: 'white',
            //         dateCount: '1 february 2023 23:59',
            //     },
            //     { 
            //         id: 2, 
            //         title: 'Or gratuit',
            //         content: 'L\'or est gratuit tout le mois de janvier !', 
            //         background: '#ad8827',
            //         contentLink: 'Je fonce !',
            //         color: 'white',
            //         dateCount: '10 june 2023 23:59',
            //     }
            // ],
            barres : json
        }
    },
    methods: {
        editbarre(el) {
            var barreId = el.id;

            var newContent = prompt('Nouveau contenu : ', this.barres[barreId].content);
            this.barres[barreId].content = newContent;

            var newTitle = prompt('Nouveau titre : ', this.barres[barreId].title);
            this.barres[barreId].title = newTitle;

            var newBackground = prompt('Nouveau fond : ', this.barres[barreId].background);
            this.barres[barreId].background = newBackground;

            var newLink = prompt('Nouveau lien : ', this.barres[barreId].contentLink);
            this.barres[barreId].contentLink = newLink;

            var newColor = prompt('Nouvelle couleur de texte : ', this.barres[barreId].color);
            this.barres[barreId].color = newColor;

            var newDate = prompt('Nouvelle date : ', this.barres[barreId].dateCount);
            this.barres[barreId].dateCount = newDate;

            this.datetimer(barreId);
            for (let i = 0; i < this.barres.length; i++) {
                this.barres[i].id = i
            }
            return;
        },
        dltbarre(el) {
            this.barres.splice(this.barres.indexOf(el), 1)
            for (let i = 0; i < this.barres.length; i++) {
                this.barres[i].id = i;
                this.datetimer(i)
            }
        },
        addbarre() {
            for (let i = 0; i < this.barres.length; i++) {
                this.barres[i].id = i;
            }
            var newBarre = {
                id: this.barres.length,
                title: prompt('Titre : '),
                content: prompt('Contenu : '),
                background: prompt('Couleur de fond : '),
                contentLink: prompt('Lien : '),
                color: prompt('Couleur du texte : '),
                dateCount: prompt('Date : '),
            }
            this.barres.push(newBarre)
            this.datetimer(this.barres.length-1)
        },
        datetimer(nb) {
            var countDownDate = new Date(this.barres[nb].dateCount).getTime();
            if (!isNaN(countDownDate)) {
                var x = setInterval(function() {
                    var now = new Date().getTime();
                    var distance = countDownDate - now;

                    var barres = document.querySelectorAll('.barres .demo')

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
        exportbarre() {
            var myJsonString = JSON.stringify(this.barres, null, 2);

            // POST avec API fetch renvoi une 404

            // const requestOptions = {
            //     method: "POST",
            //     headers: new Headers({
            //         'Content-Type': 'application/json',
            //         'Accept': 'application/json',
            //     }),
            //     body: myJsonString
            // };
            // fetch("../assets/label.json", requestOptions)
            //     .then(response => response.json())
            //     .then(data => (this.postId = data.id));

            // Téléchargement d'un fichier label.json 

            const blob = new Blob([myJsonString], {type:'application/json'})
            const link = document.createElement('a')
            link.href = URL.createObjectURL(blob)
            link.download = 'label'
            link.click()
            URL.revokeObjectURL(link.href)
        }
    },
    mounted() {
        var barres = document.querySelectorAll('.barres .demo')
        let i = -1;
        barres.forEach(() => {
            i++
            this.datetimer(i)
        })
    },
}

</script>

<template>
    <div class="adminpanel">
      <img alt="Vue logo" src="../assets/logo.png">
      <ul class="barres">
        <li class="containerbarre"
            v-for="barre in barres"
            :key="barre.id"
        >
            <p>{{ barre.title }}</p>
            <HelloBarre
                :content="barre.content"
                :background="barre.background"
                :contentLink="barre.contentLink"
                :color="barre.color"
                :dateCount="barre.dateCount"
                :data-date="barre.dateCount"
            />
            <button v-on:click="editbarre(barre)">Modifier</button>
            <button v-on:click="dltbarre(barre)">Supprimer</button>
        </li>
      </ul>
      <button v-on:click="addbarre()">Ajouter une barre</button>
      <button v-on:click="exportbarre()">Exporter en JSON</button>
    </div>
</template>

<style lang="scss">
    .adminpanel {
        .barres {
            padding: 0;

            .containerbarre {
                display: flex;
                position: relative;
                margin: 20px 0;

                 & > p {
                    position: absolute;
                    top: -40px;
                    color: black;
                }
                
                .hellobarre {
                    position: relative;
                    width: calc(100% - 65px);

                    span {
                        position: absolute;
                    }
                }
            }
        }
    }
</style>