<script lang="ts" setup>
import { reactive } from 'vue';

let balance = '70.00';
const withdrawForm = reactive({
  wallet: '',
  channel: '',
  amount: '',
});
</script>

<template>
  <div class="q-pa-lg">
    <q-banner class="bg-accent q-py-md q-px-lg" dark>
      <div>Wallet Balance</div>
      <div class="text-h4 q-my-sm">${{ balance }}</div>
      <div></div>
    </q-banner>

    <div>
      <fieldset class="q-pa-lg q-my-lg" style="max-width: 768px">
        <legend>Wallet Information</legend>
        <q-form spellcheck="off">
          <q-input
            v-model="withdrawForm.channel"
            dark
            label="crypto channel eg USDT"
            label-color="positive"
            standout
            class="q-mb-md"
          ></q-input>
          <q-input
            v-model="withdrawForm.amount"
            dark
            label="Amount"
            label-color="positive"
            standout
            class="q-mb-md"
          ></q-input>
          <q-input
            v-model="withdrawForm.wallet"
            dark
            label="Wallet Address"
            label-color="positive"
            standout
            class="q-mb-md"
          ></q-input>
          <br />
          <q-btn color="positive">Initiate Withdraw</q-btn>
        </q-form>
      </fieldset>
    </div>
  </div>
</template>
