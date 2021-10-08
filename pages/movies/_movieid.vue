<template>
    <div class="app">
    <Nav />
    <Loading v-if="$fetchState.pending" />
    <div v-else class="container single-movie">
        <div class="movie-info">
          <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
            </div>
            <div class="movie-content">
                <h1>{{ movie.title }} </h1>
                <p class="movie-fact tagline">
                    <span>Genre: {{ movie.genres[0].name }}, {{ movie.genres[1].name }} </span>
                </p>
                <span>Overview: {{ movie.overview }} </span>
            </div>
        </div>
    </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: 'single-movie',
        data()
        {
            return{
                movie: null
            }
        },
        async fetch(){
            await this.getMovieId()
        },
        fetchDelay: 1000,
        methods: {
            async getMovieId(){
                const data = axios.get(
                    `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=dc2672f87bc9009fa52d09cdc876c282&language=en-US`
                    )
                    const result = await data
                    this.movie = result.data
            }
        }
    }
</script>

<style lang="scss" scoped>
.single-movie {
  color: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 32px 16px;
  .button {
    align-self: flex-start;
    margin-bottom: 32px;
  }
  .movie-info {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 32px;
    color: #fff;
    @media (min-width: 800px) {
      flex-direction: row;
      align-items: flex-start;
    }
    .movie-img {
      img {
        max-height: 500px;
        width: 100%;
        @media (min-width: 800px) {
          max-height: 700px;
          width: initial;
        }
      }
    }
    .movie-content {
      h1 {
        font-size: 56px;
        font-weight: 400;
      }
      .movie-fact {
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