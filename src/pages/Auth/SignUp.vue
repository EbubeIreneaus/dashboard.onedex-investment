<script setup lang="tsx">
import { reactive } from 'vue';

const formRegister = reactive({
  fullname: '',
  email: '',
  password: '',
});

const formLogin = reactive({
  Remember: false,
  email: '',
  password: '',
});
</script>

<template>
  <div class="q-py-md-sm q-py-lg q-px-md-xl bg-primary row items-center" style="min-height:100dvh">
    <div class="row q-col-gutter-x-lg q-col-gutter-y-xl items-center  text-white q-mx-md-auto  q-px-md-xl q-px-lg full-width" style="max-width: 1228px">
      <div class="col-md col-12">
        <div class="text-h4 q-mb-md">Login</div>
        <q-form>
          <q-input
            outlined
            v-model="formRegister.email"
            type="email"
            label="Email"
            class="q-mb-md text-white"
            label-color="positive"
            dark
          />
          <q-input
            outlined
            v-model="formRegister.password"
            type="password"
            label="Email"
            class="q-mb-md"
            label-color="positive"
            dark
          />
          <q-checkbox
            class=""
            label="Remember me"
            v-model="formLogin.Remember"
             checked-icon="task_alt"
            unchecked-icon="highlight_off"
            color="positive"
            keep-color
          ></q-checkbox>
          <q-btn rounded class="q-px-xl block q-my-md" color="positive">submit</q-btn>
          <div class="h6"><router-link to="">Forgot your password?</router-link></div>
        </q-form>
      </div>
      <div class="col-md col-12">
        <div class="text-h4 q-mb-md">Register</div>
        <q-form>
          <q-input
            outlined
            v-model="formRegister.fullname"
            label="Fullname"
            class="q-mb-md"
            label-color="positive"
            dark
          />
          <q-input
            outlined
            v-model="formRegister.email"
            type="email"
            label="Email"
            class="q-mb-md"
            label-color="positive"
            dark
          />
          <q-input
            outlined
            v-model="formRegister.password"
            type="password"
            label="Password"
            class="q-mb-md"
            label-color="positive"
            dark
          />
          <div class="q-py-md text-body1 text-weight-medium">
            Your personal data will be used to support your experience
            throughout this website, to manage access to your account, and for
            other purposes described in our privacy policy.
          </div>
          <q-btn rounded class="q-px-xl" color="positive">submit</q-btn>
        </q-form>
      </div>
    </div>
  </div>
</template>
