<script setup lang="ts">
import { ref, reactive, computed, watch, toRef } from 'vue';

// const itemName1 = ref<String>("Desk");
const itemName2 = "Bike";

const item1 = reactive({
  name: "Deck",
  price: 40000
});

// const price1 = 40000;
const price2 = 20000;

const url1 = "https://www.amazon.co.jp/VECELO-%E3%83%A9%E3%83%83%E3%82%AF%E4%BB%98%E3%81%8D%EF%BC%88A4%E5%AF%BE%E5%BF%9C%EF%BC%89%E3%83%A9%E3%82%B9%E3%83%86%E3%82%A3%E3%83%83%E3%82%AF%E3%83%96%E3%83%A9%E3%82%A6%E3%83%B3-%E5%B9%85120%C3%97%E5%A5%A5%E8%A1%8C60cm-%E3%80%90%E6%97%A5%E6%9C%AC%E6%AD%A3%E8%A6%8F%E8%BC%B8%E5%85%A5%E5%93%81%E3%80%91-DX-T01-02/dp/B08P2RZWQP/ref=sr_1_1?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&crid=E5SBURPHDBC&dib=eyJ2IjoiMSJ9.iQP5v9kWZxukHSFwiDwqlQfOYsp7628yF1wn_nle3dHlr5X4akUfTdXaZsClGi-DrE-tAuShyreZnC7sayNwKr3R2Cpt_Sf6a98G93xLbQkVNp60QurTIaG3o-r-1ONJ2nYwFDQIQZMZc7Pm25Y9i5cEcl67ZxeFrQ-igdl62G9V9N-vVbECT4xHBnw_YyMXYY_x5Den2FVzc0yP0r08cFbANgyqULq-A7ScKrIzw3K8L8X07QJr2fVh0CsIoDiYSAZeeYTIQFzlyxBuzZ1FX1Mek9oH_UoIF_Nrt0gErAE.5SPcjhh1kIrPTCZyYVONHkAqmJCVGYt-JRDHV36un4w&dib_tag=se&keywords=desk&qid=1708753143&sprefix=desk%2Caps%2C308&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"

const buy = (itemName: string) => {
  alert('Are you sure to buy' + itemName + "?");
}

const input = (event: any) => {
  item1.name = event.target.value;
}

const inputPrice = (event: any) => {
  item1.price = event.target.value;
}

const clear = () => {
  item1.name = '';
  item1.price = 0;
}

const budget = 50000;

// computedは条件に応じて表示を変更したい場合に使用する
// const priceLabel = computed(() => {
//   if (item1.price > budget) {
//     return "too expensive ...";
//   } else {
//     return item1.price + "yen";
//   }
// });

const priceLabel = ref<String>(item1.price + "yen");
const { price } = toRef(item1);
watch(price, () => {
  if (price.value > budget) {
    price.value = "too expensive ...";
  } else {
    price.value + "yen";
  }
});

</script>

<template>
  <div class="container">
    <h1>Payment</h1>
    <input v-model="item1.name" />
    <input v-model="item1.price" />
    <button v-on:click="clear">Clear</button>
    <div class="payment">
      <label>{{ item1.name }}</label>
      <!-- <label>{{ item1.price }} yen</label> -->
      <label>{{ priceLabel }}</label>
      <a v-bind:href=url1> bought at...</a>
      <button v-on:click="buy(item1.name)">BUY</button>
    </div>
    <div class="payment">
      <label>{{ itemName2 }}</label>
      <label>{{ price2 }} yen</label>
      <button v-on:click="buy(itemName2)">BUY</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background-color: aliceblue;
  margin-bottom: 8px;
}
input {
  margin-bottom: 8px;
}

label {
  font-size: 20px;
  font-weight: bold;
}
</style>