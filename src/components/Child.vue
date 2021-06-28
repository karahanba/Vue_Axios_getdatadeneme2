<template>
  <div>
    <h2>Child Component</h2>
    <p>{{name}}</p>
    <p>{{info}}</p>
    <p>{{info.email}}</p>
    <button @click="getInfo"> Click me </button>
  </div>

  <div>
    <ChildOfChild/>
  </div>
</template>

<script>
import ChildOfChild from "./ChildOfChild";
//import {provide, reactive, ref} from "vue";
export default {
  name:'Child',
  props:{
    name: {type:String,default:'Ali'},
    info : Object,
    getInfo : Function

  },
  components:{ChildOfChild},
  setup(){
    /*const information1 = ref('Merhaba')
    const mypreciousobject = reactive({
      longitude:90,
      latitude:135
    })
    provide('information1',information1)
    provide('mypreciousobject',mypreciousobject)*/



    //Bunlar reactive değil
    /*provide('information1','Merhaba')
    provide('mypreciousobject',{
      longitude:90,
      latitude:135
    })*/
  }


}
</script>

<style scoped>

</style>