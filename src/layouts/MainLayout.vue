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

        <q-toolbar-title> Quasar App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header>
          <div v-for="link in linksList" :key="link.title" v-bind="link">
            <q-item clickable @click="goTo(link.link), toggleLeftDrawer()">
              <q-item-section v-if="link.icon" avatar>
                <q-icon :name="link.icon" />
              </q-item-section>
              <q-item-section>
                <q-item-label>{{ link.title }}</q-item-label>
                <q-item-label caption>{{ link.caption }}</q-item-label>
              </q-item-section>
            </q-item>
          </div>
        </q-item-label>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const leftDrawerOpen = ref(false);

const goTo = (link) => {
  router.push({ path: link });
};

const linksList = [
  {
    title: "Home",
    caption: "Go to home page",
    icon: "home",
    link: "/",
  },
  {
    title: "Test1",
    caption: "Go to test1 page",
    icon: "shop",
    link: "test1",
  },
  {
    title: "Test2",
    caption: "Go to test2 page",
    icon: "settings",
    link: "test2",
  },
];

const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value;
};
</script>
