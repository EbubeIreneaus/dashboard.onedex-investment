<script lang="tsx" setup>
import { reactive } from 'vue';

const plans = [
  { label: 'Bronze', value: 'bronze', min: 50, roi: '20%', duration: '24 hrs' },
  { label: 'Silver', value: 'silver',  min: 350, roi: '40%', duration: '48 hrs' },
  { label: 'Gold', value: 'gold', min: 900, roi: '60%', duration: '72 hrs' },
  { label: 'VIP', value: 'vip', min: 5000, roi: '80%', duration: '5 days' },
];
const investForm = reactive({
  plan: 'silver',
  amount: ''
})
</script>
<template>
  <div
    class="full-width row justify-center items-center q-pa-md "
    style="min-height: 400px"
  >
    <div style="max-width: 768px">
      <div class="text-h4 text-positive text-weight-bold text-center q-mb-md" >
        Invest In Your Feature, Invest Today
      </div>
      <div class="text-body1 text-center q-mb-lg">
        Investing with us 100% secured. Below are the investment plans in
        our platform.
      </div>

      <div>
        <q-input
          type="number"
          step="50"
          v-model="investForm.amount"
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
        <fieldset>
          <legend>Choose a plan</legend>
          <q-option-group
          v-model="investForm.plan"
          type="radio"
          :options="plans"
          dark
          color="positive"

        >
          <template v-slot:label="plan">
            <div class="row items-center">
              <span class="text-teal">{{ `${plan.label}($${plan.min}) ${plan.duration}` }}</span>
              <!-- <q-icon :name="opt.icon" color="teal" size="1.5em" class="q-ml-sm" /> -->
            </div>
          </template>
        </q-option-group>
        </fieldset>
      </div>

      <q-btn color="positive" class="q-mt-md">invest now</q-btn>
    </div>
  </div>
</template>
