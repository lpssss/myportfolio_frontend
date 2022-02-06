<template>
  <q-layout id='login-layout' view='hhh lpR fff'>
        <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'LoginLayout'
});
</script>

<style scoped lang='scss'>
#login-layout{
  background-color: #EEEDE7;
}
</style>
