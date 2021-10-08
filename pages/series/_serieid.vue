<template>
    <div class="app">
        <Nav />
        <Loading v-if="$fetchState.pending" />
        <div v-else class="container single-serie">
            <div class="serie-info">
                <div class="serie-img">
                    <img :src="`https://image.tmdb.org/t/p/w500/${serie.poster_path}`" alt="">
                </div>
            <div class="serie-content">
                <h1> {{ serie.name }} </h1>
                <p class="serie-fact tagline">
                    <span>Genre: {{ serie.genres[0].name }} </span>
                </p>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: 'single-serie',
        data(){
            return{
                serie: null
            }
        },
        async fetch(){
            await this.getSerieId()
        },
        fetchDelay: 1000,
        methods: {
            async getSerieId(){
                const data = axios.get(
                    `https://api.themoviedb.org/3/tv/${this.$route.params.serieid}?api_key=dc2672f87bc9009fa52d09cdc876c282&language=en-US`
                )
                const result = await data
                this.serie = result.data
            }
        }
    }
</script>

<style lang="scss" scoped>
    .single-serie{
        color: #fff;
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding: 32px 16px;

        .serie-info{
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 32px;
            color: #fff;
            @media (min-width: 800px) {
            flex-direction: row;
            align-items: flex-start;
        }
        .serie-img{
            img {
                max-height: 500px;
                width: 100%;
                @media (min-width: 800px) {
                max-height: 600px;
                width: initial;
                }
            }
        }
        .serie-content {
            h1 {
                font-size: 56px;
                font-weight: 400;
            }
            .serie-fact {
                margin-top: 12px;
                font-size: 20px;
                line-height: 1.5;
                span {
                font-weight: 600;
                text-decoration: underline;
                }
            }
            .tagline {
                font-style: italic;
                span {
                font-style: normal;
                }
            }
      }
    }
}
</style>