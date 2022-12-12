<script setup lang="ts">
import { RouterLink } from "vue-router";
</script>

<template>
  <header>
    <nav class="navigation">
      <img
        src="@/assets/logo-no-background.svg"
        alt="logo"
        width="200"
        height="130"
        class="logo"
      />
      <div class="nav-links">
        <RouterLink to="/" class="nav-link"><p>home</p> </RouterLink>
        <RouterLink to="/about" class="nav-link"><p>about</p> </RouterLink>
      </div>
    </nav>
  </header>
</template>

<style scoped>
nav {
  width: 100%;
  height: fit-content;
  position: fixed;
  padding: 0rem 1rem;
  top: 0;
  left: 0;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  flex-wrap: wrap;
  background-color: rgba(250, 248, 245, 0.6);
}
.logo {
  display: block;
  margin: 0.5rem 0;
}
.nav-links {
  font-size: 12px;
  display: flex;
  justify-content: center;
  margin: 0.6rem 0;
  gap: 1.3rem;
}
.nav-link {
  background-color: rgb(250, 248, 245);
  color: #373bc8;
  font-weight: 600;
  text-align: center;
  padding: 0.5rem 2rem;
  box-shadow: 4px 4px 0px #373bc8;
  transform: translate(-3px, -3px);
  transition: 0.4s;
}

.nav-link.router-link-exact-active {
  box-shadow: 0px 0px 0px #373bc8;
  transform: translate(0px, 0px);
}

.nav-link.router-link-active {
  /* border: 2px solid #373bc8; */
  transform: translate(0px, 0px);
  box-shadow: 0px 0px 0px #373bc8;
}

@media (min-width: 1024px) {
  .logo {
    margin: 0 2rem 0;
  }
  nav {
    font-size: 1rem;
    padding: 1rem 0;
  }
}
@media (min-width: 400px) {
  nav {
    justify-content: center;
  }
}
</style>
