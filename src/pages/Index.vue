<template>
  <q-page>
    <BannerSection />
    <InterestSection />
    <TheorySection />
    <ProjectsSection />
  </q-page>
</template>

<script lang="ts">
import BannerSection from 'components/BannerSection.vue'
import ProjectsSection from 'components/ProjectsSection.vue';
import { defineComponent } from 'vue';
import InterestSection from 'components/InterestSection.vue';
import TheorySection from 'components/TheorySection.vue';

export default defineComponent({
  name: 'PageIndex',
  components: { TheorySection, InterestSection, ProjectsSection, BannerSection },

});
</script>
