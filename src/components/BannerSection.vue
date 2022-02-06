<template>
  <q-banner class='bg-secondary text-black'>
    <div class='text-center'>
      <div class='text-h1 text-weight-medium'>
        Hello,
      </div>
      <div class='q-pa-md text-h6'>
        Welcome to my website.
        <br> This website serves to showcase my interests, knowledge base and projects.
        <br> More features and design coming soon.
      </div>
    </div>
    <div class='q-pa-sm text-center'>
      <div class='text-h6'>My Social Media</div>
      <div>
        <q-btn flat icon='fab fa-linkedin fa-2x' round :href='linkedin' target="_blank" />
        <q-btn flat icon='fab fa-github fa-2x' round :href='github' target="_blank" />
        <q-btn flat icon='fab fa-facebook fa-2x' round :href='facebook' target="_blank" />
        <q-btn flat icon='fab fa-instagram fa-2x' round :href='instagram' target="_blank" />
      </div>
    </div>
  </q-banner>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';
import { SOCIALMEDIA_LINKS } from 'components/social-media';

export default defineComponent({
  name: 'BannerSection',
  setup(){
    const {linkedin,github,facebook,instagram}=SOCIALMEDIA_LINKS
    console.log(linkedin)
    return{
      linkedin,
      github,
      facebook,
      instagram
    }
  }
});
</script>

<style scoped>
</style>
