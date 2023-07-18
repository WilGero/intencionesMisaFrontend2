<template>
       <b-card title="Card Title" no-body>
    <b-card-header header-tag="nav">
      <b-nav card-header tabs>
        <!-- <b-nav-item>'s with child routes. Note the trailing slash on the first <b-nav-item> -->
        <b-nav-item :to="{name:'inicio'}" exact exact-active-class="active">Inicio</b-nav-item>
        <b-nav-item to="/misas" exact exact-active-class="active">Misas</b-nav-item>
        <b-nav-item to="/reginten" exact exact-active-class="active">Registrar Intencion</b-nav-item>
        <b-nav-item to="/about" exact exact-active-class="active">Acerca de...</b-nav-item>
      </b-nav>
    </b-card-header>

    <b-card-body>
      <!-- Child route gets rendered in <router-view> or <nuxt-child> -->
      <router-view></router-view>
        <!-- Or if using Nuxt.js
      <nuxt-child></nuxt-child>
      -->
    </b-card-body>
  </b-card>
</template>

<script>
export default{
    name:'MenuComponent'
}
</script>