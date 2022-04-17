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
          Almalinux Errata and List
        </q-toolbar-title>

        <div>Almalinux Errata v{{ version }}</div>
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
          Essential Links
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
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import {version} from '../../package.json'

const linksList = [
  {
    title: 'Home',
    caption: 'almalinux.org',
    icon: 'school',
    link: 'https://almalinux.org'
  },
  {
    title: 'Github',
    caption: 'github.com/almalinux',
    icon: 'code',
    link: 'https://github.com/almalinux'
  },
  {
    title: 'Chat Channel',
    caption: 'chat.almalinux.org',
    icon: 'chat',
    link: 'https://chat.almalinux.org'
  },
  {
    title: 'Forum',
    caption: 'forums.almalinux.org',
    icon: 'record_voice_over',
    link: 'https://forums.almalinux.org/'
  },
  // {
  //   title: 'Twitter',
  //   caption: '@almalinux',
  //   icon: 'rss_feed',
  //   link: 'https://twitter.almalinux.org'
  // },
  // {
  //   title: 'Facebook',
  //   caption: '@AlmaLinux',
  //   icon: 'public',
  //   link: 'https://facebook.almalinux.org'
  // },
  {
    title: 'Almalinux Wiki',
    caption: 'Community Wiki site',
    icon: 'favorite',
    link: 'https://wiki.almalinux.org'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
