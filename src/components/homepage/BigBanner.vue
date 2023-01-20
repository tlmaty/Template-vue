<template>
    <div class="component-bigbanner">
        <h1>Composant : BigBanner</h1>
        <div class="data">
            <div class="bbbg">
                <h2>Image de fond</h2>
                <BigBannerBackground
                    :bbbgimgsrc="this.bigbannerdata.bigbannerbackgroundata.src"
                    :bbbgimgalt="this.bigbannerdata.bigbannerbackgroundata.alt"
                />
                <button @click="editcomponent(this.bigbannerdata.bigbannerbackgroundata)">Modifier l'image de fond</button>
            </div>
            <div class="bbtitle">
                <h2>Titre</h2>
                <BigbannerTitle
                    :bbtitle="this.bigbannerdata.bigbannertitledata.text"
                />
                <button @click="editcomponent(this.bigbannerdata.bigbannertitledata)">Modifier le titre</button>
            </div>
            <div class="bbimg">
                <h2>Image</h2>
                <BigbannerImage
                    :bbimgsrc="this.bigbannerdata.bigbannerimagedata.src"
                    :bbimgalt="this.bigbannerdata.bigbannerimagedata.alt"
                    :bbimgwidth="this.bigbannerdata.bigbannerimagedata.width"
                    :bbimgheight="this.bigbannerdata.bigbannerimagedata.height"
                />
                <button @click="editcomponent(this.bigbannerdata.bigbannerimagedata)">Modifier l'image</button>
            </div>
            <div class="bbparagraph">
                <h2>Paragraphe</h2>
                <BigbannerParagraph
                    :bbparagraph="this.bigbannerdata.bigbannerparagraphdata.text"
                />
                <button @click="editcomponent(this.bigbannerdata.bigbannerparagraphdata)">Modifier le paragraphe</button>
            </div>
            <div class="bblink">
                <h2>Lien</h2>
                <BigbannerLink
                    :bblinkhref="this.bigbannerdata.bigbannerlinkdata.href"
                    :bblinktext="this.bigbannerdata.bigbannerlinkdata.text"
                />
                <button @click="editcomponent(this.bigbannerdata.bigbannerlinkdata)">modifier le lien</button>
            </div>
            <div class="bbentries">
                <h2>Entrées</h2>
                <ul>
                    <li v-for="entry in this.bigbannerdata.bigbannerentriesdata" :key="entry.id">
                        <BigbannerEntry
                            :bbentryhref="entry.bbentryhref"
                            :bbentrytext="entry.bbentrytext"
                        />
                    </li>
                </ul>
                <button @click="editcomponent(this.bigbannerdata.bigbannerentriesdata)">Modifier les entrées</button>
            </div>
        </div>
    </div>
</template>

