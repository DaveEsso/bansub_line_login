<template>
    <div>
        <h1>{{message}}</h1>
        <PersonsList/>
        <PersonsList/>
    </div>
</template>

<script>
import PersonsList from './PersonsList.vue'
export default {
  name: "ListData",
  components:{
    PersonsList
  },
  data(){
    return{
        message:"แสดงรายชื่อพนักงาน"
    }
  }
}
</script>

<style>

</style>