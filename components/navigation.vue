<template>
  <div>
    <div class="nav">
      <div class="link"><NuxtLink to="/">Главная страница</NuxtLink></div>
      <div class="link"><NuxtLink to="/about">О нас</NuxtLink></div>
      <div class="link"><NuxtLink to="/articles">Доска объявлений</NuxtLink></div>
    </div>
  </div>
</template>

<style>
.nav {
  display: flex;
  flex-direction: column;
  height: 150px;
  width: 200px;
}
.link {
  background-color: black;
  border-radius: 15px;
  margin: 7px;
  padding: 5px;
  text-align: center;

}

a {
  text-decoration: none;
  color: white;
}
a.nuxt-link-exact-active {
  color: coral;
}

</style>