<script>
    import BigBannerBackground from './BigBanner/BigbannerBackground.vue';
    import BigbannerTitle from './BigBanner/BigbannerTitle.vue';
    import BigbannerImage from './BigBanner/BigbannerImage.vue';
    import BigbannerParagraph from './BigBanner/BigbannerParagraph.vue';
    import BigbannerLink from './BigBanner/BigbannerLink.vue';
    import BigbannerEntry from './BigBanner/BigbannerEntry.vue';
    export default {
        name: 'BigBanner',
        components: {
            BigBannerBackground,
            BigbannerImage,
            BigbannerTitle,
            BigbannerParagraph,
            BigbannerLink,
            BigbannerEntry
        },
        data() {
            return {
                bigbannerdata: {
                    bigbannerbackgroundata: {
                        'name': 'bbbgimg',
                        'src': 'https://www.maty.com/homepage/RWD/REFONTE_NOEL_2022/Banners/2023-01-18/A-desktop-new-AH22-Soldes-2eme-demarque.jpg',
                        'alt': 'Image background'
                    },
                    bigbannertitledata: {
                        'name': 'bbtitle',
                        'text': 'Soldes Maty, jusqu\'à -50%'
                    },
                    bigbannerimagedata: {
                        'name': 'bbimg',
                        'src': 'https://www.maty.com/homepage/RWD/REFONTE_NOEL_2022/Banners/2023-01-18/logo-soldes-2eme-dem-horizontal.png',
                        'alt': '2eme demarque soldes',
                        'width': 416,
                        'height': 190
                    },
                    bigbannerparagraphdata: {
                        'name': 'bbparagraph',
                        'text': '-10%* supplémentaire sur une sélection de bijoux et montres'
                    },
                    bigbannerlinkdata: {
                        'name': 'bblink',
                        'href': 'https://www.maty.com',
                        'text': 'J\'en profite !'
                    },
                    bigbannerentriesdata: [
                        {
                            'id': 0,
                            'bbentryhref': 'https://www.google.com',
                            'bbentrytext': 'Femme'
                        },
                        {
                            'id': 1,
                            'bbentryhref': 'https://www.google.com',
                            'bbentrytext': 'Homme'
                        },
                        {
                            'id': 2,
                            'bbentryhref': 'https://www.google.com',
                            'bbentrytext': 'Bagues'
                        },
                        {
                            'id': 3,
                            'bbentryhref': 'https://www.google.com',
                            'bbentrytext': 'Bracelets'
                        },
                        {
                            'id': 4,
                            'bbentryhref': 'https://www.google.com',
                            'bbentrytext': 'Boucles'
                        },
                        {
                            'id': 5,
                            'bbentryhref': 'https://www.google.com',
                            'bbentrytext': 'Montres'
                        },
                    ]
                }
            }
        },
        mounted() {
        },
        methods: {
            editcomponent(el) {
                // var elementsdata = Object.entries(el.bigbannerdata)
                // for (let i = 0; i < elementsdata.length; i++) {
                //     let elementactive = elementsdata[i]
                //     console.log(elementsdata[i])

                //     var newcontent = prompt('Nouveau ' + elementactive[1])
                // }
                // console.log(Object.getOwnPropertyNames(el.bigbannerdata))

                switch (el.name) {
                    case 'bbbgimg':
                        var newbgsrc = prompt('Nouvelle image de fond', el.src)
                        el.src = newbgsrc
                        var newbgalt = prompt('Nouvelle balise alt', el.alt)
                        el.alt = newbgalt
                        break;

                    case 'bbtitle':
                        var newtitle = prompt('Nouveau titre', el.text)
                        el.text = newtitle
                        break;
                        
                    case 'bbimg':
                        var newimgsrc = prompt('Nouvelle image ', el.src)
                        el.src = newimgsrc
                        var newimgalt = prompt('Nouvelle balise alt', el.alt)
                        el.alt = newimgalt
                        break;

                    case 'bbparagraph':
                        var newparagraph = prompt('Nouveau paragraphe', el.text)
                        el.text = newparagraph
                        break;

                    case 'bblink':
                        var newlinkhref = prompt('Nouvau lien ', el.href)
                        el.href = newlinkhref
                        var newlinktext = prompt('Nouveau texte', el.text)
                        el.text = newlinktext
                        break;

                    default:
                        console.log(el[0])
                }

                return
            }
        }
    }
</script>

<style lang="scss">
    .component-bigbanner {
        background: #e6e6e6;
        padding: 20px;
        margin: 20px;
        border: solid 1px #333;
        border-radius: 5px;

        h1 {
            padding-bottom: 20px;
            margin-bottom: 20px;
            border-bottom: solid 1px rgba(51, 51, 51, 0.5)
        }

        .data {
            display: flex;
            gap: 20px;

            > div {
                width: calc(100% / 6);
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: space-between;

                h2 {
                    margin-bottom: 50px;
                    text-decoration: underline;
                }

                img {
                    height: auto;
                }
            }

            ul {
                li {
                    list-style: none;
                }
            }

            button {
                margin-top: 50px;
            }
        }

        * {
            max-width: 100%;
            margin: 0;
            padding: 0;
        }
    }
</style>