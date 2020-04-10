<template>
 <q-layout view="hHh lpR fFf">

    <q-header reveal elevated class="bg-primary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="left = !left" />

        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo/svg/quasar-logo.svg">
          </q-avatar>
          Marco Marson Dashboard
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="left" side="left" elevated>
      <!-- drawer content -->
    </q-drawer>

    <q-page-container>
      <fade-transition :duration="100" mode="out-in">
        <router-view />
      </fade-transition>
    </q-page-container>

    <q-footer reveal elevated class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo/svg/quasar-logo.svg">
          </q-avatar>
          Title
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
import {FadeTransition} from 'vue2-transitions';

export default {
  name: 'MainLayout',
   data () {
    return {
      left: false
    }
  },
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
