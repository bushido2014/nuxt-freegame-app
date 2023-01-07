<template>
  <header class="header" :class="{ sticky_header: active }">
    <div class="container flex">
      <div class="logo">
        <nuxt-link to="/">
          <img src="https://i.postimg.cc/Y28kwxgp/freetogame-logo.png"
        /></nuxt-link>
      </div>
      <nav>
        <ul class="flex">
          <li>
            <nuxt-link to="/"> Home</nuxt-link>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>
<script>
export default {
  data() {
    return {
      active: false,
    };
  },
  mounted() {
    window.document.onscroll = () => {
      let navBar = document.querySelector('header');
      if (window.scrollY > navBar.offsetTop) {
        this.active = true;
      } else {
        this.active = false;
      }
    };
  },
};
</script>
