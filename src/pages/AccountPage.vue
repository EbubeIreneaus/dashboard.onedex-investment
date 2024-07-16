<script setup lang="tsx">
import { reactive, ref } from 'vue';

const user = reactive({
  fullname: 'Okigwe Ebube Ireneaus',
  email: 'alfredebube7@gmail.com',
  psw: '',
});
const confirm = ref('')
</script>
<template>
  <div class="full-width full-height row items-center q-py-xl q-px-md">
    <div class="full-width" style="max-width: 768px">
      <q-form autocorrect="off" spellcheck="false">
        <fieldset class="q-pa-lg q-mb-lg">
          <legend>Personal</legend>
          <q-input
          outlined
          v-model="user.fullname"
          dark
          color="white"
          label="Fullname"
          label-color="positive"
          class="q-mb-md"
        />
        <q-input
          outlined
          v-model="user.email"
          dark
          color="white"
          label="Email Address"
          label-color="positive"
          class="q-mb-md"
          readonly
        />
        </fieldset>
        <fieldset class="q-pa-lg">
          <legend>Password</legend>
          <q-input label="Password" type="password" label-color="positive" outlined dark color="white" v-model="user.psw" class="q-mb-md" />
          <q-input label="Confirm" type="password" label-color="positive" outlined dark color="white" v-model="confirm" class="q-mb-md" />
          <q-btn color="positive" >save password</q-btn>
        </fieldset>
      </q-form>
    </div>
  </div>
</template>
