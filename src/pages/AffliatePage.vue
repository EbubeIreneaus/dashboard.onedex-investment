<script lang="ts" setup>
import { useCopy } from 'src/composables/clipboard';
import { currencyFormater } from 'src/composables/money';
import { inject, onMounted, ref } from 'vue';
// import { useQuasar } from 'quasar';
// import { useNotify } from 'src/composables/notify';

// const $q = useQuasar();
const backend = inject('backend');
const userId = inject('userId');

const account = ref({
  balance: 0
})

let referralLink = ref('https://onedex-investment.com/auth?r=');

async function getAccount(){
  let req = await fetch(`${backend}/accountInfo?id=${userId}`)
  const res = await req.json()
  account.value = res
  referralLink.value = `https://dashboard.onedex-investment.com/auth?r=${res.user.id}`
}



onMounted(()=>{
  getAccount()
})
</script>
<template>
  <div>
    <div class="q-pa-lg">
      <div class="row q-gutter-x-sm">
        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section
            class="column justify-center items-center q-gutter-md"
          >
            <div class="text-h5">0</div>
            <div>Total Referrals</div>
          </q-card-section>
        </q-card>

        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section
            class="column justify-center items-center q-gutter-md"
          >
            <div class="text-h5">$0.00</div>
            <div>Total Commision</div>
          </q-card-section>
        </q-card>

        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section
            class="column justify-center items-center q-gutter-md"
          >
            <div class="text-h5">{{ currencyFormater(account.balance) }}</div>
            <div>Wallet Balance</div>
          </q-card-section>
        </q-card>

        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section
            class="column justify-center items-center q-gutter-md"
          >
            <div class="text-h5">$0.00</div>
            <div>Pending Commision</div>
          </q-card-section>
        </q-card>
      </div>

      <q-banner class="bg-accent text-positive q-my-lg">
        <div>
          Referr a family or friends today and earn 20% commision on every
          investment they made with us (coming soon.).
        </div>
      </q-banner>

      <div>
        <q-input
          v-model="referralLink"
          readonly
          standout
          dark
          label="My Referral Link"
        >
        <template v-slot:append>
          <q-icon name="content_copy" @click="useCopy(referralLink)"></q-icon>
        </template>
      </q-input>
      </div>
    </div>
  </div>
</template>
