<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <header class="tengri-header">
    <div class="logo">
      <a href="index.html"><img class="img-logo" src="./assets/images/main_long.svg" alt=""></a>
    </div>
    <nav>
      <ul>
        <li><a href="index.html">Новости</a></li>
        <li><a href="#articles">Статьи</a></li>
        <li><a href="#future">Что будет с Казахстаном?</a></li>
      </ul>
    </nav>

  </header>
  <div class="whatsapp-button">
    <a href="https://api.whatsapp.com/send?phone=KZ&text=Подпишитесь%20на%20канал%20Tengrinews.kz%20в%20WhatsApp" target="_blank">Подписывайтесь на канал Tengrinews.kz в WhatsApp</a>
  </div>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
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
    margin-top: 1rem;
  }
}
</style>
