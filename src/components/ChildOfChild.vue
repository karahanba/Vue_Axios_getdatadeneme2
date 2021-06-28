<template>
  <button @click="updateInfos"> Update for Provide/Inject</button>
  <div>
    {{myinfo}}+{{myprecious}}<br/>
    {{myprecious.longitude}} -- {{myprecious.latitude}}

  </div>
</template>

<script>
//import {inject, onUpdated} from "vue";
//import {inject, onBeforeMount} from "vue";
import {inject} from "vue";

export default {
  setup() {
    /*const myinfo = inject('information1','?')
    const myprecious = inject('mypreciousobject')*/

    let myinfo = inject('information1','?')
    let myprecious = inject('mypreciousobject')

    let updateInfos = async () => {//async () =>
      /*myinfo = 'iyi akşamlar',
      myprecious = {
        longitude:45,
        latitude:50
      },*/
      console.log(myinfo.value)
      console.log(myprecious.longitude)
      console.log(myprecious.latitude)

      myinfo.value='iyi akşamlar'
      myprecious.longitude=45
      myprecious.latitude=50
      //console.log(myinfo + myprecious.latitude + myprecious.longitude)

    }
    /*onUpdated(()=>{
      myinfo = 'iyi akşamlar',
          myprecious = {
            longitude:45,
            latitude:50
          }
      console.log('onUpdated')
    })*/

   /* onBeforeMount(async () => {
      await updateInfos();
    })
*/


    return{
      myinfo,
      myprecious,
      updateInfos
    }
  },


}
</script>
<!--

<style scoped>

</style>-->
