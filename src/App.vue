<template>
  <div id="app">
    <img
      alt="Vue logo"
      src="./assets/logo.png"
      style="
        border: 1px solid #ddd;
        border-radius: 4px;
        padding: 0px;
        width: 50px;
        cursor: pointer;
        box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
      "
    />
    <h1>Currency Exchange App</h1>
    <div class="container">
      <div class="contaner-one">
        <select name="first-currency" id="first-currency" v-model="currency_one" >
          <option value="IND">IND</option>
          <option value="USD">USD</option>
          <option value="ENG">ENG</option>
          <option value="RUS">RUS</option>
          <option value="JPN">JPN</option>
          <option value="EUR">EUR</option>
          <option value="DEN">DEN</option>
          <option value="BCCI">BCCI</option>
          <option value="ICC">ICC</option>
          <option value="SAP">SAP</option>
        </select>
        <input type="number" name="input-one" id="input-one" v-model="amountOne" @input="fetchData()"/>
      </div>
      <div class="container-two">
        <button @click="switchValues();">Switch</button>
        <h4 id="baseValue">1{{currency_one}} = {{rate}} {{currency_two}}</h4>
      </div>
      <div class="conatiner-three">
         <select name="second-currency" id="second-currency" v-model="currency_two" >
          <option value="IND">IND</option>
          <option value="USD">USD</option>
          <option value="ENG">ENG</option>
          <option value="RUS">RUS</option>
          <option value="JPN">JPN</option>
          <option value="EUR">EUR</option>
          <option value="DEN">DEN</option>
          <option value="BCCI">BCCI</option>
          <option value="ICC">ICC</option>
          <option value="SAP">SAP</option>
        </select>
        <input type="number" name="input-two" id="input-two" placeholder="0" disabled v-model="amountTwo"/>
      </div>
      <div class="conatiner-four">
        <h4 id="lastlyUpdated">Lastly Updated : <strong>{{data.date}}</strong></h4>
      </div>
    </div>
    <!-- <h1>Something New</h1> -->
  </div>
</template>

<script>
export default {
  name: "App",
  data(){
    return{
      data:[],
      currency_one:"EUR",
      currency_two:"USD",
      rate:"",
      amountOne : 1,
      amountTwo : 0,
    }
  },
  components: {},
  methods:{
    fetchData(){
      fetch('http://api.exchangeratesapi.io/v1/latest?access_key=2e55d3899fb71cf12c0d57409aa06873')
      .then (res=>res.json())
      .then (data =>{
        this.data = data;
        this.rate = data.rates[this.currency_two];
        this.amountTwo= this.amountOne * this.rate.toFixed(2);
      })
    },
    switchValues(){
      const tempval = this.currency_one;
      this.currency_one = this.currency_two;
      this.currency_two = tempval;
      this.fetchData();
    }
  },
  mounted(){
    this.fetchData();
  }
};
</script>

<style>
html {
  background: #f4f4f4;
}
#app {
  font-family: "Seoge-UI", Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  align-items: center;
  align-content: center;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
h1 {
  color: rgb(0, 0, 0);
}
.container{
border: 1px solid black;
display: inline-block;
align-items: center;
width: 300px;
}
.container-two{
  display: space-between;
}
.container-two button {
  margin-top: 5px;
  padding: 5px;
  font-size: 18px;
  background-color: rgba(49, 219, 19, 0.349);
  color: black;
  width: 30%;
  height: 10%;
  border: none;
  outline: none;
  cursor: pointer;
}
select {
  padding: 5px;
  margin: 5px;
  border: 1px solid black transparent;
  outline: none;
}
input {
  padding: 5px;
  margin: 5px;
  border: 1px solid black transparent;
  outline: none;
}
#lastlyUpdated {
  font-weight: 500;
}
#baseValue {
  font-weight: 500;
}
/*@import'~bootstrap/dist/css/bootstrap.css'*/
</style>
