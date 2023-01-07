<template>
  <div>
    <Header />
    <Nuxt />
    <Footer />
    <div class="back">
      <BackToTop />
    </div>
  </div>
</template>
<script>
import Header from '~/components/Header';
import Footer from '~/components/Footer';
import BackToTop from '~/components/BackToTop.vue';
export default {
  components: {
    Header,
    Footer,
    BackToTop,
  },
  head() {
    return {
      title: 'Free-To-Play Games Database API',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Home page description',
        },
      ],
    };
  },
};
</script>
