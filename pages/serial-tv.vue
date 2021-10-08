<template>
    <div class="app">
        <Nav />
        <Loading v-if="$fetchState.pending"/>
          <div v-else class="container movies">
            <div class="movies-grid">
              <div class="movie" 
                v-for="(serie, index) in series"
                :key="index">
                <div class="movie-img">
                  <img :src="`https://image.tmdb.org/t/p/w500/${serie.poster_path}`" alt="">
                  <p class="review"> {{ serie.vote_average }} </p>
                </div>
                <div class="info">
                  <p class="title"> 
                    {{ serie.name}}
                  </p>
                  <NuxtLink  class="button button-light" :to=" {name : 'series-serieid', params: {serieid: serie.id} } ">
                    Get More
                  </NuxtLink>
                </div>
              </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        data(){
            return{
                series: []
            }
        },
        async fetch(){
          await this.getSeries()
        },
        methods: {
            async getSeries(){
                const data = axios.get(                    
                    `https://api.themoviedb.org/3/tv/popular?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US`
                )
                const result = await data
                result.data.results.forEach((serie) => {
                  this.series.push(serie)
                })
                console.log(this.series)
            }
        }        
    }
</script>

<style lang="scss" scoped>
.movies {
    padding: 32px 16px;
    .movies-grid {
      display: grid;
      column-gap: 32px;
      row-gap: 64px;
      grid-template-columns: 1fr;
      @media (min-width: 500px) {
        grid-template-columns: repeat(2, 1fr);
      }
      @media (min-width: 750px) {
        grid-template-columns: repeat(2, 1fr);
      }
      @media (min-width: 1100px) {
        grid-template-columns: repeat(4, 1fr);
      }
      .movie {
        position: relative;
        display: flex;
        flex-direction: column;
        .movie-img {
          position: relative;
          overflow: hidden;
          img {
            display: block;
            width: 100%;
            height: 100%;
          }
          .review {
            position: absolute;
            top: 0;
            right: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 40px;
            height: 40px;
            background-color: #c92502;
            color: #fff;
            border-radius: 0 0 16px 0;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
              0 2px 4px -1px rgba(0, 0, 0, 0.06);
          }
        }
        .info {
          margin-top: auto;
          .title {
            margin-top: 8px;
            color: #fff;
            font-size: 20px;
          }
          .release {
            margin-top: 8px;
            color: #c9c9c9;
          }
          .button {
            margin-top: 8px;
          }
        }
      }
    }
  }
</style>