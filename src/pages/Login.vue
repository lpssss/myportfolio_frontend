<template>
  <q-page>
    <q-card class='absolute-center login-card'>
      <q-card-section>
        <div class='text-h6 text-center'>Login</div>
      </q-card-section>

      <q-separator />
      <q-card-section>
        <q-form
          class='q-gutter-md'
          @reset='onReset'
          @submit='onSubmit'
        >
          <q-input
            v-model='username'
            :rules="[ val => val && val.length > 0 || 'Please type something']"
            filled
            label='Username'
            lazy-rules
          />

          <q-input
            v-model='password'
            :rules="[ val => val && val.length > 6 || 'Password length greater than 6']"
            filled
            label='Password'
            lazy-rules
          />

          <div class='text-center'>
            <q-btn color='primary' label='Login' type='submit' />
          </div>
        </q-form>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Login'
});
</script>

<style scoped lang='scss'>
.login-card{
  width:100%;
  max-width: 300px;
}
</style>
