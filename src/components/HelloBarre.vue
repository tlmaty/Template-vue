<template>
    <div class="hellobarre" :style="{ background: this.background, color: this.color }">
        <p>{{ content }} <a href="#">{{ contentLink }}</a>{{ countDown }}</p>
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
        ],
        mounted() {
            let helloBarre = document.querySelector('.hellobarre');
            let closeBtn = document.querySelector('.hellobarre > span');
            closeBtn.addEventListener('click', () => {
                helloBarre.classList.add('closed');
            });
        },
    }
</script>

<style lang="scss">
    .hellobarre {
        //background: #00395d; 
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

        span {
            right: 1%;
            position: fixed;
            cursor: pointer;

            &:hover {
                opacity: .7;
            }
        }
    }
</style>