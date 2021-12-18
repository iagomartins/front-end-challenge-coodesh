<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          Desafio Coodesh
        </q-toolbar-title>

        <div>Feito com Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Navegação
        </q-item-label>

        <RouteLink
          v-for="link in routeLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
      <q-separator class="q-my-md"></q-separator>
      <q-list>
        <q-item-label
          header
        >
          Links Externos
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'
import RouteLink from 'components/RouteLink.vue'

const routesList = [
  {
    title: 'Home',
    caption: 'Página inicial',
    icon: 'home',
    link: '/'
  },
  {
    title: 'Pacientes',
    caption: 'Lista de pacientes',
    icon: 'person',
    link: '/patients'
  },
];

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/iagomartins',
    icon: 'code',
    link: 'https://github.com/iagomartins'
  },
  {
    title: 'Twitter',
    caption: '@iaamartins',
    icon: 'rss_feed',
    link: 'https://twitter.com/iaamartins'
  },
  {
    title: 'Facebook',
    caption: '@jack.angster',
    icon: 'public',
    link: 'https://www.facebook.com/jack.angster/'
  },
  {
    title: 'Linkedin',
    caption: 'Perfil Linkedin',
    icon: 'link',
    link: 'https://www.linkedin.com/in/iago-martins-711575155/'
  }
];

import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
    RouteLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      routeLinks: routesList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
