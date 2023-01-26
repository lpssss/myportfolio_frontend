<template>
  <q-layout view='hhh lpR fff'>

    <q-header class='bg-secondary text-black'>
      <q-toolbar>
        <q-toolbar-title>
          <span id='app-title'>Poh Seng's Portfolio</span>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-footer id="footer" class='bg-secondary text-black'>
      <div class='q-pa-sm text-center'>
        <span>Copyright <q-icon name="copyright" /> 2023. All rights reserved. Powered By Vercel, ASP.NET, Docker, Nginx</span>
      </div>
    </q-footer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script lang='ts'>

import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MainLayout',
});
</script>

<style lang='scss' scoped>
#app-title {
  font-family: 'Yellowtail', cursive;
  font-size: 1.5rem;
}
</style>
