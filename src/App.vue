<template>
  <h1>Crypto</h1>
  <Input :changeAmount="changeAmount" :convert="convert" :favorite="favorite"/> 
  <p v-if="error != ''" className="error header-info">{{ error }}</p>
  <p v-if="result != ''" className="result header-info">Результат: {{ result }}</p>
  <Favorite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>
  <div className="selectors">
    <Selector :setCrypto="setCryproFirst" :cryptoNow="cryptoFirst"/>
    <Selector :setCrypto="setCryproSecond" :cryptoNow="cryptoSecond"/>
  </div>
</template>

<script>

import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import Favorite from './components/Favorite.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default {
  components: {Input, Selector, CryptoConvert, Favorite},
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: []
    }
  },
  methods: {
    changeAmount(val) {
      this.amount = val;
    },
    setCryproFirst(val) {
      this.cryptoFirst = val;
    },
    setCryproSecond(val) {
      this.cryptoSecond = val
    },
    async convert() {
      this.result = '';
      if (this.amount <= 0) {
        this.error = 'Введите число больше нуля';
        return
      }
      else if (this.cryptoFirst == '' || this.cryptoSecond == '') {
        this.error = 'Выберите валюты';
        return
      }
      else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = 'Выберите разные валюты';
        return
      }


      this.error = '';
      await convert.ready();
      console.log(this.amount)
      this.result = convert[this.cryptoFirst][this.cryptoSecond](this.amount);
    },
    favorite() {
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond
      })
    },
    getFromFavs(index) {
      let currFav = this.favs[index];
      this.cryptoFirst = currFav.from;
      this.cryptoSecond = currFav.to;
    },
    
  }
}
</script>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
  margin-top: 20px;
}

.error { 
  color: rgb(200, 19, 19);
  font-size: 20px ;
}

.result {
  color: white;
  font-weight: bold;
  font-size: 25px;
}

.header-info {
  margin: 20px 0;
}
</style>
