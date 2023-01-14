<template>
  <section class="single-game">
    <div>
      <loader v-show="loader"></loader>
    </div>
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
          </div>
        </div>
      </div>
      <div class="system" v-if="game.minimum_system_requirements">
        <h4>Minimum System Requirements</h4>
        <div class="flex">
          <div class="system-item">
            <div>
              <p class="system-item__title">Operational System - SO</p>
              <p>{{ game.minimum_system_requirements.os }}</p>
            </div>
            <div>
              <p class="system-item__title">Processor</p>
              <p>{{ game.minimum_system_requirements.processor }}</p>
            </div>
            <div>
              <p class="system-item__title">Memory</p>
              <p>{{ game.minimum_system_requirements.memory }}</p>
            </div>
          </div>
          <div class="system-item">
            <div>
              <p class="system-item__title">Storage</p>
              <p>{{ game.minimum_system_requirements.storage }}</p>
            </div>
            <div>
              <p class="system-item__title">Graphics card</p>
              <p>{{ game.minimum_system_requirements.graphics }}</p>
            </div>
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
import Loader from '~/components/loader/loader.vue';
import Swiper from 'swiper/swiper-bundle.min';
import 'swiper/swiper-bundle.min.css';
export default {
  data() {
    return {
      loader: true,
    };
  },
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
    }),
      setTimeout(() => {
        this.loader = false;
      }, 1800);
  },

  head() {
    return {
      title: this.game.title,
    };
  },
};
</script>
