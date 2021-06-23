<template>
  <div class="m-auto p-3 max-w-screen-xl">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/selection">Terminauswahl</router-link> |
      <router-link to="/overview">Terminübersicht</router-link>
    </div>
    <h1 class="text-greenSheen text-2xl py-5">
      VRS Masterarbeitsstudie Joelle
    </h1>
    <router-view />
  </div>
</template>

