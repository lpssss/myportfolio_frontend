<template>
  <q-page>
    <BannerSection />
    <InterestSection admin />
    <TheorySection />
    <ProjectsSection />
  </q-page>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';
import BannerSection from 'components/BannerSection.vue';
import InterestSection from 'components/InterestSection.vue';
import TheorySection from 'components/TheorySection.vue';
import ProjectsSection from 'components/ProjectsSection.vue';
export default defineComponent({
  name: 'AdminIndex',
  components: { ProjectsSection, TheorySection, InterestSection, BannerSection }
});
</script>

<style scoped>

</style>
