<template>
 <q-layout view="hHh Lpr lff">

    <q-header reveal elevated class="bg-secondary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu"  v-if="login" @click="drawer  = !drawer " />

        <q-toolbar-title>
         Marco Marson
        </q-toolbar-title>
         
          <q-btn flat round dense icon="person" class="q-mr-xs" />
          <q-btn flat round dense icon="settings" />
      </q-toolbar>
    </q-header>

    <q-drawer v-model="drawer " :width="200"
        :breakpoint="500" side="left" >
      <!-- drawer content -->
      <q-scroll-area class="fit">
          <q-list v-for="(menuItem, index) in menuList" :key="index">

            <q-item @click="drawer  = !drawer " clickable :active="menuItem.label === 'Outbox'" v-bind:to="menuItem.link" v-ripple>
              <q-item-section avatar>
                <q-icon :name="menuItem.icon" />
              </q-item-section>
              <q-item-section>
                {{ menuItem.label }}
              </q-item-section>
            </q-item>

           <q-separator v-if="menuItem.separator" />

          </q-list>
        </q-scroll-area>
    </q-drawer>

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
   data () {
    return {
      drawer: false,
      login:false,
      menuList:[ {
          icon: 'home',
          label: 'Home',
          separator: true,
          link:"/"
        },
        {
          icon: 'watch_later',
          label: 'Mangas',
          separator: false,
           link:"/manga"
        },
        {
          icon: 'add',
          label: 'Insert Manga',
          separator: false,
          link:"/insertManga"
        },
      ]
    }
  },
   components: {
      FadeTransition
    }
}
</script>
<style lang="scss">
</style>
