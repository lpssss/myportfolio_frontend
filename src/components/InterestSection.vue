<template>
  <div class='q-pa-md row items-start q-gutter-md' v-if='interest.length'>
    <q-card class='my-card'>
      <q-card-section>
        <div class='text-h6'>Background & Interest</div>
        <div class='q-px-md q-pt-sm'>{{interest}}</div>
      </q-card-section>

      <q-card-section v-if='admin'>
        <!--        TODO: add functionality for admin-->
        Pending
      </q-card-section>
    </q-card>
  </div>
</template>

<script lang='ts'>
import { api } from 'boot/axios';
import { ApiLinks } from 'src/api-links';
import { defineComponent, ref } from 'vue';
import { AxiosResponse } from 'axios';

const API_LINK: string = ApiLinks.Interest;
export default defineComponent({
  name: 'InterestSection',
  props: {
    admin: {
      type: Boolean
    }
  },
  setup() {
    //TODO: may need to change server response data structure
    interface Interest {
      id: string;
      interest: string;
    }

    const interest = ref('');

    async function getInterestData() {
      try {
        const response: AxiosResponse<Interest[]> = await api.get(API_LINK);
        interest.value = response.data[0].interest;
      } catch (error) {
        console.log(error);
      }
    }

    void getInterestData();

    return {
      interest
    };
  }
});
</script>

<style lang='scss' scoped>
.my-card {
  width: 100%
}
</style>
