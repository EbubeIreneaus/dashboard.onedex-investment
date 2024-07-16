<script lang="ts" setup>
let referralLink = 'https://mysite.com/auth?r=20ekkdji949300309292029939303';
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
            <div class="text-h5">$0.00</div>
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
          investment they made with us.
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
          <q-icon name="content_copy"></q-icon>
        </template>
      </q-input>
      </div>
    </div>
  </div>
</template>
