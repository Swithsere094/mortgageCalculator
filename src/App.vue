<script>
import rangeComponent from "./components/rangeComponent.vue"
import {ref} from "vue";
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';

export default {
  components: {
    rangeComponent,
  },
  setup(){
    const opParams = ref({})
    const loanAmount = ref(0);
    const repaymentTime = ref(0);
    return {
      opParams,
      loanAmount,
      repaymentTime,
    }
  },
  methods: {
    changeValue(value){
      this.opParams[value.type] = value.selectedValue;
    },
    calcMortgage(){
      const purchase = this.opParams.Purchase ?? 0;
      const down = this.opParams.Down ?? 0;
      const repayment = (this.opParams.Repayment ?? 2) * 12;
      const intest = (this.opParams.Intest ?? 1) / 100 / 12;

      console.log(`Purchase: ${purchase}`)
      console.log(`Down: ${down}`)
      console.log(`Repayment: ${repayment}`)
      console.log(`intest: ${intest}`)

      if(parseInt(purchase) <= parseInt(down)){
        console.log(purchase <= down)
        toast("Purchase price must be bigger than down payment!" , {autoClose:2000, type: 'info', theme:'dark'});
        return;
      }

      this.loanAmount = purchase-down;
      this.repaymentTime = this.loanAmount * (intest * (Math.pow((1 + intest),repayment)) / ((Math.pow((1 + intest),repayment)) - 1))
      this.repaymentTime = this.repaymentTime.toFixed(3)
    }
  }
}
</script>

<template>
  <main>
    <div class="container">
      <h1>Mortgage Calculator</h1>
      <div class="grid">
        <div class="item">
          <rangeComponent type="1" min="0" max="1000" subtitle="Purchase price:" v-on:changeValue="changeValue"/>
        </div>
        <div class="item">
          <!-- <h2>Down payment: </h2> -->
          <rangeComponent type="1" min="0" max="1000" subtitle="Down payment:" v-on:changeValue="changeValue"/>
        </div>
        <div class="item">
          <!-- <h2>Repayment time: </h2> -->
          <rangeComponent type="2" min="2" max="25" subtitle="Repayment time:" v-on:changeValue="changeValue"/>
        </div>
        <div class="item">
          <!-- <h2>Intest rate: </h2> -->
          <rangeComponent type="3" min="1" max="100" subtitle="Intest rate:" v-on:changeValue="changeValue"/>
        </div>
        <div class="item">
          <h2>Loan amount: </h2>
          <strong>{{ loanAmount }} $</strong>
        </div>
        <div class="item">
          <h2>Estimated pr.month: </h2>
          <strong>{{ repaymentTime }} $</strong>
        </div>
      </div>
      <button v-on:click="calcMortgage()">Get a mortgage quote</button>
    </div>
  </main>
</template>

<style scoped>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 98vw;
    height: 98vh;
  }
  .container{
    padding: 50px 20px;
    background-color: #e6e6e6;
    border-radius: 10px;
  }
  .container h1, .container button {
    margin-left: 7vw;
  }
  .container button{
    margin-top: 20px;
    padding: 25px 40px;
    font-size: 20px;
    border-radius: 7px;
    border: 0px;
    background-color: #866ac6;
    color: #fff;
  }
  .grid{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    justify-items: center;
    width: 80vw;
    padding: 50px;
  }
  .item {
    width: 72%;
    text-align: center;
  }
  .item h2 {
    font-weight: 600;
    margin-bottom: 10px;
  }
  .item strong {
    font-size: 30px;
  }
</style>


