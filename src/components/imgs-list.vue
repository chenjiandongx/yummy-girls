<template>
    <div class="container"
         v-infinite-scroll="loadMore"
         infinite-scroll-distance="600"
         infinite-scroll-throttle-delay="100"
         infinite-scroll-disabled="busy"
         :items="items">
        <div class="waterfall">
            <div class="img-cell" v-for="item in items">
                <img :src="item.imgSrc"/>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: 'App',
        data () {
            return {
                items: []
            }
        },
        created() {
            this.fetchJson();
        },
        methods: {
            loadMore() {
                try {
                    for (let i = 0; i < 6; i++) {
                        this.items.push(window.__INITIAL_STATE__[~~(Math.random() * 1000) + 1])
                    }
                } catch (e) {
                }
            },
            fetchJson() {
                axios.get("https://raw.githubusercontent.com/chenjiandongx/mmjpg/master/yummy.json")
                    .then(response => {
                        window.__INITIAL_STATE__ = response.data;
                        this.loadMore();
                    }).catch(error => {
                })
            }
        }
    }
</script>

<style>
    body {
        padding: 12px 0 0 0;
        margin: 0;
        height: 100%;
        width: 100%;
        background-color: #f6f6f6;
    }

    .container {
        width: 96%;
        margin: 0 auto;
    }

    .waterfall {
        -moz-column-count: 3;
        -webkit-column-count: 3;
        column-count: 3;
        -moz-column-width: 24em;
        -webkit-column-width: 24em;
        column-width: 24em;
        -moz-column-gap: 1em;
        -webkit-column-gap: 1em;
        column-gap: 1em;
    }

    .img-cell {
        padding: 0.75em;
        -webkit-column-break-inside: avoid;
        break-inside: avoid;
        background: white;
        border-bottom: 2px solid #eee;
        transition: all .3s;
    }

    .img-cell:hover {
        transform: translateY(-3px);
        box-shadow: 1px 1px 20px #999;
    }

    .img-cell img {
        width: 100%;
    }
</style>
