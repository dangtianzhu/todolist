<template>
  <div class="container">
    <div>
      已完成{{isComplete}} / 全部{{list.length}}
    </div>
    <div v-if="isComplete > 0" class="btn">
      <button @click="clear">清除已完成</button>
    </div>
  </div>
</template>

<script>
import {defineComponent,ref} from 'vue'
export default defineComponent ({
    name: 'navFooter',
    props:{
      list:{
        type: Array,
        required: true
      }
    },
    setup() {
      let isComplete = ref(1)
     
      let clear = ()=>{
        console.log("clear")
      }
      return {
        isComplete,
        
      }
        
    }
 
})
</script>

<style lang="less" scoped>

</style>
