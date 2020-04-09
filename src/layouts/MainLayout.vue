<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>

        <q-toolbar-title>
          Hi Technologies DashBoard
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <fade-transition :duration="100" mode="out-in">
        <router-view />
      </fade-transition>
    </q-page-container>
  </q-layout>
</template>

<script>
import {FadeTransition} from 'vue2-transitions';

export default {
  name: 'MainLayout',
   components: {
      FadeTransition
    }
}
</script>
<style lang="scss">
.q-page-container{
  position: relative;
    float: right;
    width: 100%;
    min-height: 100vh;
    //border-top: 2px solid $primary;
    background: linear-gradient(#1e1e2f, #1e1e24);
}
.q-toolbar{
  padding: 10px 30px 10px 15px;
  width: 100%;
  z-index: 1050;
  background: #1a1e34;

}
</style>
