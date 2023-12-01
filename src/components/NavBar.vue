<!-- Navbar.vue -->

<template>
  <nav>
    <div class="logo">
      <img :src="logoSrc" alt="Logo" />
    </div>
    <button v-if="shouldShowMenuButton" class="menu-toggle" @click="toggleMenu">
      &#9776;
    </button>
    <ul :class="{ 'nav-links': true, show: isMenuOpen }">
      <li v-for="(item, index) in items" :key="index">
        <a :href="item.link" @click="closeMenu">{{ item.label }}</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    logoSrc: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isMenuOpen: false,
      shouldShowMenuButton: false,
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    closeMenu() {
      this.isMenuOpen = false;
    },
    checkScreenWidth() {
      this.shouldShowMenuButton = window.innerWidth <= 768;
    },
  },
  mounted() {
    // Check screen width on component mount
    this.checkScreenWidth();

    // Listen for window resize events to update shouldShowMenuButton
    window.addEventListener("resize", this.checkScreenWidth);
  },
  beforeDestroy() {
    // Remove the resize event listener when the component is destroyed
    window.removeEventListener("resize", this.checkScreenWidth);
  },
};
</script>

<style scoped>
/* Add your styling here */
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #333;
  color: white;
  padding: 10px;
}

.logo img {
  max-width: 100px; /* Adjust the max-width as needed */
}

.menu-toggle {
  display: none; /* Initially hide the menu button */
  background: none;
  border: none;
  color: white;
  font-size: 1.5em;
  cursor: pointer;
}

.nav-links {
  list-style-type: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.nav-links li {
  margin-right: 10px;
}

.nav-links a {
  color: white;
  text-decoration: none;
}

/* Responsive styles */
@media (max-width: 768px) {
  .nav-links {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 60px;
    left: 0;
    background-color: #333;
    width: 100%;
    padding: 10px;
    box-sizing: border-box;
  }

  .nav-links.show {
    display: flex;
  }

  .nav-links li {
    margin-right: 0;
    margin-bottom: 10px;
  }

  .menu-toggle {
    display: block; /* Show the menu button when the width is 768px or less */
  }
}
</style>
