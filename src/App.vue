<script>
import Navbar from "./components/NavBar.vue";

export default {
  components: {
    Navbar,
  },
  data() {
    return {
      navbarItems: [
        { label: "Home", link: "#" },
        { label: "About", link: "#about" },
        { label: "Services", link: "#services" },
        { label: "Contact", link: "#contact" },
      ],
    };
  },
};
</script>

<template>
  <div class="container">
    <Navbar :items="navbarItems" logoSrc="./src/assets/vue.svg" />
  </div>
</template>

<style scoped></style>
