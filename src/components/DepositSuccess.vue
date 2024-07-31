<script setup lang="ts">
import Swal from 'sweetalert2';
import { useCopy } from 'src/composables/clipboard';
import {ref} from 'vue'
type CryptoKey = 'BTC' | 'USDT' | 'ETH' ;
let dialog = ref(true);
// eslint-disable-next-line @typescript-eslint/no-explicit-any
const paymentOption: any = {
  BTC: { address: '1JwgsfZ2FPpmH9HVta68BwFU55kne8XH2v', img: 'https://cryptologos.cc/logos/bitcoin-btc-logo.png?v=032' },
  USDT: { address: 'TGKEfpfy7Lsv9gxPXRpQ2cTxAJnB6kCgZd', img: 'https://cryptologos.cc/logos/tether-usdt-logo.png?v=032' },
};
const props = defineProps(['channel'])
let crypto: CryptoKey = props.channel;
const cryptoAddress = paymentOption[crypto].address;

function madePayment(){
  dialog.value= false
  Swal.fire({
      title: 'Please Wait.',
      text: 'We have recieve your request and we are proccessing it.',
      icon: 'info',
      confirmButtonText: 'Cool',
      background: '#02022a',
      color: '#ffffff',
    });
}
</script>

<template>
  <div>
    <q-dialog v-model="dialog"  backdrop-filter="blur(4px) saturate(150%)">
      <q-card dark style="max-width: 350px; width: 100%">
        <q-card-section>
          <div class="text-body1">Confirm my payment</div>
        </q-card-section>
        <q-card-section>
          <q-img
            :src="paymentOption[crypto].img"
            :ratio="16 / 9"
            fit="scale-down"
          >
            <template v-slot:error>
              <div
                class="absolute-full flex flex-center bg-negative text-white"
              >
                Cannot load image
              </div>
            </template>
          </q-img>
        </q-card-section>
        <q-card-section>
          <div class="text-caption text-center q-py-md">
            kindly make deposit to the below wallet address
          </div>
          <q-input
            v-model="cryptoAddress"
            readonly
            standout
            dark
            label="Payment Wallet Address"
          >
            <template v-slot:append>
              <q-icon name="content_copy" @click="useCopy(cryptoAddress)"></q-icon>
            </template>
          </q-input>
        </q-card-section>
        <q-card-section>
          <q-btn color="accent" @click="madePayment">I have made my payment</q-btn>
        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>
