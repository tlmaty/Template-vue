<template>
    <div class="hellobarre" :style="{ background: this.background, color: this.color }">
        <p>{{ content }} <a href="#">{{ contentLink }}</a><span class="demo"></span></p>
        <span>X</span>
    </div>
</template>

<script>
    export default {
        name: 'HelloBarre',
        props: [
            'content',
            'background',
            'color',
            'contentLink',
            'dateCount',
        ],
        mounted() {
            let helloBarre = document.querySelector('.hellobarre');
            let closeBtn = document.querySelector('.hellobarre > span');
            closeBtn.addEventListener('click', () => {
                helloBarre.classList.add('closed');
            });
            this.countDown()
        },

        methods: {
            countDown : () => {
                var countDownDate = new Date("28 janvier 2023").getTime();

                var x = setInterval(function() {
                    var now = new Date().getTime();

                    var distance = countDownDate - now;

                    var days = Math.floor(distance / (1000 * 60 * 60 * 24));
                    days == '0' ? days = '' : days = days + 'j '
                    var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)) + 'h ';
                    var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60)) + 'm ';
                    var seconds = Math.floor((distance % (1000 * 60)) / 1000) + 's';

                    document.querySelector(".demo").innerHTML = days + hours + minutes + seconds;

                    if (distance < 0) {
                        clearInterval(x);
                        document.querySelector(".demo").innerHTML = "";
                    }
                }, 1000);
            }
        }
    }
</script>

<style lang="scss">
    .hellobarre {
        position: sticky;
        top: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        transition: all .5s;
        min-height: calc(2 * 0.875rem);
        height: 100%;

        &.closed {
            height: 0;
            min-height: inherit;

            p, span, a {
                font-size: 0rem;
            }
        }

        p, span, a {
            color: inherit;
            margin: 0;
            font-size: 0.875rem;
            line-height: 2;
            transition: all .5s;
        }

        p {
            max-width: 85%;
        }

        & > span {
            right: 1%;
            position: fixed;
            cursor: pointer;

            &:hover {
                opacity: .7;
            }
        }
    }
    .hellobarres {
        
    }
</style>