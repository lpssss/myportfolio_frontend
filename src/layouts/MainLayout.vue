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
        <span>Copyright <q-icon name="copyright" /> 2022. All rights reserved.</span>
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
