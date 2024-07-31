<template>
  <q-page class="q-px-lg">

    <!-- TradingView Widget BEGIN marquee -->
    <div class="tradingview-widget-container">
      <div class="tradingview-widget-container__widget twget"></div>
    </div>
    <!-- TradingView Widget END -->
    <div class="">
      <div class="row q-gutter-sm">
        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section class="row justify-between items-center">
            <div>
              <div class="text-h5">{{ currencyFormater(account.balance) }}</div>
              <div>Account Balance</div>
            </div>
            <q-icon
              name="account_balance_wallet"
              size="lg"
              color="secondary"
            ></q-icon>
          </q-card-section>
        </q-card>

        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section class="row justify-between items-center">
            <div>
              <div class="text-h5">{{ currencyFormater(account.active_investment) }}</div>
              <div>Active Investment</div>
            </div>
            <q-icon name="savings" size="lg" color="secondary"></q-icon>
          </q-card-section>
        </q-card>

        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section class="row justify-between items-center">
            <div>
              <div class="text-h5">{{ currencyFormater(account.pending_withdraw) }}</div>
              <div>Pending Withdrawal</div>
            </div>
            <q-icon name="account_balance" size="lg" color="secondary"></q-icon>
          </q-card-section>
        </q-card>

        <q-card class="bg-accent col-md col-12 q-py-md rounded-xl">
          <q-card-section class="row justify-between items-center">
            <div>
              <div class="text-h5">{{ currencyFormater(account.total_earnings) }}</div>
              <div>Total Earning</div>
            </div>
            <q-icon name="attach_money" size="lg" color="secondary"></q-icon>
          </q-card-section>
        </q-card>
      </div>
    </div>
    <div class="q-pa-md q-gutter-sm">
      <q-banner rounded class="bg-accent text-white">
        <div class="text-white text-body1 q-py-lg">
          Hello Ireneaus (Not Ireneaus?
          <router-link to="/auth/logout" class="text-white">Log Out</router-link
          >)
        </div>
        <div class="q-py-lg text-body1">
          From your account dashboard you can make
          <router-link to="/deposit" class="text-white">Deposit</router-link>,
          manage your
          <router-link to="/account" class="text-white">Account</router-link>,
          and initiate
          <router-link to="/withdrawal" class="text-white"
            >Withdrawal</router-link
          >.
        </div>
      </q-banner>
    </div>

    <!-- TradingView Widget BEGIN AAPL-->
    <div class="tradingview-widget-container bg-accent q-mb-md">
      <div class="tradingview-widget-container__widget TradingviewWidget1" style="height:400px"></div>
    </div>
    <!-- TradingView Widget END -->

    <q-table
      :columns="tableColumn"
      title="Orders"
      row-key="id"
      :rows="tableRow"
      class="bg-accent text-white"
    ></q-table>
  </q-page>
</template>

<script setup lang="ts">
// import { ref } from 'vue';
import { useMeta } from 'quasar';
import { MetaOptions } from 'quasar/dist/types/meta';
import { QTableColumn } from 'quasar';
import { inject, onMounted, ref } from 'vue';
import { currencyFormater } from 'src/composables/money';

const account = ref({
  balance: 0.00,
  active_investment: 0.00,
  pending_withdraw: 0.00,
  total_earnings: 0.00
})
const userId = inject('userId')
const backend = inject('backend')
defineOptions({
  name: 'IndexPage',
});
let meta: MetaOptions = {
  title: 'Dashboard',
  script: {
    livecoinWidgetQuee: {
      src: 'https://www.livecoinwatch.com/static/lcw-widget.js',
      defer: 'true',
    },
  },
};

useMeta(meta);

const tableColumn: QTableColumn[] = [
  { name: 'id', label: 'orderId', field: 'orderId', required: true, align: 'left' },
  {
    name: 'type',
    label: 'Type',
    field: 'type',
    required: true,
    align: 'left',
    sortable: true,
  },
  {
    name: 'channel',
    label: 'Channel',
    field: 'channel',
    required: true,
    align: 'left',
    sortable: true,
  },
  {
    name: 'amount',
    label: 'Amount(USD)',
    field: 'amount',
    required: true,
    align: 'left',
    sortable: true,
  },
  {
    name: 'status',
    label: 'Status',
    field: 'status',
    required: true,
    align: 'left',
    sortable: true,
  },

];

const tableRow = ref([])

async function getAccount(){
  let req = await fetch(`${backend}/accountInfo?id=${userId}`)
  account.value = await req.json()
}

async function getOrders() {
  let req = await fetch(`${backend}/order?id=${userId}`)
  tableRow.value = await req.json()

}

onMounted(() => {
  getAccount()
  getOrders()

  const twgetScript = document.createElement('script');
  twgetScript.type = 'text/javascript';
  twgetScript.src =
    'https://s3.tradingview.com/external-embedding/embed-widget-ticker-tape.js';
  twgetScript.async = true;
  twgetScript.innerHTML = JSON.stringify({
    symbols: [
      {
        proName: 'FOREXCOM:SPXUSD',
        title: 'S&P 500 Index',
      },
      {
        proName: 'FOREXCOM:NSXUSD',
        title: 'US 100 Cash CFD',
      },
      {
        proName: 'FX_IDC:EURUSD',
        title: 'EUR to USD',
      },
      {
        proName: 'BITSTAMP:BTCUSD',
        title: 'Bitcoin',
      },
      {
        proName: 'BITSTAMP:ETHUSD',
        title: 'Ethereum',
      },
    ],
    showSymbolLogo: true,
    isTransparent: true,
    displayMode: 'adaptive',
    colorTheme: 'dark',
    locale: 'en',
  });
  document.querySelector('.twget')?.append(twgetScript)
});
</script>
