/* eslint-disable */
<template>
  <div class="hello">
    <div id="crypto-container" v-for="(value, key) in cryptos">
      <span class="left">{{key}}</span>
      <span class="right">${{value.USD}}</span>
      <span class="right">£{{value.GBP}}</span>
      <span class="right">€{{value.EUR}}</span>
    </div>
  </div>
</template>

<script>
// add axios
import axios from "axios";

export default {
  name: "HelloWorld",
  data: () => ({
    cryptos: [],
    errors: []
  }),

  created() {
    // retrieve API endpoint, capture data
    axios
      .get(
        "https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,IOT&tsyms=USD,EUR,GBP"
      )
      .then(response => {
        this.cryptos = response.data;
        console.log(response.data);
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  background: #f1f1f1;
}
#crypto-container {
  background: white;
  width: 80%;
  margin: 0 auto 4px auto;
  padding: 1em;
  box-shadow: 1px 1px 0 lightgrey;
}
span.left {
  font-weight: bold;
}
span.right {
  padding-left: 1.5em;
  float: right;
}
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  list-style: none;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
