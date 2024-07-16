<template>
  <q-layout view="lHh Lpr lFf" class="bg-primary text-white">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          {{ activePage }}
        </q-toolbar-title>

        <q-btn round class="q-mx-lg">
          <q-avatar>
            <img src="../assets/admin-user.jpg" alt="" />
          </q-avatar>
          <q-menu class="bg-accent text-white">
            <div class="row no-wrap q-pa-md">
              <!-- <div class="column">
                <div class="text-h6 q-mb-md">Settings</div>
              </div>

              <q-separator vertical inset class="q-mx-lg" /> -->

              <div class="column items-center">
                <q-avatar size="72px">
                  <img src="../assets/admin-user.jpg" />
                </q-avatar>

                <div class="text-subtitle1 q-mt-md q-mb-xs">Ebube Ireneaus</div>

                <q-btn
                  color="primary"
                  label="Logout"
                  push
                  size="sm"
                  v-close-popup
                />
              </div>
            </div>
          </q-menu>
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      class="bg-primary"
      elevated
    >
      <q-list class="full-height text-white" padding>
        <q-item-label header class="q-py-lg"> </q-item-label>

        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
          @click="activePage = link.title"
          class="q-mb-md"
        />
      </q-list>
    </q-drawer>

    <q-page-container class="">
      <div
        class="livecoinwatch-widget-5"
        lcw-base="USD"
        lcw-color-tx="#999999"
        lcw-marquee-1="coins"
        lcw-marquee-2="movers"
        lcw-marquee-items="10"
      ></div>

      <router-view />

      <div
        class="tradingview-widget-container q-mt-lg"
        style="height: 400px; width: 100%"
      >
        <div
          class="tradingview-widget-container__widget TradingviewWidget2 text-white full-height full-width"
        ></div>
        <div class="tradingview-widget-copyright">
          <a
            href="https://www.tradingview.com/"
            rel="noopener nofollow"
            target="_blank"
            ><span class="blue-text">Track all markets on TradingView</span></a
          >
        </div>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import EssentialLink, {
  EssentialLinkProps,
} from 'components/EssentialLink.vue';

defineOptions({
  name: 'MainLayout',
});

const activePage = ref<string>('Dashboard');

const linksList: EssentialLinkProps[] = [
  {
    title: 'Dashboard',
    icon: 'dashboard',
    link: '/',
  },
  {
    title: 'Profile',
    icon: 'manage_accounts',
    link: '/account',
  },
  // {
  //   title: 'Wallet',
  //   icon: 'account_balance_wallet',
  //   link: '',
  // },
  {
    title: 'Deposit',
    icon: 'payments',
    link: '/deposit',
  },
  {
    title: 'Invest',
    icon: 'savings',
    link: '/invest',
  },
  {
    title: 'Withdraw',

    icon: 'account_balance',
    link: '/withdraw',
  },
  {
    title: 'Affliate',
    icon: 'diversity_2',
    link: '/affliate',
  },
  {
    title: 'Logout',
    icon: 'logout',
    link: '/auth/logout',
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
onMounted(() => {
  const TradingViewscript1 = document.createElement('script');
  TradingViewscript1.type = 'text/javascript';
  TradingViewscript1.async = true;
  TradingViewscript1.src =
    'https://s3.tradingview.com/external-embedding/embed-widget-forex-cross-rates.js';
  TradingViewscript1.innerHTML = JSON.stringify({
    width: '100%',
    height: '100%',
    currencies: ['EUR', 'USD', 'JPY', 'GBP', 'CHF', 'AUD', 'CAD', 'NZD'],
    isTransparent: false,
    colorTheme: 'dark',
    locale: 'en',
    backgroundColor: '#02023f',
  });
  document.querySelector('.TradingviewWidget1')?.append(TradingViewscript1);

  const TradingviewWidget2 = document.createElement('script');
  TradingviewWidget2.type = 'text/javascript';
  TradingviewWidget2.src =
    'https://s3.tradingview.com/external-embedding/embed-widget-advanced-chart.js';
  TradingviewWidget2.async = true;
  TradingviewWidget2.innerHTML = JSON.stringify({
    autosize: true,
    symbol: 'BINANCE:BTCUSDT',
    interval: 'D',
    timezone: 'Etc/UTC',
    theme: 'dark',
    style: '1',
    backgroundColor: '#02023f',
    locale: 'en',
    allow_symbol_change: true,
    calendar: false,
    support_host: 'https://www.tradingview.com',
  });
  document.querySelector('.TradingviewWidget2')?.append(TradingviewWidget2);
});
</script>
