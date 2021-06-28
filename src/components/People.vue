<template>
  <div class="people">
    <hr/>
    People test
    <hr/>
    <div>
      <p ref="p">My name is {{name}} and my age is {{age}}</p>

      <button @click="handleClick">click for ref action</button>
    </div>

    <div v-for="user in randomUser" :key="user">
      First Name:{{user.first_name}} | Last Name:{{user.last_name}}| Title:{{user.employment.title}}
      <button @click="getRandomUser"> Get random user</button>
    </div>

<!--    <div v-if="randomUser.user !== undefined">
      <div v-for="user in randomUser" :key="user">
        First Name:{{user.first_name}} | Last Name:{{user.last_name}}| Title:{{user.employment.title}}
        <button @click="getRandomUser"> Get random user</button>
      </div>
    </div>-->
  </div>
</template>

<script>
//import {onBeforeMount, reactive, ref} from 'vue'
import {ref} from 'vue'
//import axios from "axios"; // yeni düzenleme ile burada axios'u import etmeye gerek kalmadı?

export default {
  name: 'People',
  props:{
    randomUser: Object,
    getRandomUser : Function
  },
  setup(){
    console.log('setup')

    //Data
    const p = ref(null) //In Vue 3.0 we can make any variable REACTIVE anywhere with a new ref function

    let name = 'Batuhan'
    let age = 25


    console.log(p)

    /*let randomUser = reactive({  //BUNU DA App.Vue 'A TAŞIMAK GEREKEBİLİR
      user: {
        first_name: "Default",
        last_name: "Default",
        employment: {
          title: "Default"
        }
      }
    });*/

    // Lifecycle Hooks
    /*onBeforeMount( () => {           //App.Vue 'A TAŞIDIM
       getRandomUser();
    })*/


    //Functions
    /*async function getRandomUser(){               //FONKSİYONUN İÇERİĞİ App.Vue 'DAN GELECEK ŞEKİLDE DÜZENLİYORUM.
      await axios
          .get('https://random-data-api.com/api/users/random_user')
          .then(response => randomUser.user = response.data)//console.log(response.data))//
    }*/
    const handleClick = () => {
      console.log(p.value.innerHTML)
      p.value.innerHTML='I like running and spending time with my friends in the nature.'
      console.log(p)
    }

    return{
      /* Data */
      name,
      age,
      p,
      //randomUser,
      /* Functions */
      handleClick,
      //getRandomUser

    }
  },
  created() {
    console.log('created')
  },
  mounted() {
    console.log('mounted')
  }
}
</script>

<style scoped>

</style>