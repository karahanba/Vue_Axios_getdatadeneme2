<template>
<!--  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->

<!--  <div :class="classObject"></div>-->

<!--  <div v-if="type === 'A'">
    A
  </div>
  <div v-else-if="type === 'B'">
    B
  </div>
  <div v-else-if="type === 'C'">
    C
  </div>
  <div v-else>
    Not A/B/C
  </div>-->
  <div v-for="item in currencyExchangeRates.value" :key="item">
    <div>
      {{item.code}} | <span v-html="item.symbol"/> | {{item.rate}}
    </div>
  </div>

  <button @click="getCurrencyExchangeData()">Refresh</button>

  <hr/>

  <div>
    {{randomNumbers}}

    <div v-for="(item,i) in randomNumbers.number" :key="i">{{item}}</div>

    <button @click="getRandomNumberList()">Get New Random Numbers!</button>
  </div>

  <div>

    <People :getRandomUser="getRandomUser" :randomUser="randomUser" />

  </div>

  <div>
    <Child :name="name" :info="desiredInfo.kullanici" :getInfo="getInfo"/>
  </div>


</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import axios from "axios";
import {onBeforeMount, provide, reactive, ref} from "vue";
import People from './components/People.vue'

import Child from "./components/Child.vue";
//import ChildOfChild from "./components/ChildOfChild.vue";

export default {
  name: 'App',
  components:{
    Child,
    People
  },
  /*props:{
    //something:{i1:'asds',i2:'asds'}

  },*/
  setup(){
    // Data
    let currencyExchangeRates = reactive({
      value: undefined
    });

    let randomNumbers = reactive({
      number: undefined
      //list: [1,2,3]
    });

    let desiredInfo = reactive({ // Child componenti için tanımlandı.önceden reactive değildi?
      kullanici:{
        name: 'Batuhano',
        email: 'Batuhan@test'
      }});

    // if a repository, randomUser for example, is not reactive.
    // This means from a user's perspective, the repository list would remain empty.
    let randomUser = reactive({  //DAHA ÖNCE People.Vue İÇERİSİNDE TANIMLANIYORDU
      user: {
        first_name: "Default",
        last_name: "Default",
        employment: {
          title: "Default"
        }
      }
    });

    // Lifecycle Hooks
    onBeforeMount(async () => {
      await getCurrencyExchangeData();
      await getRandomNumberList();//?
    })
    onBeforeMount( () => { //People.vue
      getRandomUser();
    })


    // Functions
    async function getCurrencyExchangeData(){
      await axios
          .get('https://api.coindesk.com/v1/bpi/currentprice.json')
          .then(response => currencyExchangeRates.value = response.data.bpi)
    }

    async function getRandomNumberList(){
      await axios.get('https://www.random.org/integers/?num=10&min=1&max=6&col=1&base=10&format=plain&rnd=new')//'http://www.randomnumberapi.com/api/v1.0/random')
                 .then(response =>randomNumbers.number = response.data.split('\n'))//console.log(response.data))
    }

    async function getInfo(){//For Child component
      await alert("Function Called")

    }

    async function getRandomUser(){               //BU FONKS. DAHA ÖNCE People.Vue İÇERİSİNDE TANIMLANIYORDU
      await axios
          .get('https://random-data-api.com/api/users/random_user')
          .then(response => randomUser.user = response.data)//console.log(response.data))//
    }


    const information1 = ref('Merhaba')
    const mypreciousobject = reactive({
      longitude:90,
      latitude:135
    })
    provide('information1',information1)
    provide('mypreciousobject',mypreciousobject)


    //Bunlar reactive değil
    /*provide('information1','Merhaba')
    provide('mypreciousobject',{
      longitude:90,
      latitude:135
    })*/


    return{
      /* Data */
      currencyExchangeRates,
      randomNumbers,
      /*kullanici:{
        name: 'Batuhano',
        email: 'Batuhan@test'
      },*/
      desiredInfo,
      name:'Batuhanno',
      randomUser, //People.vue


      /* Functions */
      getCurrencyExchangeData,
      getRandomNumberList,
      getInfo,
      getRandomUser //People.vue

    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
