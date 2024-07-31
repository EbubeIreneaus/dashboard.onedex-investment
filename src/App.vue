<template>
  <router-view  :userId="userId"/>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router';
import { useQuasar } from 'quasar';
import { provide, ref } from 'vue';
defineOptions({
  name: 'App'
});

const router = useRouter()
const $q = useQuasar()
let url = process.env.DEV?'http://127.0.0.1:8000/api': 'https://server.onedexinvestment.com/api'
let userId = ref(null)

function checkuser_and_getuser(){
  if ($q.cookies.has('userId')) {
    userId.value = $q.cookies.get('userId')
  }else{
    router.push('/auth')
  }
}
checkuser_and_getuser()
provide('backend', url)
provide('userId', userId.value )
</script>
