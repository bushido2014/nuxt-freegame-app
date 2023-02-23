<template>
  <div>
    <HomeSlide />

    <section class="home">
      <div class="container">
        <div class="search-bar">
          <input
            v-model="searchTerm"
            type="text"
            placeholder="Search games..."
            class="search-input"
          />
        </div>
        <div class="game-wrapper grid">
          <div
            class="card"
            v-for="game in filteredGames.slice(0, 42)"
            :key="game.id"
          >
            <div
              class="card-header"
              v-bind:style="{
                'background-image': 'url(' + game.thumbnail + ')',
              }"
            ></div>
            <div class="card-body">
              <h5>{{ game.title }}</h5>
              <div class="card-text">{{ game.short_description }}</div>
              <div class="stands flex">
                <span class="option">
                  {{ game.platform }}
                </span>
                <span class="category">{{ game.genre }}</span>
              </div>
              <div class="card-footer">
                <NuxtLink :to="`/${game.id}`" class="button">
                  Read More
                </NuxtLink>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import HomeSlide from '~/components/HomeSlide';

export default {
  components: {
    HomeSlide,
  },
  data() {
    return {
      urlGame: 'https://free-to-play-games-database.p.rapidapi.com/api/games',
      apiKey: '8c225fdb62mshce8bc529a49bbadp1d87c7jsn82460f41d425',
      rHost: 'free-to-play-games-database.p.rapidapi.com',
      games: [],
      searchTerm: '',
    };
  },

  mounted() {
    this.loadFetch();
  },

  computed: {
    filteredGames() {
      return this.games.filter((game) => {
        const title = game.title.toLowerCase();
        const desc = game.short_description.toLowerCase();
        const term = this.searchTerm.toLowerCase();

        return title.includes(term) || desc.includes(term);
      });
    },
  },

  methods: {
    async loadFetch() {
      const games = await this.$axios
        .$get(this.urlGame, {
          headers: {
            'X-RapidAPI-Key': this.apiKey,
            'X-RapidAPI-Host': this.rHost,
          },
        })
        .then((games) => {
          this.games = games;
        });
    },
  },

  head: {
    bodyAttrs: {
      class: 'home-page',
    },
  },
};
</script>
