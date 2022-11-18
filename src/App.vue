<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <img
      src="@/assets/logo-no-background.svg"
      alt="logo"
      width="200"
      height="130"
      class="logo"
    />

    <div class="wrapper">
      <nav>
        <RouterLink to="/" class="nav-link"><p>home</p> </RouterLink>
        <RouterLink to="/about" class="nav-link"><p>about</p> </RouterLink>
      </nav>
    </div>
  </header>

  <div class="router-view">
    <RouterView />
  </div>
</template>

<style scoped>
.logo {
  display: block;
  margin: 0.5rem auto 0;
}

nav {
  width: 100%;
  font-size: 12px;
  display: flex;
  justify-content: center;
  margin: 0.6rem 0;
  gap: 1.3rem;
}
.nav-link {
  background-color: rgb(250, 248, 245);
  /* border: 2px solid #373bc8; */
  color: #373bc8;
  font-weight: 600;
  text-align: center;
  padding: 0.5rem 2rem;
  box-shadow: 4px 4px 0px #373bc8;
  transform: translate(-3px, -3px);
  transition: 0.4s;
}

.nav-link.router-link-exact-active {
  /* border: 2px solid #373bc8; */
  box-shadow: 0px 0px 0px #373bc8;
  transform: translate(0px, 0px);
}

.nav-link.router-link-active {
  /* border: 2px solid #373bc8; */
  transform: translate(0px, 0px);
  box-shadow: 0px 0px 0px #373bc8;
}

.router-view {
  padding: 2rem 1rem;
  height: 100%;
  display: flex;
  justify-content: center;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;
    padding: 1rem 0;
  }
}
</style>
