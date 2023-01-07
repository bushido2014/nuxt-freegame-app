<template>
  <section class="home-slide">
    <div class="swiper homeSwiper" ref="swiper">
      <div class="swiper-wrapper">
        <div
          v-for="homeslide in homeslides"
          class="swiper-slide animeslide-slide"
          v-bind:style="{
            'background-image': 'url(' + homeslide.imgSrc + ')',
          }"
        >
          <div class="container">
            <div class="slide-dext" data-animate="bottom">
              <h1>{{ homeslide.title }}</h1>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import homeslides from '../data/HomeSlide.json';
import Swiper from 'swiper/swiper-bundle.min';
import 'swiper/swiper-bundle.min.css';
export default {
  data() {
    return {
      homeslides,
    };
  },
  async mounted() {
    await this.$nextTick();
    new Swiper(this.$refs.swiper, {
      autoplay: {
        delay: 2600,
      },
      loop: true,
      speed: 2600,
      effect: 'fade',
    });
  },
};
</script>

<style scoped>
.homeSwiper .swiper-slide {
  position: relative;
  padding: 15px 0;
  min-height: 520px;
  background-size: cover;
  text-align: center;
}
.slide-dext {
  padding: 20px 40px;
  border-radius: 8px;
  background-color: #202238;
  opacity: 0.9;
  max-width: 550px;
  width: 100%;
  position: relative;
  text-align: center;
}
.homeSwiper h1 {
  font-size: 3.2rem;
  text-transform: uppercase;
}
.animeslide-slide {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}
.animeslide-slide.swiper-slide-active [data-animate] {
  opacity: 1;
  transform: none;
}

[data-animate] {
  opacity: 0;
  transition: all 0.8s ease-out;
}
[data-animate='bottom'] {
  transform: translate3d(0, 15px, 0);
}
@media only screen and (max-width: 992px) {
  .homeSwiper h1 {
    font-size: 2.6rem;
  }
  .slide-dext {
    padding-left: 15px;
    padding-right: 15px;
  }
}
</style>
