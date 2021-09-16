<template>
  <div id="app">
    <xinput placeholder="换行符输入演示"  :min_width=200 ></xinput>
  </div>
</template>
<style scoped>
#app{
  padding: 10px;
  border: 2px solid rgb(240, 99, 43);
}
</style>
<script>
import xinput from './components/Input'
export default ({
    components: {
    xinput
  },
  data:function(){
    return{
      disabled:'disabled'
    }
  }
})
</script>
