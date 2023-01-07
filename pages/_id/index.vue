<template>
  <section class="single-game">
    <div class="container">
      <div class="back-home">
        <NuxtLink class="button" :to="{ name: 'index' }"> Back </NuxtLink>
      </div>
      <h2>{{ game.title }}</h2>
      <div class="game-description flex">
        <div class="game-gallery">
          <div class="swiper singleSwiper" ref="swiper">
            <div class="swiper-wrapper">
              <div
                v-for="screenshot in game.screenshots"
                :key="screenshot.id"
                class="swiper-slide screenshot-swiper"
              >
                <img :src="screenshot.image" alt="" class="screenshot" />
              </div>
            </div>
          </div>
        </div>
        <div class="game-details">
          <h4>Additional Information</h4>
          <div class="flex game-details__list">
            <ul>
              <li>
                Platform: <span>{{ game.platform }}</span>
              </li>
              <li>
                Developer:<span>{{ game.developer }}</span>
              </li>
              <li>
                Genre:<span>{{ game.genre }}</span>
              </li>
              <li>
                Release Date:<span>{{ game.release_date }}</span>
              </li>
            </ul>

            <ul>
              <li v-for="minimum in game.minimum_system_requirements">
                {{ minimum }}
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="game-text">
        <p>{{ game.description }}</p>
      </div>
    </div>
  </section>
</template>

<script>
import Swiper from 'swiper/swiper-bundle.min';
import 'swiper/swiper-bundle.min.css';
export default {
  async asyncData({ $axios, params }) {
    const config = {
      'x-rapidapi-key': '8c225fdb62mshce8bc529a49bbadp1d87c7jsn82460f41d425',
      'x-rapidapi-host': 'free-to-play-games-database.p.rapidapi.com',
    };
    const result = await $axios.get(
      'https://free-to-play-games-database.p.rapidapi.com/api/game',
      {
        params: { id: params.id },
        headers: config,
      }
    );
    return {
      game: result.data,
    };
  },

  async mounted() {
    await this.$nextTick();
    new Swiper(this.$refs.swiper, {
      autoplay: {
        delay: 2000,
      },

      loop: true,
      speed: 1800,
    });
  },
  head() {
    return {
      title: this.game.title,
    };
  },
};
</script>
