<script setup lang="ts">
import { defineAsyncComponent, reactive, ref } from 'vue';
import { useQuasar } from 'quasar';
import { useRouter } from 'vue-router';
const EmailVerificationComponent = defineAsyncComponent(
  () => import('components/Auth/EmailVerification.vue')
);
const $q = useQuasar();
const isRegistering = ref(false);
const isLoggingin = ref(false);
const showEmailVerificationDialog = ref(false);
const router = useRouter()
// const isLoggingIn = ref(false)

function notify(
  status: 'error' | 'success',
  msg: string,
  caption: string | undefined
) {
  $q.notify({
    message: msg,
    caption: caption,
    icon: status == 'error' ? 'error' : 'task_alt',
    color: status == 'error' ? 'negative' : 'success',
  });
}


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

async function Register() {
  isRegistering.value = true;

  try {
    const req = await fetch('http://127.0.0.1:8000/api/auth/signup', {
      method: 'post',
      body: JSON.stringify(formRegister),
    });

    if (!req.ok) {
      // if request is not okay
      isRegistering.value = false;
      return false;
    }

    const res = await req.json();

    if (res.status != 'success') {
      isRegistering.value = false;
      notify('error', 'Server Error', res.msg);
    }

    $q.cookies.set('userId', res.userId);
    isRegistering.value = false;
    showEmailVerificationDialog.value = true
  } catch (error) {
    isRegistering.value = false;
    console.log(error);
  }
}


async function Login() {
  isLoggingin.value = true;

  try {
    const req = await fetch('http://127.0.0.1:8000/api/auth/signin', {
      method: 'post',
      body: JSON.stringify(formLogin),
    });

    if (!req.ok) {
      // if request is not okay
      isLoggingin.value = false;
      return false;
    }

    const res = await req.json();
    if (res.status == 'unverified') {
      $q.cookies.set('userId', res.userId);
      isLoggingin.value = false;
      return showEmailVerificationDialog.value = true
    }

    if (res.status == 'success') {
      $q.cookies.set('userId', res.userId);
      isLoggingin.value = false;
      return router.push('/')
    }

    notify('error', 'Server Error', res.msg);
    return isLoggingin.value = false;

  } catch (error) {
    isLoggingin.value = false;
    console.log(error);
  }
}
</script>

<template>
  <div
    class="q-py-md-sm q-py-lg q-px-md-xl bg-primary row items-center"
    style="min-height: 100dvh"
  >
    <div
      class="row q-col-gutter-x-lg q-col-gutter-y-xl items-center text-white q-mx-md-auto q-px-md-xl q-px-lg full-width"
      style="max-width: 1228px"
    >

      <div class="col-md col-12">
        <div class="text-h4 q-mb-md">Login</div>
        <q-form @submit.prevent="Login">
          <q-input
            outlined
            v-model="formLogin.email"
            type="email"
            label="Email"
            class="q-mb-md text-white"
            label-color="positive"
            dark
          />
          <q-input
            outlined
            v-model="formLogin.password"
            type="password"
            label="Password"
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
          <q-btn rounded type="submit" class="q-px-xl block q-my-md" color="positive" :loading="isLoggingin"
            >submit</q-btn
          >
          <div class="h6">
            <router-link to="">Forgot your password?</router-link>
          </div>
        </q-form>
      </div>

      <div class="col-md col-12">
        <div class="text-h4 q-mb-md">Register</div>
        <q-form @submit.prevent="Register()">
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
          <q-btn
            rounded
            class="q-px-xl"
            color="positive"
            type="submit"
            :loading="isRegistering"
            >submit</q-btn
          >
        </q-form>
      </div>
    </div>
    <email-verification-component
      v-if="showEmailVerificationDialog"
      :email="isRegistering?formRegister.email:formLogin.email"
      label="ONEDEX Account Verification"
    ></email-verification-component>
  </div>
</template>
