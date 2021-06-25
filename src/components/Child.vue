<template>
  <div>
    <h2>Child Component</h2>
    <p>{{name}}</p>
    <p>{{info}}</p>
    <p>{{info.email}}</p>
    <button @click="getInfo"> Click me </button>
  </div>
</template>

<script>
export default {
  name:'Child',
  props:{
    name: {type:String,default:'Ali'},
    info : Object,
    getInfo : Function

  },


}
</script>

<style scoped>

</style>