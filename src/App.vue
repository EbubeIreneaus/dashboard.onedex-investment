<template>
  <router-view  :userId="userId"/>
</template>

<script setup lang="ts">
import { inject, provide} from 'vue';
defineOptions({
  name: 'App'
});

let url = process.env.DEV?'http://127.0.0.1:8000/api': 'https://server.onedex-investment.com/api'
provide('backend', url)
let userId = inject('userId')
</script>
