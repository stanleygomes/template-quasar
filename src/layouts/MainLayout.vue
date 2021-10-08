<template>
  <q-layout view="lHh Lpr lFf" class="bg-dark" >
    <q-header elevated  >
      <q-toolbar
      class="row items-center"
      :class="{'justify-between':$q.screen.lt.md, 'justify-center':$q.screen.gt.sm,}">

        <img
            src="../assets/quasar-logo-vertical.svg"
            alt="Logo o Gira"
            width="100"
            height="80" >
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          class="lt-md inline"
          @click="toggleRightDrawer"
        />
        <NavBar
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
          :path="link.path"
          class="gt-sm inline"
        />

        <q-separator color="gray" class="q-mx-lg gt-sm inline" inset vertical />

        <q-btn
          color="primary"
          text-color="white"
          class="gt-sm inline"
          label="Baixar carteira"
        />
      </q-toolbar>
    </q-header>

    <q-drawer
      side="right"
      v-model="rightDrawerOpen"
      show-if-above
      bordered
      class="full-width bg-dark lt-md inline"
    >
      <q-list>
        <q-item-label header>
          <div class="row items-center justify-between">
            <img
            src="../assets/quasar-logo-vertical.svg"
            alt="Logo o Gira"
            width="100"
            height="80" >

            <q-btn
              flat
              dense
              round
              icon="menu"
              color="primary"
              aria-label="Menu"
              class="lt-sm inline"
              @click="toggleRightDrawer"
            />
          </div>
        </q-item-label>

        <NavBar
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
          :path="link.path"
          :isMobile="true"
        />
        <q-separator color="gray" inset />
      </q-list>
      <div class="row q-ma-md items-center justify-between">
        <q-btn
          color="primary"
          text-color="white"
          class="q-mt-lg"
          label="Baixar carteira"
        />
      </div>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import NavBar from 'src/components/NavBar.vue';

const linksList = [
  {
    title: 'Home',
    link: '/',
  },
  {
    title: 'O Gira',
    link: '/o-gira',
  },
  {
    title: 'Nosso modelo',
    link: '/nosso-modelo',
  },
  {
    title: 'Perguntas frequentes',
    link: '/perguntas-frequentes',
  },
];

import { defineComponent, ref } from 'vue';
import { useQuasar } from 'quasar';

export default defineComponent({
  name: 'MainLayout',

  components: {
    NavBar,
  },

  setup() {
    const rightDrawerOpen = ref(false);
    const $q = useQuasar();

    return {
      $q,
      linksList,
      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value;
      },
    };
  },
});
</script>

<style>
.q-drawer {
  width: 100% !important;
}
</style>
