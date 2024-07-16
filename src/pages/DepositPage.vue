<script setup lang="ts">
import { reactive } from 'vue';

let paymentForm = reactive({
  amount: '',
  channel: 'BTC',
});

const options = [
  { value: 'BTC', label: 'Bitcion' },
  { value: 'ETH', label: 'Ethereum' },
  { value: 'USDT', label: 'USDT(TRC20)' },
];
</script>
<template>
  <div
    class="full-width row justify-center items-center q-pa-md"
    style="min-height: 400px"
  >
    <div style="max-width: 768px">
      <div class="text-h4 text-positive text-weight-bold text-center q-mb-md">
        Secured Payment Methods
      </div>
      <div class="text-body1 text-center q-mb-lg">
        Payment is 100% secured. Below are well integrated payment options in
        our platform.
      </div>

      <div>
        <q-input
          type="number"
          step="50"
          v-model="paymentForm.amount"
          label="Amount(USD)"
          label-color="positive"
          standout
          prefix="$"
          bg-color="black"
          class="text-white"
          dark
        />
      </div>
      <div class="q-pa-lg">
        <q-option-group
          v-model="paymentForm.channel"
          type="radio"
          :options="options"
          dark
          color="positive"

        >
          <template v-slot:label="opt">
            <div class="row items-center">
              <span class="text-teal">{{ opt.label }}</span>
              <!-- <q-icon :name="opt.icon" color="teal" size="1.5em" class="q-ml-sm" /> -->
            </div>
          </template>
        </q-option-group>
      </div>

      <q-btn color="positive" class="q-mt-md">save and continue</q-btn>
    </div>
  </div>
</template>
