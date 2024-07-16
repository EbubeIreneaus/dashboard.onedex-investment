<script setup lang="ts">
import {useQuasar} from 'quasar'
import { useRouter} from 'vue-router'
useQuasar().cookies.remove('userId')
useRouter().push('/auth/signup')
</script>

